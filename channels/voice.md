---
type: Channel
title: Voice
description: How to use outbound and inbound phone calls, including AI voice agents, within the TCPA consent rules, where they fit, and how to measure them against a holdout.
tags: [channel, voice, outbound-calls, ai-voice-agents, ivr, tcpa, robocall, consent, stir-shaken]
timestamp: 2026-06-14T00:00:00Z
---

## What it is

Voice is the phone call as a CRM touch: a live agent, an automated IVR, or, increasingly, an AI voice agent that holds a natural spoken conversation. Its distinctive value is bandwidth and persuasion, it is the richest, most personal channel and the only one that can resolve a complex issue or close a sale in a single synchronous exchange. The cost per touch and the legal exposure are the highest in the mix, which is why it is reserved for the few moments that earn a conversation.

## Permission and reach

The most heavily regulated channel in the bundle. In the US the TCPA governs marketing calls: a call using an artificial or prerecorded voice, or an autodialler, to a consumer needs prior express written consent, on top of national and internal Do-Not-Call compliance, caller identification, and immediate opt-out. Reach is any number you hold with the required consent, but the consent bar, not the number, is the binding constraint. This is operational guidance, not legal advice; see [legislation and compliance](/references/legislation-and-compliance.md).

## AI voice agents and the consent line

The channel's frontier is the AI voice agent: software that converses in a synthetic or cloned voice and can scale a persuasive call across a whole list. Treat it as fully in scope rather than a loophole.

> [!danger] An AI voice agent calling cold is an illegal robocall
> In February 2024 the FCC ruled that an AI-generated voice is an "artificial or prerecorded voice" under the TCPA, so an outbound marketing call placed with an AI voice is a robocall and needs prior express written consent. The new capability does not change the permission: an AI agent calling cold is an illegal robocall, exactly as a recorded message would be.

The legitimate uses are inbound (the customer called you) and outbound to consumers who gave written consent, where the agent handles reminders, renewals, qualification, or support, and discloses that it is automated. The economics invert the old limit, voice was always capped by human agent time, which AI removes, which is precisely why the consent and disclosure discipline matters more here, not less. See [consent and preferences](/foundations/consent-and-preferences.md).

## Filtering and editing

Carrier-level call labelling and blocking now sit between you and the answer. STIR/SHAKEN signs the calling number, and a number that draws complaints gets a "spam likely" label and stops being answered, the voice analogue of a sender-reputation collapse. Answer rate is the metric that decides everything else, and it degrades with the same irrelevance that sinks every other channel.

## Technical specifics

The controls are mostly legal and reputational rather than payload-shaped.

* **Consent and Do-Not-Call.** Prior express written consent for marketing robocalls; scrub against the national and your internal DNC lists; honour opt-out immediately and permanently.
* **Caller ID and attestation.** STIR/SHAKEN cryptographically signs the originating number; unattested or spoofed numbers are blocked or labelled, so use registered, attested numbers.
* **Disclosure and identification.** Identify the caller and the business at the start of the call, and for automated or AI-voiced calls, disclose that the call is automated.
* **Calling-time restrictions.** Observe the permitted calling window and quiet hours for the recipient's locale.

## Best-fit jobs

High-value, complex, or time-sensitive moments that justify a synchronous call and its cost: high-value winback, renewals and onboarding for premium accounts, inbound sales and support, appointment and booking confirmation, and collections. The worst job is low-value mass promotion, which is uneconomic with human agents and, with an AI voice, the fastest route to a spam label and a TCPA complaint.

## Voice versus the messaging channels

Voice is synchronous, persuasive, and expensive, and it carries the heaviest legal load, so reserve it for the moment that genuinely needs a conversation. Anything that can be a message should be one, an [SMS](/channels/sms-and-rcs.md), a [conversational](/channels/conversational-messaging.md) thread, or an [email](/channels/email.md); the call is for what a message cannot resolve, a negotiation, a complex support case, a high-value save. Run it under the same contact strategy so a call does not land on top of three other touches; see [orchestration and frequency](/foundations/orchestration-and-frequency.md).

## Constraints

Highest cost per touch and highest legal exposure of any channel. Carrier labelling can erase reach regardless of consent. The consent bar is strict and AI does not lower it, it raises the disclosure burden. The channel scales with cost when staffed by humans and with regulatory risk when automated, so there is no free lever for volume.

## Measurement

Read it like the other channels: distrust the dashboard and measure the downstream action against a randomised holdout. Hold back an eligible, consented slice, call the rest, and measure the difference in the action you wanted, renewal, payment, retention, not the connect. Watch answer rate, complaint rate, and spam-labelling as guardrails, since a rising complaint rate caps future reach. AI-agent calls add transcript-level signal, but the channel's lift is still incremental conversion against the held-out group. See [holdouts and control groups](/measurement/holdouts-and-control-groups.md).

## Lifecycle role

The high-touch, high-value channel, for the few moments worth a live conversation, sitting above the messaging channels in both cost and persuasive power. Most programmes reach for it at the high-value winback and renewal moments and leave the rest to messaging.

## Related

* [SMS and RCS](/channels/sms-and-rcs.md)
* [Conversational messaging](/channels/conversational-messaging.md)
* [Consent and preferences](/foundations/consent-and-preferences.md)
* [Legislation and compliance](/references/legislation-and-compliance.md)
* [Orchestration and frequency](/foundations/orchestration-and-frequency.md)
* [Holdouts and control groups](/measurement/holdouts-and-control-groups.md)

## Citations

[1] [FCC, AI-generated voices in robocalls are illegal (Declaratory Ruling, February 2024)](https://www.fcc.gov/document/fcc-makes-ai-generated-voices-robocalls-illegal)
[2] [FCC, Declaratory Ruling FCC 24-17 (full text)](https://docs.fcc.gov/public/attachments/FCC-24-17A1.pdf)
[3] [FCC, telemarketing and robocall rules](https://www.fcc.gov/general/telemarketing-and-robocall-rules)
[4] [FTC, Telemarketing Sales Rule](https://www.ftc.gov/legal-library/browse/rules/telemarketing-sales-rule)
