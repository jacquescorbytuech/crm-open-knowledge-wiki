---
type: Channel
title: Voice
description: How to use outbound and inbound phone calls, including AI voice agents, within the consent rules that govern automated marketing calls, where they fit, and how to measure them against a holdout.
tags: [channel, voice, outbound-calls, ai-voice-agents, ivr, tcpa, robocall, consent, stir-shaken]
generated:
  by: human:jacquescorbytuech
  at: 2026-08-20T00:00:00Z
sources:
  - id: fcc-ai-generated-voices-in-robocalls-are
    resource: https://www.fcc.gov/document/fcc-makes-ai-generated-voices-robocalls-illegal
    title: "FCC, AI-generated voices in robocalls are illegal (Declaratory Ruling, February 2024)"
  - id: fcc-declaratory-ruling-fcc-24-17-full
    resource: https://docs.fcc.gov/public/attachments/FCC-24-17A1.pdf
    title: "FCC, Declaratory Ruling FCC 24-17 (full text)"
  - id: fcc-telemarketing-and-robocall-rules
    resource: https://www.fcc.gov/general/telemarketing-and-robocall-rules
    title: "FCC, telemarketing and robocall rules"
  - id: ftc-telemarketing-sales-rule
    resource: https://www.ftc.gov/legal-library/browse/rules/telemarketing-sales-rule
    title: "FTC, Telemarketing Sales Rule"
---

## What it is

Voice is the phone call as a CRM touch: a live agent, an automated IVR, or, increasingly, an AI voice agent that holds a natural spoken conversation. Its distinctive value is bandwidth and persuasion: the richest, most personal channel in the mix, and the only one that can resolve a complex issue or close a sale in a single synchronous exchange. The cost per touch and the legal exposure are the highest in the mix, which is why it is reserved for the few moments that earn a conversation.

## Permission and reach

The most heavily regulated channel in the bundle. In the US the TCPA governs marketing calls: a call using an artificial or prerecorded voice, or an autodialler, to a consumer needs prior express written consent, in addition to national and internal Do-Not-Call compliance, caller identification, and immediate opt-out. Reach is any number you hold with the required consent, but the consent bar, not the number, is the binding constraint. Other regimes set their own bar: UK PECR requires specific prior consent for automated marketing calls; Australia requires telemarketers to screen their lists against the Do Not Call Register. This is operational guidance, not legal advice; see [legislation and compliance](/references/legislation-and-compliance.md).

## AI voice agents and the consent line

The channel's frontier is the AI voice agent: software that converses in a synthetic or cloned voice and can scale a persuasive call across a whole list. Treat it as fully in scope rather than a loophole.

> [!danger] An AI voice agent calling cold is an illegal robocall
> In February 2024 the FCC ruled that an AI-generated voice is an "artificial or prerecorded voice" under the TCPA, which makes an outbound marketing call placed with an AI voice a robocall requiring prior express written consent. The new capability does not change the permission: an AI agent calling cold is an illegal robocall, exactly as a recorded message would be.

The legitimate uses are inbound (the customer called you) and outbound to consumers who gave written consent, where the agent handles reminders, renewals, qualification, or support, and discloses that it is automated. The economics invert the old limit. Voice was always capped by human agent time; AI removes that cap, which is why the consent and disclosure discipline matters more here. See [consent and preferences](/foundations/consent-and-preferences.md).

## Filtering and editing

Carrier-level call labelling and blocking now sit between you and the answer. Most markets run some form of caller-ID authentication to establish that the calling number is not spoofed; the US and Canada mandate STIR/SHAKEN, which cryptographically signs the originating number. A number that draws complaints gets a "spam likely" label and stops being answered, the voice analogue of a sender-reputation collapse. Answer rate is the metric that decides everything else, degrading with the same irrelevance that sinks every other channel.

## Technical specifics

The controls are mostly legal and reputational rather than payload-shaped.

* **Consent and Do-Not-Call.** Automated and prerecorded marketing calls need prior consent in most regimes; the US bar is prior express written consent. Many jurisdictions run a do-not-call register, such as the US national DNC, the UK's TPS and Australia's Do Not Call Register. Scrub against every register covering your recipients plus your internal suppressions. Honour opt-out immediately and permanently.
* **Caller ID and attestation.** Use registered numbers that pass whatever caller-ID authentication your market runs. In the US and Canada that is STIR/SHAKEN; unattested or spoofed numbers are blocked or labelled.
* **Disclosure and identification.** Identify the caller and the business at the start of the call. For an automated or AI-voiced call, also disclose that it is automated.
* **Calling-time restrictions.** Observe the permitted calling window and quiet hours for the recipient's locale.

## Best-fit jobs

High-value, complex, or time-sensitive moments that justify a synchronous call and its cost: high-value winback, renewals and onboarding for premium accounts, inbound sales and support, appointment and booking confirmation, and collections. The worst job is low-value mass promotion, which is uneconomic with human agents and, with an AI voice, the fastest route to a spam label and a regulatory complaint.

## Voice versus the messaging channels

Voice is synchronous, persuasive, expensive, and the most legally exposed channel in the mix: reserve it for the moment that genuinely needs a conversation. Anything that can be a message should be one, an [SMS](/channels/sms-and-rcs.md), a [conversational](/channels/conversational-messaging.md) thread, or an [email](/channels/email.md); the call is for what a message cannot resolve, a negotiation, a complex support case, a high-value save. Run it under the same contact strategy so a call does not land on top of three other touches; see [orchestration and frequency](/foundations/orchestration-and-frequency.md).

## Constraints

Highest cost per touch and highest legal exposure of any channel. Carrier labelling can erase reach regardless of consent. The consent bar is strict. Automating the call adds a disclosure burden on top of it. Because the channel scales with cost when staffed by humans and with regulatory risk when automated, there is no free lever for volume.

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
