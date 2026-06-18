---
type: Playbook
title: Automation and Sequences
description: How to build trigger-based welcome, abandoned cart, and re-engagement flows across email, SMS, and push, choosing the channel for each touch, with message-by-message cadences, sunset criteria, and a pre-launch testing checklist.
tags: [automation, welcome, abandoned-cart, re-engagement, sunset, lifecycle]
timestamp: 2026-06-14T00:00:00Z
---

## Triggers and goals

An automation fires from an event (signup, purchase, browse, inactivity) rather than a calendar. Every automation needs a defined objective before it is built, or you cannot measure or improve it. See [set a goal before you build](/principles/goal-before-build.md).

> [!warning] An error in an automation runs at scale, silently
> A broadcast mistake reaches one audience once; a broken flow keeps misfiring to everyone who enters it. Test the trigger, content, and timing before going live.

Before you build any flow, write down the entry trigger (the event that admits a contact), the exit condition (the event that pulls them out, almost always the conversion the flow exists to drive), the goal metric you will read it against, the suppression rules that override it, and the channel each message goes out on. Get these on paper first; the message copy is the easy part.

## Trigger types

The entry trigger is whatever event your platform can listen for, and the menu varies between them. No flow needs all of them, and a trigger you lack can usually be reconstructed from one you have, so treat the list as options rather than requirements:

| Trigger | Fires when | Typical use |
| --- | --- | --- |
| List or segment entry | A contact is added to a list or segment, one at a time or as a batch | The workhorse, and an option in every capable platform: welcome series, onboarding, any flow keyed to joining a group. |
| Field or tag change | A field or tag on a contact is set or updated, including by an import touching many contacts at once | Reacting to a status the rest of your stack writes: a score crossing a threshold, a preference set, a tag applied. Widely supported. |
| Date based | A contact reaches a set offset from a date field | Birthday and anniversary messages, renewal and expiry reminders, a re-engagement nudge a fixed number of days after a last-purchase date. Common. |
| Import | A scheduled CSV drop to a secure FTP or similar location lands | Largely superseded by APIs and now mostly an enterprise-tier feature; once a standard way to drive flows such as an hourly abandoned-cart export. |
| Event or API | An in-platform behaviour (message interaction, page view, conversion) fires, or an external system calls the API | The open-ended one: anything your product, site, or app can signal. Advanced cases lean on a developer or a third-party integration. Widely supported. |
| RSS | A watched feed gains an item | New-post or new-content notifications, with the message templated from the feed item (title, content). Less widely supported. |

Choose by what your platform exposes and what writes the signal, not by the label on the menu. A field-change trigger fed by an import does the job an import trigger would; an API event can stand in for most of the rest. Where a trigger is missing, a little creativity against the ones you do have usually reaches the same outcome.

## Choosing the channel for each message

A sequence is a series of jobs, not a series of emails. Each message can go out on whichever channel fits its job. The outbound channels share one hard rule: you can only use a channel the contact has consented to, and consent does not transfer between channels. An email subscriber has not agreed to SMS or push, so most flows start email-only and gain other channels as those grants arrive. See [consent and preferences](/foundations/consent-and-preferences.md).

Choose the outbound channel by fit:

* **Email** is the default: rich layout, no per-message cost, room to explain. Most steps live here.
* **SMS** is immediate and near-certain to be seen, but short, interruptive, and costed per send. Reserve it for time-critical touches where being seen now is the point: an abandoned cart while intent is warm, a last call before a link expires.
* **Push**, app or browser, is free and immediate but easy to ignore and gone once dismissed. It suits users who have the app installed and a job that can be said in a line.

[In-app](/channels/in-app.md) sits apart from the three above, which is why it does not appear as a row in the cadence tables. It needs no opt-in, since the user is already inside the product, but it cannot initiate contact: it only fires when the user is in a session, so it cannot be scheduled as a touch at a fixed offset to someone who is not there. It carries the steps that land while the user is present, in-product onboarding, a finish-setup prompt, a cart reminder shown on the next visit, and leans on the outbound channels to do the reaching. Treat it as the destination a flow drives toward, fired on a session trigger, not as a timed step in the sequence.

The same frequency budget and collision rules govern every channel a flow uses, so a sequence does not get to spend contact allowance the broadcast calendar has already claimed. See [orchestration and frequency](/foundations/orchestration-and-frequency.md) for how the channel-per-job decision and the shared cap are managed across the programme.

## Welcome sequence

The welcome window is the highest engagement moment a subscriber will have with you, and welcome messages earn markedly higher open and click rates than ordinary campaigns, so the first one must deliver on whatever the signup promised. The signup happened on a channel, almost always email, and that is the channel that holds consent at this point, so the series runs there and reaches for another only once the subscriber has opted into it. A sensible default is a three to five message series, each with one job:

| Message | Timing | Channel | Job |
| --- | --- | --- | --- |
| 1 | Immediate, on signup | The channel the signup promise was made on, usually email | Deliver on the signup promise: send the lead magnet, confirm the subscription, set expectations for what and how often you will send. No selling. |
| 2 | ~24 hours later | Email | Tell the brand story and the one reason to care. Point to your best content or hero products. Soft, single call to action. |
| 3 | A few days later (~day 3 to 5) | Email, or push for subscribers who have the app | Handle the main objection and prompt the first action. Only here, if at all, does an incentive belong. |

Do not lead with a discount: it trains customers to game the system and attracts deal seekers. Offer incentives last, not first, and only to first time buyers where they make sense. Set the exit condition to the first purchase (or whatever the goal action is) so converters stop receiving the remaining onboarding messages. See [the welcome window](/principles/the-welcome-window.md) and [offers and incentives](/foundations/offers-and-incentives.md).

## Abandoned cart cadence

Most carts are abandoned, around seven in ten, so a recovery sequence is one of the highest-return automations there is. Trigger from the abandonment event with a short, useful sequence that reminds rather than nags. The immediacy of the trigger makes this the flow where SMS and push earn their place: a text or push notification while the cart is still warm is seen in minutes, where an email may wait for the next inbox check. Use them where you hold the consent, and keep email as the channel that carries the detail. A standard three-touch cadence, each touch with a distinct job:

| Touch | Timing | Channel | Job |
| --- | --- | --- | --- |
| 1 | ~1 hour after abandonment | Email, or SMS or push if you hold the consent | Plain reminder. Show the items, restore the cart in one click. Assume a distraction, not a decision. |
| 2 | ~24 hours after abandonment | Email | Handle the objection. Reinforce value: reviews, returns policy, shipping, stock. Still no discount. |
| 3 | ~72 hours after abandonment | Email, with SMS for a final time-boxed nudge | Optional urgency or, if your economics genuinely support it, a measured incentive. Last resort, not reflex. |

The same discount discipline applies: a reflexive discount in the first abandoned cart message teaches customers to abandon deliberately to summon one. Keep the incentive to the final touch, and only where the margin justifies it. Exit the flow on purchase. The same three-touch shape works for browse abandonment, with softer copy and no incentive, since intent is weaker than a built cart.

## Re-engagement and sunset

Run a re-engagement sequence for subscribers who have gone quiet, then sunset the ones who do not respond. This protects the engaged cohort rather than shrinking the asset, because dormant contacts drag sender level reach. See [engagement is the new deliverability](/principles/engagement-is-deliverability.md). This flow is the active step in the wider [database health and sunsetting](/foundations/database-health.md) lifecycle, which frames decay, re-engagement, and sunset as one ongoing practice.

Dormancy is usually measured per channel, so someone who has stopped opening email may still read a text or tap a push. The win-back is the natural place to try a channel the contact is not dormant on, where you hold the consent for it, since the whole point is to break a pattern that email alone is no longer breaking.

Define the trigger by an inactivity window: no open, click, or purchase for a period read off your own engagement distribution rather than a flat figure. The right length scales with how often you send and how often the customer naturally buys, since 90 days is dozens of sends for a daily sender and only a handful for a monthly one. The win-back is short, two to three messages:

| Message | Timing | Channel | Job |
| --- | --- | --- | --- |
| 1 | At the inactivity trigger | Email | Acknowledge the absence, remind them of the value, ask if they still want to hear from you. |
| 2 | ~5 to 7 days later | Email, or a channel they are not dormant on, such as SMS or push | Give one strong reason to return: best content, a saved-list nudge, or a genuine offer if it fits. |
| 3 | ~5 to 7 days later | Email | Explicit last call. State plainly that you will stop messaging unless they engage, with a one-click stay button. |

Sunset criteria: any contact who does not open, click, or purchase across the full win-back, and remains past the inactivity window, is suppressed from broadcast sending. Do not delete them outright; move them to a suppressed or sunset segment so the history survives and a future genuine re-opt-in can revive them. Sending to a never-engaging tail is what erodes deliverability for everyone else.

## Pre-launch testing

An error in an automation runs at scale and silently, so test every flow before it goes live to a real audience. Walk this checklist with a seeded test contact:

1. **Trigger fires.** The entry event admits the contact, and only that event does. Unrelated events do not enrol them.
2. **Entry and exit conditions hold.** Converters exit; non-qualifying contacts never enter; nobody can enter twice unintentionally.
3. **Each message goes out on the right channel, and renders there.** The step sends on its intended channel, every dynamic field resolves with a sane fallback for missing data, and the content fits the channel: no raw tokens, no broken links, no empty blocks, and nothing that overruns an SMS or a push notification.
4. **Timing gaps are correct.** The real delays between messages match the design, allowing for any quiet-hours or send-time rules, which differ by channel.
5. **Consent and suppression are respected.** A contact only receives a step on a channel they have consented to; unsubscribed, sunset, and globally suppressed contacts are excluded, and frequency caps from [orchestration and frequency](/foundations/orchestration-and-frequency.md) apply across all channels the flow uses.

Then watch a few metrics in the first days live, because they reveal a broken flow before subscribers complain:

* **Entry volume** against expectation. A flat zero means the trigger is misconfigured; a flood means the entry condition is too loose.
* **Send and delivery rate** per step. A step that never sends, or bounces hard, is broken.
* **Step-to-step progression and exit rate.** Nobody exiting on conversion suggests the exit condition is wrong; everybody dropping at one step points to that message.
* **Unsubscribe and spam-complaint rate.** A spike means cadence or targeting is off; pause and fix rather than let it run.

## Beyond static flows

Build these foundational automations well first. Where they go next, a system that decides per user what to send, when, and whether to send at all rather than dropping everyone into the same static flow, is the subject of [decisioning and personalisation](/foundations/decisioning-and-personalisation.md); the constraint there is data, not tooling.

## Related

* [The welcome window](/principles/the-welcome-window.md)
* [Set a goal before you build](/principles/goal-before-build.md)
* [Offers and incentives](/foundations/offers-and-incentives.md)
* [Consent and preferences](/foundations/consent-and-preferences.md)
* [Campaign planning and calendar](/foundations/campaign-planning-and-calendar.md)
* [Lifecycle mapping](/foundations/lifecycle-mapping.md)
* [In-app](/channels/in-app.md)
* [Orchestration and frequency](/foundations/orchestration-and-frequency.md)
* [Decisioning and personalisation](/foundations/decisioning-and-personalisation.md)
* [Engagement is the new deliverability](/principles/engagement-is-deliverability.md)

## Citations

[1] [HubSpot, email automation (trigger-based sending outperforms scheduled broadcasts)](https://www.hubspot.com/glossary/email-automation)
[2] [Mailmodo, welcome email statistics (higher open and click rates than standard campaigns)](https://www.mailmodo.com/guides/welcome-email-statistics/)
[3] [Baymard Institute, average cart abandonment rate (~70%)](https://baymard.com/lists/cart-abandonment-rate)
