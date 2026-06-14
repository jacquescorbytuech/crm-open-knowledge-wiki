---
type: Channel
title: Email
description: The highest volume, lowest marginal cost, and most heavily mediated lifecycle channel, addressable to a list the sender holds.
tags: [channel, email, deliverability, lifecycle]
timestamp: 2026-06-14T00:00:00Z
---

## What it is

Email is the workhorse of lifecycle marketing: a message addressed to an address on a list you hold, delivered over open federated protocols, at effectively zero marginal cost per send. It is the highest volume and lowest cost channel, and the one with the deepest tooling, the longest measurement history, and the most editing between you and the recipient.

## Permission and reach

A subscription is an address plus a consent record you hold and can take to another provider. Reach is governed by deliverability rather than by a per device permission. Authentication is the price of entry (see [authentication](/foundations/authentication.md)), and sender level engagement decides placement above it (see [engagement is the new deliverability](/principles/engagement-is-deliverability.md)). The reachable audience is the engaged subset, not the list size.

## Filtering and editing

The inbox is no longer a passive transport layer. Providers classify mail into tabs, rank it within them, and increasingly summarise it for the recipient, and the sender sees none of these decisions directly. This is the layer above the classical spam-or-inbox question; the dated platform changes that built it are catalogued in [platform interventions](/references/platform-interventions.md), and the research behind the parsing in [email intelligence research](/references/email-intelligence-research.md). For operations, the response is in [deliverability](/foundations/deliverability.md).

## Technical specifics

The format constrains the craft, and the constraints are concrete.

* **Build width.** The conventional template width is around 600 pixels, which renders reliably on desktop and scales down on mobile; wider designs clip in many desktop clients.
* **Message size.** Gmail clips a message above roughly 102KB, hiding the rest behind a "view entire message" link, which can bury your CTA and conversion tracking. Keep the HTML lean.
* **MIME.** Send a `multipart/alternative` message carrying both a plain-text and an HTML part, plainest first per the standard; a missing plain-text part is a spam signal and degrades clients that prefer it.
* **Unsubscribe headers.** Bulk senders must include a `List-Unsubscribe` header (RFC 2369) and support one-click unsubscribe via the `List-Unsubscribe-Post` header (RFC 8058), in addition to a visible in-body link.
* **Authentication.** SPF, DKIM, and aligned DMARC are the price of entry, not an optimisation. See [authentication](/foundations/authentication.md).
* **Sending infrastructure.** A new sending IP or domain needs warming, ramping volume on the most engaged subscribers first. Separate [transactional and marketing](/foundations/transactional-messaging.md) streams, ideally on distinct subdomains, so a marketing reputation problem cannot poison transactional delivery. The warming ramp, subdomain split, and recovery steps live in [deliverability](/foundations/deliverability.md).

Rendering across the client landscape, mobile, dark mode, accessibility, and alt text, is covered in [message design and rendering](/foundations/message-design-and-rendering.md).

## Best-fit jobs

Broad mid funnel work where some summary distortion is acceptable: newsletters, content and education, promotional offers to engaged subscribers, lifecycle nurture, and transactional confirmations. Editorial content tends to survive mediation better than pure promotion. Email is rarely the right channel for a genuinely time critical alert, where SMS or push lands faster and more intact.

## Constraints

Opens are corrupted by image prefetch and Mail Privacy Protection, so they are directional only and click, conversion, reply, and unsubscribe carry the signal. See [email metrics are directional](/principles/metrics-are-directional.md). The bulk sender requirements make poor list hygiene a deliverability cost, not just a waste. Image only design loses the structure the classifier reads.

List hygiene is a deliverability lever, not housekeeping. Suppress hard bounces immediately and never resend to them, retire addresses after repeated soft bounces, and sunset the never-engaging tail before it drags sender reputation down. Wire these as automated suppression rules, see [automation and sequences](/foundations/automation-and-sequences.md), run them as part of ongoing [database health](/foundations/database-health.md), and work the recovery order in [deliverability](/foundations/deliverability.md).

## Measurement

Click through, click to open, downstream conversion, reply rate, one click unsubscribe timing, and complaint rate, monitored with Postmaster Tools and SNDS. See [the deliverability metrics reference](/foundations/deliverability.md) and, where volume allows, [measuring intermediation](/measurement/measuring-intermediation.md).

## Lifecycle role

The default backbone for nurture, retention, and winback at scale, complemented rather than replaced by the other channels. Frequency and cadence are governed in [orchestration and frequency](/foundations/orchestration-and-frequency.md), which also covers how it sits in the channel mix.

## Related

* [Authentication](/foundations/authentication.md)
* [Deliverability](/foundations/deliverability.md)
* [Transactional messaging](/foundations/transactional-messaging.md)
* [Database health and sunsetting](/foundations/database-health.md)
* [Message design and rendering](/foundations/message-design-and-rendering.md)
* [Automation and sequences](/foundations/automation-and-sequences.md)
* [Orchestration and frequency](/foundations/orchestration-and-frequency.md)
* [Engagement is the new deliverability](/principles/engagement-is-deliverability.md)
* [Email metrics are directional](/principles/metrics-are-directional.md)

## Citations

[1] [Google, email sender guidelines](https://support.google.com/a/answer/81126)
[2] [Word to the Wise, deliveries and opens and clicks](https://www.wordtothewise.com/2024/06/deliveries-and-opens-and-clicks/)
[3] [Mailchimp, Gmail clips messages over ~102KB](https://mailchimp.com/help/gmail-is-clipping-my-email/)
[4] [Litmus, email development (≈600px template width)](https://www.litmus.com/blog/7-myths-of-email-development)
[5] [RFC 8058, one-click unsubscribe](https://www.rfc-editor.org/rfc/rfc8058)
[6] [RFC 2369, List-Unsubscribe header](https://www.rfc-editor.org/rfc/rfc2369)
