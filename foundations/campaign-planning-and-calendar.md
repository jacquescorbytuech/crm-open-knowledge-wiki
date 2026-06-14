---
type: Playbook
title: Campaign Planning and Calendar
description: How to plan the sending programme as a system rather than a queue, the split between triggered and broadcast messaging, the marketing calendar that coordinates them, and the governance that keeps a multi-person programme consistent.
tags: [planning, calendar, broadcast, triggered, governance, cadence]
timestamp: 2026-06-14T00:00:00Z
---

# Two kinds of sending

A lifecycle programme sends in two modes, and they are planned differently.

* **Triggered** messages fire from a customer's behaviour or state, a signup, a purchase, an abandonment, a lapse, and run continuously once built. They carry most of the relevance because they arrive when the customer's action made the message timely. Trigger-based sending consistently outperforms scheduled broadcasts on engagement and revenue per recipient.
* **Broadcast** (batch) messages go to a segment on a schedule: the newsletter, the launch, the promotion. They are how the calendar's planned moments reach the audience.

Most programmes lean too hard on broadcast because it is the visible, plannable work, and under-invest in the triggered layer that quietly does more. Plan the triggered backbone first, then schedule broadcasts around it. See [automation and sequences](/foundations/automation-and-sequences.md).

# The marketing calendar

The calendar is the shared plan of what broadcasts go out, to whom, and when, across the channels. Its job is not to fill every slot but to coordinate: to make the launch, the seasonal moment, and the promotion line up rather than collide, and to make the total contact load visible before it is sent. A calendar planned per channel re-creates the collision problem the [contact strategy](/foundations/orchestration-and-frequency.md) exists to prevent, so plan it across channels, against the one contact budget.

# Cadence and the contact budget

Decide cadence from what the audience tolerates and what you have to say, not from a quota of sends to hit. Over-sending is the fastest way to lose a list: too many messages is consistently the top reason people unsubscribe and complain, and both signals drive [deliverability](/foundations/deliverability.md) down. The calendar should respect the [frequency caps](/foundations/orchestration-and-frequency.md), counting triggered sends against the same budget, not just the broadcasts.

# Goals before slots

Every planned campaign needs a defined objective before it earns a place on the calendar, or it cannot be measured or improved and becomes filler. The slot does not justify the send; the goal does. See [set a goal before you build](/principles/goal-before-build.md).

# Governance

Once more than one person sends, the programme needs light governance to stay consistent: an agreed workflow from brief through copy, design, and approval to scheduling; a single source of truth for the calendar; and a QA step, send to a seed list, check rendering and links, confirm the audience and suppressions, before anything goes out. The discipline matters most for [automations](/foundations/automation-and-sequences.md), because an error there runs at scale and silently.

# Related

* [Automation and sequences](/foundations/automation-and-sequences.md)
* [Orchestration and frequency](/foundations/orchestration-and-frequency.md)
* [Set a goal before you build](/principles/goal-before-build.md)
* [Offers and incentives](/foundations/offers-and-incentives.md)
* [Lifecycle mapping](/foundations/lifecycle-mapping.md)

# Citations

[1] [HubSpot, email automation (trigger-based sending outperforms scheduled broadcasts)](https://www.hubspot.com/glossary/email-automation)
[2] [Klaviyo, ecommerce benchmarks (targeted and automated sends beat broad broadcasts on revenue per recipient)](https://www.klaviyo.com/marketing-resources/ecommerce-benchmarks)
[3] [MarketingSherpa, why consumers unsubscribe (too many emails is the top reason)](https://marketingsherpa.com/article/chart/why-consumers-unsubscribe)
[4] [HubSpot, building an editorial/marketing calendar with an approval workflow](https://blog.hubspot.com/marketing/business-blog-editorial-calendar-templates)
