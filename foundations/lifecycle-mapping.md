---
type: Framework
title: Lifecycle Mapping
description: The customer lifecycle stages a programme is built around, and how to map the journey into a copyable template, transition triggers, and a workshop that produces the spec your automations, orchestration, and measurement are built from.
tags: [lifecycle, journey-mapping, stages, retention, crm, workshop, triggers]
timestamp: 2026-06-14T00:00:00Z
---

## What it is

Lifecycle mapping is the discipline of describing where a customer is in their relationship with you, so that messaging responds to their state rather than to your campaign calendar. It is the organising frame that the channels, the automations, and the measurement all hang off. Without it you have a stream of broadcasts; with it you have a system.

## The stages

Most programmes resolve to five stages, whatever the local names.

* **Acquisition.** The lead is captured and consent is taken. The job is a clean, well sourced opt in, not a name on a list. See [list building](/foundations/list-building.md) and [consent and preferences](/foundations/consent-and-preferences.md).
* **Onboarding.** The first days, where the relationship is made or lost. The welcome window is the highest engagement you will ever have, so the activation job belongs here. See [the welcome window](/principles/the-welcome-window.md).
* **Engagement.** The long middle, where an active customer is nurtured, educated, and cross sold. Most volume lives here, and so does most of the risk of fatigue.
* **Retention.** Holding a customer who is at risk of lapsing, through value reminders, loyalty, and timely intervention. This is where the economics are decided. See [retention and LTV](/measurement/retention-and-ltv.md).
* **Winback.** Reactivating the lapsed, and the honest decision to stop mailing the truly disengaged because continuing to mail them is a deliverability cost. See [engagement is the new deliverability](/principles/engagement-is-deliverability.md).

## Mapping the journey

A journey map lays the stages against the moments that move a customer between them: the trigger events, the decisions, the points of friction, and the messages each stage should carry. The output is not a diagram for its own sake. It is the specification the [automations](/foundations/automation-and-sequences.md) implement and the [orchestration](/foundations/orchestration-and-frequency.md) layer sequences across channels.

## The journey-map template

Map one row per stage, then split a stage into multiple rows where the customer job differs (a new buyer and a repeat buyer in Engagement are two rows). Copy this table and fill it in. The illustrative entries below show the shape, not a recommendation for your programme.

| Stage | Customer job | Entry trigger | Key messages | Channel | Goal / decision metric | Frequency |
| --- | --- | --- | --- | --- | --- | --- |
| Acquisition | Decide whether to opt in | Form submit, consent captured | Confirm, set expectations | Email | Confirmed opt-in rate | Once, plus reminder |
| Onboarding | Get first value | Opt-in confirmed | Welcome, activate the core action | Email, push | Activation rate (first key action) | Short burst over the welcome window |
| Engagement | Get ongoing value | Activated, or first repeat action | Education, cross-sell, content | Email, push, in-app | Repeat-action rate, revenue per active | Steady, capped by frequency rules |
| Retention | Avoid lapsing | Engagement score drops below threshold | Value reminder, loyalty, save offer | Email, SMS | Lapse rate, reactivation within window | Triggered, low base rate |
| Winback | Reconsider the relationship | Inactivity window exceeded | Reactivation, last value, sunset | Email, SMS | Reactivation rate, then suppression | Few attempts, then stop |

## Stage-transition triggers

Each move between stages needs a defined entry trigger and an exit, so a customer is only ever in one stage and the [automations](/foundations/automation-and-sequences.md) know when to start and stop. The windows below are illustrative defaults, not benchmarks; set them from your own purchase cycle and inactivity distribution.

* **Acquisition to Onboarding.** Consent confirmed. The trigger is the confirmation event, not the form submit.
* **Onboarding to Engagement.** First repeat key action (a second session, second purchase), OR a fixed window elapses, say 14 days, whichever comes first. Promote on the behaviour when you can, on the clock when you cannot.
* **Engagement to Retention.** An inactivity or declining-engagement signal: no key action for an at-risk window, say 30 days, or an engagement score crossing a threshold. This is a risk indicator, not a lapse yet.
* **Retention to Winback.** Inactivity exceeds the lapsed window, say 90 days, with no response to retention messaging.
* **Winback to suppressed.** A capped number of reactivation attempts, say three, with no engagement. Stopping is the action; continuing to mail the unresponsive is a deliverability cost. See [engagement is the new deliverability](/principles/engagement-is-deliverability.md).

An **engagement score** is the composite those transitions test: a single measure of how recently and how often a customer engages, rolled up from the signals below — opens, clicks, sessions, purchases over a rolling window — into one number a rule can compare against a threshold. It is the same recency-and-frequency logic [segmentation models](/foundations/segmentation-models.md) use to score an audience, applied here to drive stage transitions rather than segments, and banded into [engagement tiers](/foundations/orchestration-and-frequency.md) to set frequency. Define it from the signals you can instrument and set the threshold from your own distribution, not from a borrowed number.

Risk indicators worth watching inside Engagement and Retention, before a hard transition fires: falling open or click rate over a rolling window, lengthening gaps between key actions, a single high-value action followed by silence, and declining session frequency.

## Running a lifecycle-mapping workshop

A map is produced by the people who own the customer, not drafted alone in a tool. Run a single working session of roughly two hours to get a first draft on the wall.

* **Who is in the room.** The CRM or lifecycle owner facilitates. Bring product or growth (they know the activation moment), data or analytics (they know what is measurable today), customer support (they know the friction), and someone who can approve channels and budget. Keep it small enough to decide.
* **The prompts, in order.** Name the five stages in your language. For each stage ask: what is the customer trying to do here? What event tells us they have entered this stage? What event tells us they have left it, up or down? What is the one thing we want them to do, and how would we measure it? What is the risk that loses them here?
* **The output.** A filled-in journey-map table, one row per stage and per distinct customer job, with every entry and exit trigger named and every goal tied to a metric the data owner has confirmed is trackable. Flag rows where the trigger is not yet instrumented; those are the build backlog before the automation can exist.

## How the map drives builds

The map is not documentation, it is the build spec. Each row becomes an [automation](/foundations/automation-and-sequences.md): the entry trigger is its start condition, the key messages are its steps, the exit trigger and frequency are its stop rules. The rows together feed [orchestration](/foundations/orchestration-and-frequency.md), which sequences across stages and channels and enforces frequency so two stages do not message the same person at once. Each row's goal metric is then read per stage through [core metrics](/measurement/core-metrics.md), so you measure activation against Onboarding and lapse against Retention rather than one programme-wide average that hides both.

## Why it comes first

Channel and tooling choices follow the map, not the other way round. The stage decides the job, the job decides the message, and only then does the channel decide the delivery. A programme that picks the channel first ends up sending the same broadcast everywhere and calling it lifecycle. See [set a goal before you build](/principles/goal-before-build.md).

## Related

* [Automation and sequences](/foundations/automation-and-sequences.md)
* [Orchestration and frequency](/foundations/orchestration-and-frequency.md)
* [Segmentation models](/foundations/segmentation-models.md)
* [Loyalty and retention programs](/foundations/loyalty-and-retention-programs.md)
* [The welcome window](/principles/the-welcome-window.md)
* [Retention and LTV](/measurement/retention-and-ltv.md)

## Citations

[1] [Braze, customer lifecycle management (acquisition, activation, engagement, retention, reactivation)](https://www.braze.com/resources/articles/customer-lifecycle-management)
