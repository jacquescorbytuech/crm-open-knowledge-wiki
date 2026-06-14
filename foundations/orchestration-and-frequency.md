---
type: Playbook
title: Orchestration and Frequency
description: How to run a single contact strategy across channels, choose the channel for each job, set and tune engagement-tiered frequency caps, resolve message collisions by priority, and run a suppression check before every send.
tags: [orchestration, frequency, contact-strategy, channels, cross-channel, suppression, frequency-cap]
timestamp: 2026-06-14T00:00:00Z
---

# What it is

Orchestration is the layer that decides, for a given customer at a given moment, which message goes out, on which channel, and whether it goes out at all. It is what stops a multi channel programme from becoming several single channel programmes that happen to share an audience and collide in the customer's day.

# One contact strategy, not many

> [!note] The unit of fatigue is the customer, not the channel
> A customer who got an email, a push, and an SMS in an afternoon experienced one over-contacted relationship, not three well-run channels. Set one contact budget across all channels, not a per-channel quota each team fills.

The unit of fatigue is the customer, not the channel. A customer who got an email, a push, and an SMS in an afternoon experienced one over contacted relationship, not three well run channels. A contact strategy sets the total acceptable contact across all channels, with priority rules for what wins when several messages are eligible at once. The channel teams optimise inside that budget; they do not each spend it in full. Paid media counts too: a customer chased by a retargeting ad the day after they bought is the contact strategy leaking into the channel it most often forgets, which is why [audience sync](/foundations/audience-sync.md) brings paid under the same governance and suppression rules.

# Spending the single contact budget

Make the shared budget operational by treating a user's attention as a fixed weekly allowance that all channels draw from the same pool, not a per channel quota each team fills.

1. Set a total contact budget per engagement tier (the caps in the next section), counted across every channel together.
2. When a message becomes eligible, pick the channel by the job it needs to do (see below), not by which team owns it.
3. Charge the send against the shared budget. When the budget is spent for the window, further non transactional messages wait or drop by priority, whichever channel they came from.
4. Prefer one well chosen send over the same message duplicated across channels. Reserve a second channel for genuine fallback, for example email did not open within N hours so a push follows, not for simultaneous blasts.

The decision is which single channel carries this message, then whether the user can afford it this window. Two channels firing the same content in an afternoon is the budget being double spent.

# Choosing the channel for the job

Match the channel to what the message needs, using the [channels](/channels/) profiles.

* Time critical and must arrive intact: [SMS](/channels/sms-and-rcs.md) or [push](/channels/push.md).
* Reaching a dormant user: [push](/channels/push.md) for apps, [email](/channels/email.md) otherwise.
* Rich, mid funnel, or educational: [email](/channels/email.md).
* Acting on a live session: [in-app](/channels/in-app.md).
* High value retention worth the cost: [direct mail](/channels/direct-mail.md).

Default to the cheapest channel that does the job, and reserve the interruptive, expensive ones for what only they can do.

# Why capping matters

A frequency cap is a hard ceiling on messages per channel and in total over a rolling window, applied before send. Caps protect the two things over mailing destroys: deliverability, because complaint and disengagement signals drive placement, so a fatigued list quietly slides toward the spam folder, and the long run value of the list, because a fatigued subscriber unsubscribes once and is gone. Too many messages is consistently the single most common reason people unsubscribe, so frequency is not a minor dial. See [respect the subscriber](/principles/respect-the-subscriber.md) and [segmentation has costs](/principles/segmentation-has-costs.md).

# Engagement-tiered starting caps

An **engagement tier** is a band a user falls into based on how recently and how often they engage — the [engagement score](/foundations/lifecycle-mapping.md) from the lifecycle map, cut into a few groups. Most programmes use three: recently active (opened, clicked, or purchased inside a short window), moderately engaged (active only in a longer window), and dormant (no engagement across the sunset window). Set the window boundaries from your own engagement distribution and keep them consistent with the sunset logic in [segmentation and data](/foundations/segmentation-and-data.md); the tier is derived from observed behaviour and recomputed as it moves, not assigned once.

Set caps by segment, since your most engaged and your least engaged tolerate very different volumes. The figures below are starting defaults to tune against your own complaint and unsubscribe signals, not universal facts; the right cap for any programme is whatever maximises incremental value before fatigue costs overtake it. Begin here, then tune.

| Engagement tier | Email starting cap | Push / SMS starting cap |
| --- | --- | --- |
| Highly engaged (opened/clicked recently) | up to ~4-5 / week | up to ~3-4 / week |
| Moderately engaged | ~2-3 / week | ~1-2 / week |
| Low engagement / dormant | ~1 / week or fewer | rare, reactivation only |

Apply the lowest cap a user qualifies for, and treat SMS as scarcer than email at every tier because it is interruptive and costed per send.

# How to tune caps

Caps are a setting you converge on, not a number you guess once.

1. Start from the tiered defaults above and instrument complaint rate, unsubscribe rate, and a fatigue proxy such as falling open or click rate per additional send.
2. Widen first. Raise the cap for one tier on a random slice and watch whether incremental value keeps rising or whether complaints and unsubscribes climb faster than revenue. Most programmes find a point where another send adds sends but not value.
3. Then narrow. Pull the cap back where the fatigue signals turned, and confirm that revenue holds while complaints fall.
4. Validate against a holdout, not against gross sends. Run the candidate cap as a treatment versus the current cap on a randomised control so you read the incremental effect, not the headline send count. See [holdouts and control groups](/measurement/holdouts-and-control-groups.md).
5. Re-tier on behaviour, not once. As users move between engagement tiers their cap moves with them.

A cap that lifts gross opens but loses incremental revenue or raises complaints is a worse cap, however good the top line looks.

# Resolving collisions by priority

When several messages are eligible for the same user in the same window and the budget will not cover all of them, a fixed priority order decides what sends and what waits or drops. Higher priority wins; the rest queue or are suppressed for the window.

1. [Transactional and service](/foundations/transactional-messaging.md) (receipts, password resets, shipping, fraud alerts). Always sends, never capped, never suppressed for frequency.
2. Triggered and lifecycle (cart abandon, onboarding step, winback, renewal). Sends if the budget allows, by recency and value.
3. Broadcast and promotional (newsletters, campaigns, sales). Lowest priority, the first to yield when the budget is tight.

Within a tier, break ties by business value and by recency of the triggering event. The rule keeps a promotional blast from crowding out a renewal nudge, and keeps anything from crowding out a receipt.

# Suppression check before every send

Run this list as a final check before any send fires. A message that clears every job, channel, and cap decision above must still pass suppression, because suppression is where legal and deliverability constraints live.

* Hard bounces: address or number is dead, never send again.
* Unsubscribes: global opt out, suppress on every channel.
* Spam complaints: treat as a hard opt out, suppress and do not reactivate.
* Channel-specific opt-outs: opted out of SMS but not email means email only.
* Quiet hours: do not send inside the channel's permitted window. US SMS quiet hours are commonly observed as 8am to 9pm in the recipient's local time under TCPA practice.
* Frequency-capped: user has hit their cap for this window, defer or drop by priority.
* Recent contact and exclusions: recent purchasers, open support tickets, and any campaign exclusion list.

Quiet hours and consent based suppressions are legal constraints, not courtesies. See [consent and preferences](/foundations/consent-and-preferences.md).

# Related

* [Lifecycle mapping](/foundations/lifecycle-mapping.md)
* [Automation and sequences](/foundations/automation-and-sequences.md)
* [Campaign planning and calendar](/foundations/campaign-planning-and-calendar.md)
* [The channel mix](/channels/index.md)
* [Audience sync](/foundations/audience-sync.md)
* [Transactional messaging](/foundations/transactional-messaging.md)
* [Consent and preferences](/foundations/consent-and-preferences.md)
* [Holdouts and control groups](/measurement/holdouts-and-control-groups.md)

# Citations

[1] [MarketingSherpa, why consumers unsubscribe (too many emails is the top reason)](https://marketingsherpa.com/article/chart/why-consumers-unsubscribe)
[2] [FCC, telemarketing and robocall rules (SMS quiet hours)](https://www.fcc.gov/general/telemarketing-and-robocall-rules)
