---
type: Playbook
title: Automation and Sequences
description: How to build trigger-based welcome, abandoned cart, and re-engagement flows, with message-by-message cadences, sunset criteria, and a pre-launch testing checklist.
tags: [automation, welcome, abandoned-cart, re-engagement, sunset, lifecycle]
timestamp: 2026-06-14T00:00:00Z
---

# Triggers and goals

An automation fires from an event (signup, purchase, browse, inactivity) rather than a calendar. Every automation needs a defined objective before it is built, or you cannot measure or improve it. See [set a goal before you build](/principles/goal-before-build.md). Always test the trigger, content, and timing before going live, because an error in an automation runs at scale, silently.

Before you build any flow, write down four things: the entry trigger (the event that admits a contact), the exit condition (the event that pulls them out, almost always the conversion the flow exists to drive), the goal metric you will read it against, and the suppression rules that override it. Get these on paper first; the message copy is the easy part.

# Welcome sequence

The welcome window is the highest engagement moment a subscriber will have with you, and welcome emails earn markedly higher open and click rates than ordinary campaigns, so the first email must deliver on whatever the signup promised. A sensible default is a three to five message series, each with one job:

| Message | Timing | Job |
| --- | --- | --- |
| 1 | Immediate, on signup | Deliver on the signup promise: send the lead magnet, confirm the subscription, set expectations for what and how often you will send. No selling. |
| 2 | ~24 hours later | Tell the brand story and the one reason to care. Point to your best content or hero products. Soft, single call to action. |
| 3 | A few days later (~day 3 to 5) | Handle the main objection and prompt the first action. Only here, if at all, does an incentive belong. |

Do not lead with a discount: it trains customers to game the system and attracts deal seekers. Offer incentives last, not first, and only to first time buyers where they make sense. Set the exit condition to the first purchase (or whatever the goal action is) so converters stop receiving the remaining onboarding messages. See [the welcome window](/principles/the-welcome-window.md) and [offers and incentives](/foundations/offers-and-incentives.md).

# Abandoned cart cadence

Most carts are abandoned, around seven in ten, so a recovery sequence is one of the highest-return automations there is. Trigger from the abandonment event with a short, useful sequence that reminds rather than nags. A standard three-touch cadence, each touch with a distinct job:

| Touch | Timing | Job |
| --- | --- | --- |
| 1 | ~1 hour after abandonment | Plain reminder. Show the items, restore the cart in one click. Assume a distraction, not a decision. |
| 2 | ~24 hours after abandonment | Handle the objection. Reinforce value: reviews, returns policy, shipping, stock. Still no discount. |
| 3 | ~72 hours after abandonment | Optional urgency or, if your economics genuinely support it, a measured incentive. Last resort, not reflex. |

The same discount discipline applies: a reflexive discount in the first abandoned cart message teaches customers to abandon deliberately to summon one. Keep the incentive to the final touch, and only where the margin justifies it. Exit the flow on purchase. The same three-touch shape works for browse abandonment, with softer copy and no incentive, since intent is weaker than a built cart.

# Re-engagement and sunset

Run a re-engagement sequence for subscribers who have gone quiet, then sunset the ones who do not respond. This protects the engaged cohort rather than shrinking the asset, because dormant contacts drag sender level reach. See [engagement is the new deliverability](/principles/engagement-is-deliverability.md).

Define the trigger by an inactivity window: no open, click, or purchase for a set period. A sensible default is 90 days. The win-back is short, two to three messages:

| Message | Timing | Job |
| --- | --- | --- |
| 1 | At the inactivity trigger | Acknowledge the absence, remind them of the value, ask if they still want to hear from you. |
| 2 | ~5 to 7 days later | Give one strong reason to return: best content, a saved-list nudge, or a genuine offer if it fits. |
| 3 | ~5 to 7 days later | Explicit last call. State plainly that you will stop emailing unless they engage, with a one-click stay button. |

Sunset criteria: any contact who does not open, click, or purchase across the full win-back, and remains past the inactivity window, is suppressed from broadcast sending. Do not delete them outright; move them to a suppressed or sunset segment so the history survives and a future genuine re-opt-in can revive them. Sending to a never-engaging tail is what erodes deliverability for everyone else.

# Pre-launch testing

An error in an automation runs at scale and silently, so test every flow before it goes live to a real audience. Walk this checklist with a seeded test contact:

1. **Trigger fires.** The entry event admits the contact, and only that event does. Unrelated events do not enrol them.
2. **Entry and exit conditions hold.** Converters exit; non-qualifying contacts never enter; nobody can enter twice unintentionally.
3. **Content and merge fields render.** Every dynamic field resolves, with a sane fallback for missing data. No raw tokens, no broken links, no empty blocks.
4. **Timing gaps are correct.** The real delays between messages match the design, allowing for any quiet-hours or send-time rules.
5. **Suppression is respected.** Unsubscribed, sunset, and globally suppressed contacts are excluded, and frequency caps from [orchestration and frequency](/foundations/orchestration-and-frequency.md) apply.

Then watch a few metrics in the first days live, because they reveal a broken flow before subscribers complain:

* **Entry volume** against expectation. A flat zero means the trigger is misconfigured; a flood means the entry condition is too loose.
* **Send and delivery rate** per step. A step that never sends, or bounces hard, is broken.
* **Step-to-step progression and exit rate.** Nobody exiting on conversion suggests the exit condition is wrong; everybody dropping at one step points to that message.
* **Unsubscribe and spam-complaint rate.** A spike means cadence or targeting is off; pause and fix rather than let it run.

# Beyond static flows

Build these foundational automations well first. Where they go next, a system that decides per user what to send, when, and whether to send at all rather than dropping everyone into the same static flow, is the subject of [decisioning and personalisation](/foundations/decisioning-and-personalisation.md); the constraint there is data, not tooling.

# Related

* [The welcome window](/principles/the-welcome-window.md)
* [Set a goal before you build](/principles/goal-before-build.md)
* [Offers and incentives](/foundations/offers-and-incentives.md)
* [Campaign planning and calendar](/foundations/campaign-planning-and-calendar.md)
* [Lifecycle mapping](/foundations/lifecycle-mapping.md)
* [Orchestration and frequency](/foundations/orchestration-and-frequency.md)
* [Decisioning and personalisation](/foundations/decisioning-and-personalisation.md)
* [Engagement is the new deliverability](/principles/engagement-is-deliverability.md)

# Citations

[1] [HubSpot, email automation (trigger-based sending outperforms scheduled broadcasts)](https://www.hubspot.com/glossary/email-automation)
[2] [Mailmodo, welcome email statistics (higher open and click rates than standard campaigns)](https://www.mailmodo.com/guides/welcome-email-statistics/)
[3] [Baymard Institute, average cart abandonment rate (~70%)](https://baymard.com/lists/cart-abandonment-rate)
