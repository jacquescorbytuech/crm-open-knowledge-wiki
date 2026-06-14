---
type: Playbook
title: Orchestration and Frequency
description: How to coordinate messages across channels under a single contact strategy, choose the right channel for each job, and cap frequency so the programme does not fatigue the audience.
tags: [orchestration, frequency, contact-strategy, channels, cross-channel]
timestamp: 2026-06-14T00:00:00Z
---

# What it is

Orchestration is the layer that decides, for a given customer at a given moment, which message goes out, on which channel, and whether it goes out at all. It is what stops a multi channel programme from becoming several single channel programmes that happen to share an audience and collide in the customer's day.

# One contact strategy, not many

The unit of fatigue is the customer, not the channel. A customer who got an email, a push, and an SMS in an afternoon experienced one over contacted relationship, not three well run channels. A contact strategy sets the total acceptable contact across all channels, with priority rules for what wins when several messages are eligible at once. The channel teams optimise inside that budget; they do not each spend it in full.

# Choosing the channel for the job

Match the channel to what the message needs, using the [channels](/channels/) profiles.

* Time critical and must arrive intact: [SMS](/channels/sms-and-rcs.md) or [push](/channels/push.md).
* Reaching a dormant user: [push](/channels/push.md) for apps, [email](/channels/email.md) otherwise.
* Rich, mid funnel, or educational: [email](/channels/email.md).
* Acting on a live session: [in-app](/channels/in-app.md).
* High value retention worth the cost: [direct mail](/channels/direct-mail.md).

Default to the cheapest channel that does the job, and reserve the interruptive, expensive ones for what only they can do.

# Frequency capping

A frequency cap is a hard ceiling on messages per channel and in total over a rolling window, applied before send. Caps protect the two things over mailing destroys: deliverability, because complaint and disengagement signals drive placement, and the long run value of the list, because a fatigued subscriber unsubscribes once and is gone. Too many messages is consistently the single most common reason people unsubscribe, so frequency is not a minor dial. Set caps by segment, since your most engaged and your least engaged tolerate very different volumes. See [respect the subscriber](/principles/respect-the-subscriber.md) and [segmentation has costs](/principles/segmentation-has-costs.md).

# Suppression and quiet hours

Orchestration also decides who should not be messaged: recent purchasers, the support backlog, the unsubscribed and suppressed, and anyone inside a channel's legal quiet hours. SMS quiet hours in particular are a legal constraint, not a courtesy. See [consent and preferences](/foundations/consent-and-preferences.md).

# Related

* [Lifecycle mapping](/foundations/lifecycle-mapping.md)
* [Automation and sequences](/foundations/automation-and-sequences.md)
* [Campaign planning and calendar](/foundations/campaign-planning-and-calendar.md)
* [The channel mix](/channels/index.md)
* [Consent and preferences](/foundations/consent-and-preferences.md)

# Citations

[1] [MarketingSherpa, why consumers unsubscribe (too many emails is the top reason)](https://marketingsherpa.com/article/chart/why-consumers-unsubscribe)
[2] [FCC, telemarketing and robocall rules (SMS quiet hours)](https://www.fcc.gov/general/telemarketing-and-robocall-rules)
