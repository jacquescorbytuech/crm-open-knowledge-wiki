---
type: Playbook
title: Campaign Planning and Calendar
description: How to plan and run the sending programme as a system, the split between triggered and broadcast messaging, how to lay out and cadence a cross-channel calendar, the campaign production workflow with owners, and a pre-send QA checklist.
tags: [planning, calendar, broadcast, triggered, governance, cadence, workflow, qa, seed-list]
timestamp: 2026-06-14T00:00:00Z
---

## Triggered and broadcast sending

A lifecycle programme sends triggered and broadcast messages, and plans them differently.

* **Triggered** messages fire from a customer's behaviour or state, a signup, a purchase, an abandonment, a lapse, and run continuously once built. They carry most of the relevance because they arrive when the customer's action made the message timely. Trigger-based sending consistently outperforms scheduled broadcasts on engagement and revenue per recipient.
* **Broadcast** (batch) messages go to a segment on a schedule: the newsletter, the launch, the promotion. They are how the calendar's planned moments reach the audience.

Most programmes lean too hard on broadcast because it is the visible, plannable work, and under-invest in the triggered layer that quietly does more. Plan the triggered backbone first, then schedule broadcasts around it. See [automation and sequences](/foundations/automation-and-sequences.md).

## The marketing calendar

The calendar is the shared plan of what broadcasts go out, to whom, and when, across the channels. Its job is not to fill every slot but to coordinate: to make the launch, the seasonal moment, and the promotion line up rather than collide, and to make the total contact load visible before it is sent. A calendar planned per channel re-creates the collision problem the [contact strategy](/foundations/orchestration-and-frequency.md) exists to prevent, so plan it across channels, against the one contact budget.

## What the planning view contains

Lay the calendar out as a grid of time against channel lanes, so total contact load down any week is visible at a glance. A workable default view holds:

* **Channel lanes.** One row per channel, email, SMS, push, in-app, so a recipient's combined load across lanes is read vertically, not buried in separate tools.
* **Broadcast slots.** Each planned batch send: the campaign name, segment, goal, and proposed date. An empty slot is fine; a slot with no goal is not.
* **Triggered/automation checkpoints.** The live flows are not scheduled, but mark them on the view so planners see them competing for the same contact budget, and flag the moments a broadcast would land on top of a heavy trigger (a sale email into an active abandonment series).
* **Key retail and seasonal moments.** The fixed anchors the plan bends around: your category's peak periods, paydays, your own launch and renewal dates, and the public holidays of your main markets. Place these first, then plan campaigns relative to them.
* **Suppression and exclusion notes.** Who is held back or excluded for a given send, recent purchasers, an experiment holdout, so it is decided in planning, not at build.

## Cadence of planning

Run a rolling plan, not a fixed quarterly document that goes stale by week two. A default rhythm:

* **Rolling monthly horizon.** Keep roughly the next month firmly planned and the month after sketched, so launches have lead time without committing to slots you cannot yet brief.
* **Weekly review.** Once a week, walk the next two weeks: confirm what is briefed and on track, resolve any collisions, fill or kill empty slots, and check the contact load against the budget.
* **Seasonal pass.** Before each major retail or seasonal peak, plan that window in more detail and earlier than the normal horizon, because lead times and creative load are larger.

## Cadence and the contact budget

Decide cadence from what the audience tolerates and what you have to say, not from a quota of sends to hit. Over-sending is the fastest way to lose a list: too many messages is consistently the top reason people unsubscribe and complain, and both signals drive [deliverability](/foundations/deliverability.md) down. The calendar should respect the [frequency caps](/foundations/orchestration-and-frequency.md), counting triggered sends against the same budget, not just the broadcasts.

## Goals before slots

Every planned campaign needs a defined objective before it earns a place on the calendar, or it cannot be measured or improved and becomes filler. The slot does not justify the send; the goal does. Frame each campaign in one line before it is built: who it is for, the single action you want them to take, and the one metric that says it worked, with a rough target. If you cannot fill that line, the campaign is not ready to schedule. See [set a goal before you build](/principles/goal-before-build.md).

## The production workflow

Once more than one person sends, the programme needs a single agreed workflow so nothing ships half-built. Run each campaign through these ordered steps, each with a named owner, so a missed handoff is visible:

1. **Brief.** Campaign owner writes the one-line goal frame, audience, offer, key message, and the send window. Nothing proceeds without it.
2. **Copy.** Copywriter drafts subject, preheader, body, and call to action against the brief.
3. **Design.** Designer produces the creative and any assets, to template, with alt text supplied for every image.
4. **Build.** Email/CRM specialist assembles the message in the platform, wires links and UTMs, and sets the suppression and frequency logic.
5. **Send-list and QA.** Owner pulls and confirms the target audience and its count, then runs the pre-send QA checklist below against a seed list. Owner or a second person signs off.
6. **Schedule.** Specialist schedules the send for the planned slot, against the single source-of-truth calendar.
7. **Post-send review.** Owner reads results against the goal metric within a few days, records what to repeat or change, and feeds it back into the next plan.

## Pre-send QA checklist

Run this before every broadcast, and before activating any automation, since an automation error runs at scale and silently. Do not skip it because the campaign looks small.

* [ ] **Subject line** present, correct, and within the platform's display length.
* [ ] **Preheader** set and not pulling stray body text.
* [ ] **From-name and from-address** correct and on an authenticated sending domain.
* [ ] **Links** all resolve to the right pages, with no placeholders, and **UTMs** present and consistent.
* [ ] **Images** load, and every image has **alt text** for blocked-image and accessibility cases.
* [ ] **Render and seed test** passed across major mail clients, mobile, and dark mode.
* [ ] **Audience count** matches the expected number; investigate any large gap before sending.
* [ ] **Suppression and frequency logic** applied: exclusions, recent-send caps, and any holdout in place.
* [ ] **Tracking** configured so the send can be read against its goal metric.

## Seed-list and inbox testing

A seed list is a set of internal and proxy addresses you send a final test to before the real audience, to catch what a content preview cannot: how the message actually renders and behaves in a real inbox. Maintain a standing seed list and cover, at minimum:

* **Major mail clients and webmail** your audience actually uses, since rendering differs sharply between them.
* **Mobile**, where most opens happen, checking the message holds up at a narrow width.
* **Dark mode**, where backgrounds invert and logos or text on transparent images can disappear.
* **Seats for major clients or VIP segments**, if you serve any, so a key recipient never receives something untested.

Where the platform offers an inbox-preview render gallery, use it alongside live seeds, not instead of them.

## Governance

Once more than one person sends, the programme needs light governance to stay consistent: the agreed production workflow above, a single source of truth for the calendar, and the pre-send QA step before anything goes out. An automation error runs at scale and silently, so apply this discipline to [automations](/foundations/automation-and-sequences.md) first. Keep one owner accountable for the calendar and the contact budget, so collisions are resolved by a person, not discovered by recipients.

## Related

* [Automation and sequences](/foundations/automation-and-sequences.md)
* [Orchestration and frequency](/foundations/orchestration-and-frequency.md)
* [Set a goal before you build](/principles/goal-before-build.md)
* [Offers and incentives](/foundations/offers-and-incentives.md)
* [Lifecycle mapping](/foundations/lifecycle-mapping.md)
* [Deliverability](/foundations/deliverability.md)

## Citations

[1] [HubSpot, email automation (trigger-based sending outperforms scheduled broadcasts)](https://www.hubspot.com/glossary/email-automation)
[2] [Klaviyo, ecommerce benchmarks (targeted and automated sends beat broad broadcasts on revenue per recipient)](https://www.klaviyo.com/marketing-resources/ecommerce-benchmarks)
[3] [MarketingSherpa, why consumers unsubscribe (too many emails is the top reason)](https://marketingsherpa.com/article/chart/why-consumers-unsubscribe)
[4] [HubSpot, building an editorial/marketing calendar with an approval workflow](https://blog.hubspot.com/marketing/business-blog-editorial-calendar-templates)
