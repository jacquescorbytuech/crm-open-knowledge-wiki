---
type: Channel
title: Email
description: The highest volume, lowest marginal cost and most heavily mediated lifecycle channel, addressable to a list the sender holds.
tags: [channel, email, deliverability, lifecycle]
generated:
  by: human:jacquescorbytuech
  at: 2026-08-20T00:00:00Z
sources:
  - id: google-email-sender-guidelines
    resource: https://support.google.com/a/answer/81126
    title: "Google, email sender guidelines"
  - id: word-to-the-wise-deliveries-and-opens
    resource: https://www.wordtothewise.com/2024/06/deliveries-and-opens-and-clicks/
    title: "Word to the Wise, deliveries and opens and clicks"
  - id: mailchimp-gmail-clips-messages-over-102kb
    resource: https://mailchimp.com/help/gmail-is-clipping-my-email/
    title: "Mailchimp, Gmail clips messages over ~102KB"
  - id: litmus-email-development-600px-template-width
    resource: https://www.litmus.com/blog/7-myths-of-email-development
    title: "Litmus, email development (≈600px template width)"
  - id: rfc-8058-one-click-unsubscribe
    resource: https://www.rfc-editor.org/rfc/rfc8058
    title: "RFC 8058, one-click unsubscribe"
  - id: rfc-2369-list-unsubscribe-header
    resource: https://www.rfc-editor.org/rfc/rfc2369
    title: "RFC 2369, List-Unsubscribe header"
---

## What it is

Email is the core channel of lifecycle marketing: a message addressed to an address on a list you hold, delivered over open federated protocols, at effectively zero marginal cost per send. It is the highest volume and lowest cost channel, with the deepest tooling, the longest measurement history and the most editing between you and the recipient.

## Permission and reach

A subscription is an address plus a consent record you hold and can take to another provider. Reach is governed by deliverability rather than by a per device permission. Authentication is the precondition for reaching the inbox at all (see [authentication](/foundations/authentication.md)). Above that floor, sender level engagement decides placement (see [engagement is the new deliverability](/principles/engagement-is-deliverability.md)). The reachable audience is the engaged subset, not the list size.

## Filtering and editing

The inbox is no longer a passive transport layer. Providers classify mail into tabs, rank it within them and increasingly summarise it for the recipient, none of which the sender sees directly. This is the layer above the classical spam-or-inbox question. The dated platform changes that built it are catalogued in [platform interventions](/references/platform-interventions.md); the research behind the parsing is in [email intelligence research](/references/email-intelligence-research.md). For operations, the response is in [deliverability](/foundations/deliverability.md).

## Technical specifics

The format's constraints on the craft are concrete.

* **Build width.** The conventional template width is around 600 pixels, which renders reliably on desktop and scales down on mobile; wider designs clip in many desktop clients.
* **Message size.** Gmail clips a message above roughly 102KB, hiding the rest behind a "view entire message" link, which can bury your CTA and conversion tracking. Keep the HTML lean.
* **MIME.** Send a `multipart/alternative` message carrying both a plain-text and an HTML part, plainest first per the standard; a missing plain-text part is a spam signal and degrades clients that prefer it.
* **Unsubscribe headers.** Bulk senders must include a `List-Unsubscribe` header (RFC 2369) and support one-click unsubscribe via the `List-Unsubscribe-Post` header (RFC 8058), in addition to a visible in-body link.
* **Authentication.** SPF, DKIM and aligned DMARC are required before anything else about deliverability matters, not an optimisation to add later. See [authentication](/foundations/authentication.md).
* **Sending infrastructure.** Mail is relayed by Mail Transfer Agents over SMTP, which is why an ESP is at bottom a managed MTA fleet; the transport itself, the SMTP conversation, the envelope-versus-headers distinction and how bounces come back, is in [sending infrastructure](/foundations/sending-infrastructure.md). A new sending IP or domain needs warming, ramping volume on the most engaged subscribers first. Separate [transactional and marketing](/foundations/transactional-messaging.md) streams, ideally on distinct subdomains, so that a marketing reputation problem cannot affect transactional delivery. The warming ramp, subdomain split and recovery steps live in [deliverability](/foundations/deliverability.md).

Rendering across the client landscape, mobile, dark mode, accessibility and alt text, is covered in [message design and rendering](/foundations/message-design-and-rendering.md).

## Best-fit jobs

Broad mid funnel work where some summary distortion is acceptable: newsletters, content and education, promotional offers to engaged subscribers, lifecycle nurture and transactional confirmations. Editorial content tends to survive mediation better than pure promotion. Email is rarely the right channel for a genuinely time critical alert, where SMS or push lands faster and more intact.

## Constraints

Neither opens nor clicks deserve full trust: image prefetch and Mail Privacy Protection corrupt the first; security scanners inflate the second. The cleaner signals are conversion, reply and unsubscribe. See [email metrics are directional](/principles/metrics-are-directional.md). The bulk sender requirements make poor list hygiene a deliverability cost, not just a waste. Image only design loses the structure the classifier reads.

List hygiene is a deliverability lever, not housekeeping. Suppress hard bounces immediately and never resend to them; retire addresses after repeated soft bounces; sunset the never-engaging tail before it drags sender reputation down. Wire these as automated suppression rules, see [automation and sequences](/foundations/automation-and-sequences.md), run them as part of ongoing [database health](/foundations/database-health.md) and work the recovery order in [deliverability](/foundations/deliverability.md).

## Measurement

Click through, click to open, downstream conversion, reply rate, one click unsubscribe timing and complaint rate, monitored with Postmaster Tools and SNDS. See [the deliverability metrics reference](/foundations/deliverability.md) and, where volume allows, [measuring intermediation](/measurement/measuring-intermediation.md).

## Lifecycle role

The default backbone for nurture, retention and winback at scale, complemented rather than replaced by the other channels. Frequency and cadence are governed in [orchestration and frequency](/foundations/orchestration-and-frequency.md), which also covers how it sits in the channel mix.

## Related

* [Authentication](/foundations/authentication.md)
* [Deliverability](/foundations/deliverability.md)
* [Sending infrastructure](/foundations/sending-infrastructure.md)
* [Transactional messaging](/foundations/transactional-messaging.md)
* [Database health and sunsetting](/foundations/database-health.md)
* [Message design and rendering](/foundations/message-design-and-rendering.md)
* [Automation and sequences](/foundations/automation-and-sequences.md)
* [Orchestration and frequency](/foundations/orchestration-and-frequency.md)
* [Engagement is the new deliverability](/principles/engagement-is-deliverability.md)
* [Email metrics are directional](/principles/metrics-are-directional.md)
