---
type: Reference
title: Sending Infrastructure
description: The transport layer beneath every channel, what an MTA is and how the SMTP conversation works, how a push token routes through APNs and FCM, how SMS reaches the carrier through an aggregator, and the webhook feedback path that carries bounces, delivery receipts, and dead tokens back to suppression.
tags: [infrastructure, mta, smtp, apns, fcm, smpp, webhooks, dsn, transport, delivery]
timestamp: 2026-06-15T00:00:00Z
---

## What it is

Between the moment a programme decides to send and the moment a message reaches a device sits a transport layer most operators never see, because the [ESP](/foundations/esp-selection.md) or messaging platform hides it. It is worth understanding anyway, because its failure modes surface as the metrics you do see: a bounce, a dead push token, a delivery receipt that never arrives. This is the plumbing under [email](/channels/email.md), [push](/channels/push.md), [browser push](/channels/browser-push.md), and [SMS](/channels/sms-and-rcs.md), and the asynchronous path that carries the result back to your [suppression](/foundations/consent-and-preferences.md) and [measurement](/measurement/index.md).

## The shape every channel shares

You never hand a message to a recipient's device directly. You hand it to a gateway that owns the last hop, an MTA for email, a push service for push, an aggregator for SMS, and that gateway relays it onward and reports back later. Every channel is the same two directions:

* **Outbound, the relay chain.** Your system submits the message to a gateway over an authenticated connection. The gateway queues it, finds the next hop (a receiving mail server, Apple's or Google's push service, a mobile carrier), and forwards it, often through one or two more relays before the device.
* **Inbound, the feedback path.** The result, accepted, bounced, delivered, opened, clicked, or undeliverable because the address or token is dead, comes back asynchronously, sometimes seconds later, sometimes hours. It almost never returns on the same connection that sent the message. Consuming it correctly is what keeps a list clean and a metric honest.

The synchronous response at send time tells you only that the next hop accepted custody, not that the message arrived. Treating acceptance as delivery is the most common misreading of the whole layer.

## Email: the MTA and the SMTP conversation

A **Mail Transfer Agent** (MTA) is the server program that routes email between hosts over SMTP (RFC 5321). Postfix, Exim, PowerMTA, and Haraka are MTAs. The path has three named roles: a **Mail Submission Agent** (MSA) accepts the message from your application on the submission port, the MTA relays it across the internet to the recipient domain, and a **Mail Delivery Agent** (MDA) drops it into the destination mailbox. An ESP is, at bottom, a fleet of MTAs with reputation management, queueing, and analytics wrapped around them.

The MTA finds where to send by looking up the recipient domain's **MX records** in DNS, which list the receiving mail servers in priority order. It then opens an SMTP session and runs a scripted conversation, where the receiver answers every command with a three-digit code (`2xx` accepted, `4xx` temporary failure, retry later, `5xx` permanent failure):

```text
EHLO mail.sender.com
MAIL FROM:<bounce@sender.com>      ← the envelope sender (return-path)
RCPT TO:<user@example.com>         ← the envelope recipient
DATA                               ← then the headers and body, ending with .
```

The **envelope** addresses in `MAIL FROM` and `RCPT TO` are what actually route the mail and are separate from the `From:` and `To:` headers the recipient sees (RFC 5322). The envelope sender, the return-path, is where bounces go, which is why it is a `bounce@` address you control, not the visible `From`. A receiver can reject at `RCPT TO` (unknown user) or after `DATA` (content or policy), and where in the conversation it rejects tells you why.

Ports carry meaning. Submission from an application uses **587** (or implicit-TLS **465**); port **25** is for server-to-server relay and is widely blocked outbound on consumer networks to curb spam. Transport security is opportunistic by default: `STARTTLS` (RFC 3207) upgrades a plaintext session to TLS if both sides support it, and because that handshake can be stripped, **MTA-STS** (RFC 8461) lets a domain demand TLS and **TLS-RPT** (RFC 8460) reports failures.

Running your own MTA means owning IP warming, reputation, retry and queue policy, bounce parsing, feedback-loop processing, and the authentication records, which is why most programmes rent an ESP's fleet instead. Self-hosting is defensible only at volume where per-message cost dominates and you have the deliverability expertise to run it. The [authentication](/foundations/authentication.md) records (SPF, DKIM, DMARC) and the warming and reputation work in [deliverability](/foundations/deliverability.md) are what that fleet exists to manage.

## Email bounces and feedback loops

A bounce arrives one of two ways. A **synchronous** bounce is a `5xx` rejection during the SMTP session, the receiver refuses the message before accepting it, and your MTA knows immediately. An **asynchronous** bounce comes after the receiving server accepted the message and then could not deliver it: it generates a **Delivery Status Notification** (DSN, RFC 3464) and mails it back to the envelope return-path minutes or hours later. Your inbound processing has to parse that DSN, classify it as hard or soft, and feed hard bounces to suppression before the next send, as [deliverability](/foundations/deliverability.md) requires. DSN wording is inconsistent across providers, so reliable bounce classification is real engineering, and getting it wrong, retrying a hard bounce, is a fast route into spam.

Separately, a **feedback loop** (FBL) reports spam complaints. When a recipient hits "report spam" at a participating provider, the provider sends you a copy in **Abuse Reporting Format** (ARF, RFC 5965) so you can suppress that address. You have to register for each provider's FBL and wire the reports into suppression; an ESP does this for you.

## Push: tokens and the push service

A push notification cannot be addressed to a phone. It is addressed to a **device token**, an opaque string the operating system issues to a specific app install on a specific device, and you send not to the device but to the platform's push service, which holds the only live connection to it. The flow: the app registers for notifications, the OS returns a token, the app sends that token to your server, and your server presents it to the push service when sending.

* **APNs (Apple).** You send over a persistent **HTTP/2** connection, one request per notification, authenticated either with a **JWT provider token** (a signed ES256 bearer you rotate, the modern default) or a legacy TLS client certificate. Request headers carry the routing and delivery policy: `apns-topic` (your bundle id), `apns-push-type` (`alert`, `background`, `voip`, …), `apns-priority`, `apns-expiration` (how long APNs stores it for a offline device), and `apns-collapse-id` (replace an undelivered notification with the same id rather than stacking it).
* **FCM (Google, also Chrome and Edge web push).** The current **HTTP v1** API takes a JSON message authenticated with a short-lived **OAuth 2.0 bearer** minted from a service-account key. It exposes the same delivery controls under different names: collapse key, TTL, and priority.

The token is not stable. It rotates on app reinstall, OS restore, and at the platform's discretion, so a token you hold can silently go dead. The push service tells you when: APNs returns **410** with `Unregistered`, FCM returns `UNREGISTERED` or `NOT_REGISTERED`. Pruning those tokens the moment they come back is the push equivalent of suppressing a hard bounce, and skipping it wastes send budget and muddies reach. Because each request targets one token, reaching a large audience is a fan-out of many requests, which is the multiplexing the persistent HTTP/2 connection exists to make cheap. [Browser push](/channels/browser-push.md) is the same model behind the Web Push protocol, with VAPID identifying your server to each browser's push service.

## SMS: aggregators, SMPP, and delivery receipts

You do not connect to mobile carriers directly. An **aggregator** (the messaging side of a CPaaS such as Twilio, Sinch, or Vonage) holds the carrier interconnects and routes your message onto the right network. You reach the aggregator one of two ways: a modern **HTTP REST API**, or **SMPP** (Short Message Peer-to-Peer), the binary telecom protocol that the REST APIs themselves sit on top of. An SMPP integration opens a long-lived TCP session and **binds** as a transmitter (send only), receiver (receive only), or transceiver (both), then exchanges `submit_sm` PDUs for outbound and `deliver_sm` for inbound.

Two directions have names here: **MT** (mobile-terminated) is the message you send to a handset; **MO** (mobile-originated) is a reply coming back, which is how `STOP` and `HELP` keywords arrive. Delivery confirmation comes as a **DLR** (delivery receipt) relayed back from the carrier through the aggregator. Treat DLRs as advisory, not truth: carriers vary in whether and how quickly they return them, some report "delivered" on handoff rather than handset receipt, and a missing DLR does not reliably mean a missing message. The US registration regimes that gate this traffic, 10DLC, short codes, and toll-free, are on the [SMS and RCS](/channels/sms-and-rcs.md) page; here they are the carrier's admission control sitting in front of the aggregator route.

## The feedback path: webhooks and events

Almost everything you learn after acceptance, an asynchronous bounce, a spam complaint, a DLR, an open, a click, a dead token, arrives by **webhook**: the provider makes an HTTP POST to an endpoint you expose, carrying an event payload. Handling that endpoint well is what turns the transport layer into clean data, and it has standard hazards:

* **At-least-once delivery.** Providers retry on any non-`2xx` or timeout, so the same event can arrive more than once. Deduplicate on the event id and make the handler **idempotent**, because processing a delivery twice double-counts a metric and processing a suppression twice is merely wasteful, but the asymmetry is why you design for replay.
* **Authenticate the payload.** Your endpoint is public, so verify each request is genuinely from the provider before acting on it, normally by checking an **HMAC signature** computed over the body with a shared secret. An unauthenticated webhook endpoint is a way to poison your own suppression list and metrics.
* **Ordering is not guaranteed.** A `delivered` can arrive before the `sent` it follows. Key state on the message id and tolerate out-of-order arrival rather than assuming sequence.
* **Acknowledge fast, process later.** Return `2xx` immediately and queue the work, because a slow handler triggers the provider's retry and timeout logic and amplifies load. Where a provider offers no webhook, you fall back to **polling** an events API, which is simpler but laggier and heavier.

This path, not the send-time response, is where suppression gets fed and where the engagement numbers in [core metrics](/measurement/core-metrics.md) originate, which is why their caveats trace back to how reliably each event is reported.

## Why this matters more at scale

At a few thousand sends a month the platform hides this layer completely and you can ignore it. At the volume a large business runs, tens or hundreds of millions of messages, the abstraction leaks and every mechanism above turns into an operational lever with money attached.

* **Throughput becomes a negotiated ceiling.** Email throughput is bounded by how many concurrent SMTP connections receivers tolerate from your IPs and how fast they drain, push by how well you multiplex the HTTP/2 fan-out, SMS by the per-second rate your route is provisioned for. At scale you provision for peak: dedicated IP pools warmed and segmented by traffic type, short codes or high-throughput SMPP binds with carrier-negotiated TPS, and connection and queue tuning that a low-volume sender never touches.
* **Reputation fragments and has to be managed deliberately.** Reputation is per sending domain and per IP, so a large programme runs pools, separating transactional from marketing and high-engagement from reactivation, and warms and monitors each independently. A single shared reputation that was fine at low volume becomes a liability when one careless segment can drag the whole estate toward spam.
* **The feedback path becomes its own high-volume system.** Millions of sends generate millions of bounces, DLRs, complaints, and dead-token notifications, and the webhook ingestion that consumes them is itself a throughput problem: idempotent, queued, and resilient to provider retries and bursts. Suppression hygiene that is trivial by hand becomes pipeline engineering, and getting it wrong is now expensive in both deliverability and spend.
* **The build-versus-buy line can move.** Per-message margin is negligible at low volume and dominant at high volume, which is the one place self-hosting an MTA fleet, running direct carrier or SMPP connections, or going multi-provider for failover and rate headroom starts to pay for the deliverability and reliability expertise it demands. Most businesses still buy; the largest senders run hybrids precisely because at their volume the mechanics on this page are the cost base, not an implementation detail.

> [!note] The same plumbing, different stakes
> Nothing here changes between a small sender and a large one. What changes is that at scale a leak in any of it, a throttled IP pool, an unprocessed bounce stream, an underprovisioned SMS route, stops being an inconvenience and becomes a capacity ceiling or a deliverability incident measured in revenue.

## What the platform abstracts

An ESP, a CPaaS, or a push relay exists to hide most of this: the MTA fleet and its queues, the SMPP binds and carrier interconnects, the HTTP/2 connection pooling and token rotation, the warming and reputation. What it cannot do for you is consume the result. You still own the webhook endpoint, the bounce and DLR handling, the dead-token pruning, and the discipline of feeding all of it back into suppression and measurement. The build-versus-buy line is almost always buy, because the value is in the reliability and reputation of the relay, not in the protocol code, and the [ESP selection](/foundations/esp-selection.md) factors are largely a way of judging how well a vendor runs this layer on your behalf.

## Related

* [Email](/channels/email.md)
* [Authentication](/foundations/authentication.md)
* [Deliverability](/foundations/deliverability.md)
* [Push](/channels/push.md)
* [Browser push](/channels/browser-push.md)
* [SMS and RCS](/channels/sms-and-rcs.md)
* [ESP selection](/foundations/esp-selection.md)
* [Transactional messaging](/foundations/transactional-messaging.md)
* [Core metrics](/measurement/core-metrics.md)

## Citations

[1] [RFC 5321, Simple Mail Transfer Protocol (the SMTP conversation and response codes)](https://www.rfc-editor.org/rfc/rfc5321)
[2] [RFC 5322, Internet Message Format (header fields, distinct from the SMTP envelope)](https://www.rfc-editor.org/rfc/rfc5322)
[3] [RFC 6409, Message Submission for Mail (submission on port 587, distinct from relay)](https://www.rfc-editor.org/rfc/rfc6409)
[4] [RFC 3207, SMTP Service Extension for Secure SMTP over TLS (STARTTLS)](https://www.rfc-editor.org/rfc/rfc3207)
[5] [RFC 8461, SMTP MTA Strict Transport Security (MTA-STS)](https://www.rfc-editor.org/rfc/rfc8461)
[6] [RFC 3464, An Extensible Message Format for Delivery Status Notifications (DSN bounces)](https://www.rfc-editor.org/rfc/rfc3464)
[7] [RFC 5965, An Extensible Format for Email Feedback Reports (ARF)](https://www.rfc-editor.org/rfc/rfc5965)
[8] [Apple, sending notification requests to APNs (HTTP/2, JWT auth, request headers)](https://developer.apple.com/documentation/usernotifications/sending-notification-requests-to-apns)
[9] [Apple, handling notification responses from APNs (410 Unregistered, token status)](https://developer.apple.com/documentation/usernotifications/handling-notification-responses-from-apns)
[10] [Firebase, FCM HTTP v1 API and migration from the legacy API (OAuth 2.0 bearer)](https://firebase.google.com/docs/cloud-messaging/migrate-v1)
[11] [SMPP v3.4 specification (bind types and submit_sm/deliver_sm/DLR)](https://smpp.org/SMPP_v3_4_Issue1_2.pdf)
[12] [Twilio, SMS delivery receipts and message status callbacks](https://www.twilio.com/docs/messaging/guides/track-outbound-message-status)
