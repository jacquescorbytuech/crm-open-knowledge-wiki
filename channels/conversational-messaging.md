---
type: Channel
title: Conversational messaging
description: How to run CRM over WhatsApp and the messaging apps, work the opt-in and the 24-hour customer-service window, choose template categories, and measure it against a holdout.
tags: [channel, conversational-messaging, whatsapp, messenger, apple-messages-for-business, instagram-dm, opt-in, message-templates, customer-service-window]
timestamp: 2026-06-14T00:00:00Z
---

## What it is

Conversational messaging is CRM run over the consumer messaging apps the customer already uses with friends and family: WhatsApp above all, plus Facebook Messenger, Instagram DM, and Apple Messages for Business. Its distinctive value is a rich, two-way thread inside a trusted app, with media, buttons, read receipts, and a verified business profile. It is separate from [SMS and RCS](/channels/sms-and-rcs.md): those ride the carriers, these are over-the-top app channels governed by the platform's own policy. WhatsApp is the giant, the default messaging channel across much of Europe, Latin America, Africa, and Asia, and marginal in North America where SMS still holds.

## Permission and reach

The opt-in bar is set by the platform and sits above the law. WhatsApp requires you to obtain and record opt-in through any channel before you message a user, naming your business and making clear they will receive WhatsApp messages from you. Reach is per platform and per phone number or handle, and the thread lives in Meta's or Apple's graph, so there is no portable list you can carry elsewhere. The compensation for the high bar is quality: an opted-in conversational contact is a high-intent, high-engagement grant, not a cold address.

## Filtering and editing

Little algorithmic rewriting of an individual message once it is delivered, but the platform polices hard at the policy layer instead. Templates are pre-approved and classified by category, and each sending number carries a quality rating that throttles or blocks it when users block or report. The editor here is policy and the quality rating, not an on-device summariser, and it limits volume rather than wording.

## Technical specifics

The mechanics revolve around one window and a set of message categories.

* **The customer-service window.** When a user messages you, a 24-hour timer opens during which you can send free-form (session) messages of any type. Outside that window you may only send pre-approved template messages. This window is the core mechanic that separates reactive service from proactive outreach.
* **Template categories and pricing.** Templates are classified marketing, utility, or authentication, and you are billed by the category of the template you send. Marketing is the promotional lane and needs approval; utility follows up a user action (order, delivery, alert); authentication carries one-time passcodes. The category you choose is both a compliance and a cost decision.
* **Rich payloads.** Media, quick-reply and call-to-action buttons, list pickers, and location, well past SMS, so a message can carry an interaction rather than only text.
* **Quality rating and messaging limits.** Each number sits in a messaging-limit tier and carries a quality rating; blocks and reports lower it and cap how many users you can reach, so relevance directly governs reach.

## Best-fit jobs

Two-way, high-intent lifecycle moments: order and delivery updates, appointment reminders, authentication codes, post-purchase support, and conversational reactivation, plus opted-in promotional sends where the relationship clearly supports them. The channel shines wherever a reply is expected and the thread persists. Its worst job is cold broadcast promotion, which burns the quality rating and the opt-in that make the channel worth holding.

## Conversational messaging versus SMS versus email

Pick by reach, richness, and where the customer lives. [SMS](/channels/sms-and-rcs.md) is the lowest-common-denominator carrier channel, universal and needing no app, but one-way and plain; conversational messaging needs the app and the opt-in but returns a rich, two-way, identity-bearing thread and, in many markets, lower cost at scale. Use SMS for universal, urgent, one-way reach; conversational for rich, relationship-heavy, two-way exchanges, especially where WhatsApp is the default app. Use [email](/channels/email.md) for anything long or non-urgent. Run all three under one contact strategy; see [orchestration and frequency](/foundations/orchestration-and-frequency.md).

## Constraints

Platform dependency is total: Meta and Apple set the policy, the pricing, and the quality rules, and can throttle or suspend a number with no appeal you control. Reach skews hard by market, so the channel is central in much of the world and peripheral in the US for now. Opt-in capture and template approval add friction before the first proactive send, and the list is not portable. A quality-rating drop cuts future reach, so the channel punishes irrelevance structurally.

## Measurement

Read it against a holdout like the rest. Delivered and read receipts are richer signal than email gives, but they still measure the platform, not incremental behaviour, so hold back an eligible slice and measure the downstream action against it. Watch the quality rating, block rate, and report rate as guardrails, since they cap future reach as directly as a deliverability collapse caps email. See [holdouts and control groups](/measurement/holdouts-and-control-groups.md).

## Lifecycle role

The two-way, high-intent relationship channel, strongest in transactional and post-purchase moments and in WhatsApp-first markets, where it can carry much of what email and SMS do elsewhere. It sits alongside SMS and email under one contact strategy rather than replacing them.

## Related

* [SMS and RCS](/channels/sms-and-rcs.md)
* [Email](/channels/email.md)
* [Push](/channels/push.md)
* [Consent and preferences](/foundations/consent-and-preferences.md)
* [Orchestration and frequency](/foundations/orchestration-and-frequency.md)
* [Holdouts and control groups](/measurement/holdouts-and-control-groups.md)

## Citations

[1] [Meta, get opt-in for WhatsApp](https://developers.facebook.com/documentation/business-messaging/whatsapp/getting-opt-in)
[2] [Meta, WhatsApp Business Platform pricing and conversation categories](https://developers.facebook.com/docs/whatsapp/pricing)
[3] [Meta, WhatsApp customer-service window and message types](https://developers.facebook.com/documentation/business-messaging/whatsapp/messages/send-messages)
[4] [Meta, Messenger Platform documentation](https://developers.facebook.com/docs/messenger-platform/)
