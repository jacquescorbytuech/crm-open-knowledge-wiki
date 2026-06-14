---
type: Channel
title: SMS and RCS
description: A short, interruptive, expensive per message channel with the least editing between sender and recipient today, governed by strict explicit consent.
tags: [channel, sms, rcs, consent, transactional, carrier]
timestamp: 2026-06-14T00:00:00Z
---

# What it is

SMS delivers a short text message to a phone number, read almost immediately and almost always. RCS is its richer successor on Android, adding branding, images, suggested replies, and read receipts, rolling out through Google Messages. Together they are the most interruptive lifecycle channel and, today, the one with the least editing between sender and recipient.

# Permission and reach

Permission is an explicit opt in tied to a phone number, and the consent bar is high: TCPA in the United States, PECR in the United Kingdom, and equivalents elsewhere, with quiet hours, clear identification, and easy STOP handling expected. In the United States, application to person traffic runs over registered 10DLC numbers or short codes with carrier vetting. The number is the asset, and you cannot take a carrier relationship elsewhere the way you can an email list.

# Filtering and editing

Less than email or push, but not zero. Carriers run their own spam filtering and can block traffic, and RCS on Google Messages is gaining auto-categorisation similar in spirit to the Gmail Promotions tab. SMS is the least-edited high-volume channel today, but that is a current state, not a guarantee. See [the channel mix](/channels/index.md).

# Message length and encoding

SMS length is a hard technical limit, and exceeding it costs you. A single segment holds 160 characters in GSM-7 encoding, or just 70 in UCS-2/Unicode (which a single emoji or curly quote can trigger for the whole message). Longer messages are split and reassembled, which reserves header space and drops the per-segment count to 153 (GSM-7) or 67 (UCS-2). You are billed per segment, so an unwatched emoji can quietly double the cost of a campaign. Write tight, keep links short, and watch the encoding.

# Numbers and registration

The sending number type determines throughput and how it is policed.

* **A2P 10DLC.** Application-to-person traffic over standard 10-digit long codes in the US requires brand and campaign registration with carrier vetting (opt-in, opt-out, and use case declared). Throughput scales with a trust score; unregistered or high-volume long-code traffic is filtered.
* **Short codes.** 5-7 digit numbers engineered for high throughput and high-volume programmes; fastest to deliver, slowest and most expensive to provision.
* **Toll-free.** A middle option with its own verification, suitable for moderate volume.

# RCS

RCS Business Messaging adds a verified-sender check mark, brand logo and colour, rich cards with media, suggested replies, and read receipts, delivered through Google Messages on Android. Apple added RCS to iPhone Messages from iOS 18 on carriers that support it, bringing read receipts, typing indicators, and high-resolution media to cross-platform threads. It is richer than SMS but still carrier-mediated, and its reach depends on device, carrier, and client support.

# Best-fit jobs

Time critical and high value messages that must not be summarised or delayed: fraud and security alerts, delivery and appointment updates, two factor codes, order confirmations, and a small number of genuinely urgent promotional moments. The message that lands intact is its advantage; do not spend it on routine marketing.

# Constraints

Among the more expensive digital channels per message, well above email and push (though far below direct mail), and the lowest tolerance for volume: a single unwanted text reads as more intrusive than an unwanted email and drives opt outs fast. Length limits and weak layout control mean the proposition must be the message, not the wrapper. See [copywriting](/foundations/copywriting.md).

# Measurement

Delivery receipts are more reliable than push, and clicks on a tracked link plus downstream conversion carry the signal. Opt out rate and per message cost are the discipline metrics: SMS is the channel where frequency mistakes are most directly expensive.

# Lifecycle role

The premium, sparing channel for moments that justify the cost and the interruption. Pair it with email and in app rather than treating it as a second email list.

# Related

* [Push](/channels/push.md)
* [Orchestration and frequency](/foundations/orchestration-and-frequency.md)
* [Consent and preferences](/foundations/consent-and-preferences.md)
* [Legislation and compliance](/references/legislation-and-compliance.md)

# Citations

[1] [FCC, telemarketing and robocall rules (TCPA consent, STOP, quiet hours)](https://www.fcc.gov/general/telemarketing-and-robocall-rules)
[2] [Twilio, SMS character limits and segmentation (160/70, 153/67)](https://www.twilio.com/docs/glossary/what-sms-character-limit)
[3] [Twilio, A2P 10DLC registration](https://www.twilio.com/docs/messaging/compliance/a2p-10dlc)
[4] [Google, RCS Business Messaging best practices](https://developers.google.com/business-communications/rcs-business-messaging/guides/learn/best-practices)
[5] [Apple, turn on RCS messaging on iPhone (iOS 18)](https://support.apple.com/en-us/122195)
