---
type: Channel
title: SMS and RCS
description: How to run SMS and RCS as a premium sparing channel, controlling encoding and segment cost, choosing a sending route, enforcing consent, and measuring against a holdout.
tags: [channel, sms, rcs, consent, transactional, carrier, encoding, 10dlc, sender-id]
timestamp: 2026-06-14T00:00:00Z
---

## What it is

SMS delivers a short text message to a phone number, read almost immediately and almost always. RCS is its richer successor on Android, adding branding, images, suggested replies, and read receipts, rolling out through Google Messages. Together they are the most interruptive lifecycle channel and, today, the one with the least editing between sender and recipient.

## Permission and reach

Permission is an explicit opt in tied to a phone number, and the consent bar is high: TCPA in the United States, PECR in the United Kingdom, and equivalents elsewhere, with quiet hours, clear identification, and easy STOP handling expected. In the United States, application to person traffic runs over registered 10DLC numbers or short codes with carrier vetting. The number is the asset, and you cannot take a carrier relationship elsewhere the way you can an email list.

## Filtering and editing

Less than email or push, but not zero. Carriers run their own spam filtering and can block traffic, and RCS on Google Messages is gaining auto-categorisation similar in spirit to the Gmail Promotions tab. SMS is the least-edited high-volume channel today, but that is a current state, not a guarantee. See [the channel mix](/channels/index.md).

## Message length and encoding

SMS length is a hard technical limit, and exceeding it costs you. A single segment holds 160 characters in GSM-7 encoding, or just 70 in UCS-2/Unicode. Longer messages are split and reassembled, which reserves header space and drops the per-segment count to 153 (GSM-7) or 67 (UCS-2). You are billed per segment, so an unwatched character can quietly multiply the cost of a campaign.

Treat length discipline here as a budget control, not a style preference. One out-of-range character flips the encoding and roughly halves the characters per segment, so a single character can double the per-message bill across the whole send.

> [!warning] One stray character can flip the encoding
> This is where the budget halves in practice. GSM-7 covers the basic Latin alphabet, digits, and a short set of punctuation. The moment one character falls outside it, the whole message flips to UCS-2 and the budget halves, from 160 to 70. The usual culprits are invisible: a single emoji, or a curly quote and em dash auto-inserted by a word processor, or an accented letter, or a non-breaking space pasted from a web page. One smart quote in a 158-character draft turns a one-segment send into a three-segment send.

To keep within one segment:

* Compose in a plain-text editor, not Word or a CMS that smartens punctuation. Paste straight quotes, hyphens, and standard spaces.
* Strip emoji from bulk marketing copy. If brand voice needs one, count the message at the 70-character UCS-2 budget and design to it deliberately.
* Preview the actual encoding and segment count in your ESP before send. Most show GSM-7 vs UCS-2 and the live segment tally as you type.
* Treat the link as part of the budget. A long tracked URL alone can push a tight message over 160.

## Choosing a sending route

In the US, application-to-person (A2P) traffic runs over one of three route types, and the choice is driven by volume, throughput, and how fast you need to launch, not by message content.

* **A2P 10DLC.** Standard 10-digit long codes for application traffic. Requires brand and campaign registration with the carriers (you declare the brand, the use case, and your opt-in, opt-out, and HELP flows) before any traffic flows. Registration is mandatory and takes time, days to weeks depending on vetting and special use cases, so it is not a same-day launch. Throughput scales with an assigned trust score; unregistered or high-volume long-code traffic is filtered. Lowest cost route and the default for most lifecycle programmes once registered.
* **Short codes.** 5-7 digit numbers engineered for high throughput, built for high-volume and time-sensitive programmes. Highest cost and the slowest to provision (carrier approval and lease), but the fastest and most reliable to deliver at scale once live.
* **Toll-free.** A middle option with its own verification process, lighter than short-code provisioning and offering more throughput than an unregistered long code. Suitable for moderate volume and a quicker start than a short code.

Relative cost runs short code above toll-free and 10DLC, and segments multiply whatever the per-message rate is. Pick by the constraint that matters first: low volume and cost-sensitive, register 10DLC and wait out the registration; high sustained volume or burst sends where deliverability cannot wobble, lease a short code; somewhere between, or you need to start sooner than 10DLC vetting allows, take toll-free.

## How the message reaches the carrier

You do not connect to mobile networks directly. An aggregator (the messaging side of a CPaaS) holds the carrier interconnects and routes your traffic, and you reach it either through an HTTP REST API or through SMPP, the binary telecom protocol the REST APIs sit on top of. A message you send is mobile-terminated (MT); a reply, including a `STOP` or `HELP` keyword, comes back mobile-originated (MO). Delivery confirmation arrives as a delivery receipt (DLR) relayed back from the carrier, but treat it as advisory: carriers differ in whether and when they return one, some mark "delivered" on network handoff rather than handset receipt, and a missing DLR does not reliably mean a missing message. The registration regimes above are the carrier's admission control sitting in front of that route. The transport, the SMPP bind types, and the webhook path that carries DLRs back are in [sending infrastructure](/foundations/sending-infrastructure.md).

## Branded sender IDs and verification

Outside the US, a large share of A2P traffic uses an alphanumeric sender ID: a short text label, usually the brand name, shown in place of a phone number at the top of the message. It gives the message an identity but carries no reply path, so it suits one-way alerts and notifications rather than two-way exchanges. It is also trivial to spoof, since nothing in the protocol stops a sender from setting whatever label it likes, which is why scam texts so often arrive under a bank or government name.

Markets are closing that gap with sender ID registers that bind the label to the organisation entitled to use it. Australia's SMS Sender ID Register, run by the ACMA as part of its anti-scam programme, is the furthest along. Registration through a participating telco or message provider opened on 30 November 2025, and registration becomes mandatory from 1 July 2026. A registered sender ID must be clearly tied to the organisation, such as a matching business name or trademark, and an Australian business registers against the contact details held in the Australian Business Register, which must be current. The mechanism mirrors US 10DLC: a registration regime that gates whether your branded identity reaches the handset, with the unregistered case degraded rather than blocked outright.

> [!warning] An unregistered brand label is shown as `Unverified`
> From 1 July 2026, an SMS sent under an unregistered Australian sender ID has its brand name replaced with `Unverified` and is grouped into a single thread alongside other unregistered senders, including suspected scams. Legitimate traffic then lands next to the spam, stripped of the identity the label was meant to carry.

Treat this as the SMS counterpart of email authentication. An unverified sender label does to a text roughly what a failed `DMARC` check does to an email: the message may survive, but it arrives without its trust markers and in worse company. Where a register operates in a market you send to, register every sender ID you use before its deadline and keep the underlying business-register record current, or your own brand traffic falls into the unverified bucket. See [authentication](/foundations/authentication.md).

## Compliance in practice

The consent bar is the operational core of the channel, not a footnote.

* **Capture explicit opt-in and log it.** Consent must be an affirmative act tied to the number: a ticked unticked box, a keyword reply, a double opt-in confirmation. Log what they agreed to, when, the exact disclosure text shown, and the source. The record is your defence in a TCPA or PECR challenge, and you cannot reconstruct it later.
* **Handle STOP and HELP.** STOP (and its variants) must unsubscribe the number immediately and send one confirmation; HELP must return sender identity and contact. These are mandatory and carrier-enforced. Most platforms process them automatically, but confirm yours does and that suppression propagates across every campaign on the number, not just the one that triggered it.
* **Enforce quiet hours by recipient local time.** The federal TCPA baseline confines marketing sends to roughly 8am to 9pm in the recipient's local time zone, but treat that as the floor, not the rule: several state mini-TCPA laws (Florida, Oklahoma, Texas, and Connecticut among them) impose tighter windows and weekend or holiday limits, and obligations follow the recipient's location. Apply 8am to 9pm local as the baseline and the strictest applicable state window on top. Schedule against the recipient's zone, not the server's or the brand's, which means you need a reliable zone for each number and a queue that holds sends outside the window rather than dropping them.

## RCS

RCS Business Messaging adds a verified-sender check mark, brand logo and colour, rich cards with media, suggested replies, and read receipts, delivered through Google Messages on Android. Apple added RCS to iPhone Messages from iOS 18 on carriers that support it, bringing read receipts, typing indicators, and high-resolution media to cross-platform threads. It is richer than SMS but still carrier-mediated, and its reach depends on device, carrier, and client support.

Use the rich features for what plain SMS cannot do: the verified sender and brand identity to cut spoofing and lift trust, suggested replies and suggested actions to make the next step a single tap, and cards with media for confirmations or product moments that benefit from an image. Because reach is uneven across device, carrier, and client, design every RCS message with a graceful SMS fallback. Write the SMS version first as a self-contained message that works alone, then enrich it for RCS, so a recipient whose client does not support RCS still gets a complete, actionable text rather than a degraded fragment. Never put essential content only in a card or a suggested reply.

## Best-fit jobs

Time critical and high value messages that must not be summarised or delayed: fraud and security alerts, delivery and appointment updates, two factor codes, order confirmations, and a small number of genuinely urgent promotional moments. The message that lands intact is its advantage; do not spend it on routine marketing.

## Copy and links

Length limits and weak layout control mean the proposition must be the message, not the wrapper. The craft is to land one idea and one action inside a single segment.

* **Write to one segment.** Lead with the value or the instruction, name the sender so the message is not anonymous, and cut every word the recipient can infer. Watch the live segment count and the encoding as you draft.
* **Use branded, tracked short links, not generic shorteners.** A link on your own short domain looks legitimate, carries the tracking you need, and is far less likely to be flagged by carrier filters than a public shortener that spam traffic also uses. Make sure click attribution survives the redirect; a link the recipient does not trust does not get tapped, and a link your stack cannot measure breaks the only mid-funnel signal you have.
* **For RCS, prefer a suggested action over a raw URL** where the client supports it, and keep the SMS fallback link intact for everyone else. A scannable QR is for cross-channel print and screen, not for a message read on the same phone.

See [copywriting](/foundations/copywriting.md).

## Constraints

Among the more expensive digital channels per message, well above email and push (though far below direct mail), and the lowest tolerance for volume: a single unwanted text reads as more intrusive than an unwanted email and drives opt outs fast. Segments multiply the cost, so length discipline is a budget control, not just a craft preference.

## Measurement

Opens do not exist on this channel, so measurement reads delivery and downstream conversion, not engagement proxies. Delivery receipts are more reliable than push and confirm the message landed; clicks on a tracked link plus the conversion behind it carry the outcome signal. Because the cost and the intrusion are both high, read that conversion against a randomised holdout rather than crediting every conversion behind a send: hold back a control, compare treated against control, and bank only the incremental lift. See [holdouts and control groups](/measurement/holdouts-and-control-groups.md). Opt out rate and per message cost are the discipline metrics, since SMS is the channel where frequency mistakes are most directly expensive.

## Lifecycle role

The premium, sparing channel for moments that justify the cost and the interruption. Pair it with email and in app rather than treating it as a second email list.

## Related

* [Push](/channels/push.md)
* [Voice](/channels/voice.md)
* [Sending infrastructure](/foundations/sending-infrastructure.md)
* [Orchestration and frequency](/foundations/orchestration-and-frequency.md)
* [Consent and preferences](/foundations/consent-and-preferences.md)
* [Legislation and compliance](/references/legislation-and-compliance.md)
* [Holdouts and control groups](/measurement/holdouts-and-control-groups.md)
* [Copywriting](/foundations/copywriting.md)

## Citations

[1] [FCC, telemarketing and robocall rules (TCPA consent, STOP, quiet hours)](https://www.fcc.gov/general/telemarketing-and-robocall-rules)
[2] [Twilio, SMS character limits and segmentation (160/70, 153/67)](https://www.twilio.com/docs/glossary/what-sms-character-limit)
[3] [Twilio, A2P 10DLC registration](https://www.twilio.com/docs/messaging/compliance/a2p-10dlc)
[4] [Google, RCS Business Messaging best practices](https://developers.google.com/business-communications/rcs-business-messaging/guides/learn/best-practices)
[5] [Apple, turn on RCS messaging on iPhone (iOS 18)](https://support.apple.com/en-us/122195)
[6] [Kelley Drye, state mini-TCPA laws and quiet-hours rules for marketing texts](https://www.kelleydrye.com/viewpoints/blogs/ad-law-access/texas-mini-tcpa-law-faqs-for-marketing-texts)
[7] [ACMA, SMS Sender ID Register](https://www.acma.gov.au/sms-sender-id-register)
[8] [ACMA, unregistered branded SMS to be labelled 'Unverified' from 1 July 2026](https://www.acma.gov.au/articles/2026-05/unregistered-branded-sms-be-labelled-unverified-1-july-acma-warns)
