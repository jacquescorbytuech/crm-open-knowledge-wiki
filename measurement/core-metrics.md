---
type: Concept
title: Core Metrics
description: The metric tree a lifecycle programme is judged on, from engagement through conversion to retention and revenue, and how to choose a North Star, set guardrails, and tell the metrics that decide actions from the ones that only decorate a dashboard.
tags: [metrics, metric-tree, north-star, guardrails, kpis, leading-indicators]
timestamp: 2026-06-14T00:00:00Z
---

## The metric tree

A lifecycle programme is measured in layers, each one closer to money than the last. Read them as a tree, not a list, because a win at one level only counts if it survives to the next.

* **Engagement.** Open, click, click to open, reply, and their channel equivalents. The earliest and noisiest signals, and the most corrupted by intermediation. Useful for diagnosis, dangerous as goals. See [metrics are directional](/principles/metrics-are-directional.md).
* **Conversion.** The action the message existed to drive: a purchase, an upgrade, an activation, a booking. The first level that means something on its own.
* **Retention.** Whether the customer stays, repeats, and remains reachable over time. Where the economics of the programme are actually decided. See [retention and LTV](/measurement/retention-and-ltv.md).
* **Revenue and value.** Incremental revenue, margin, and lifetime value. The level the business cares about, and the one the others should ladder up to.

## Decision metrics versus vanity metrics

A decision metric changes what you do when it moves. A vanity metric only changes how you feel. Open rate rising while conversion is flat is a vanity result, and after Mail Privacy Protection inflated opens it is often not even real.

The test for any metric on a dashboard is one question: if this number moved ten percent, would it change what you do next week? Walk it through:

* Name the move. Write down the concrete action a ten percent swing would trigger: cut a flow, shift budget, change a send time, raise an alarm.
* If there is no action, the metric is decoration. Move it off the scorecard and into diagnostics, where it earns its place by explaining other numbers, not by being a goal.
* Watch for proxies that have drifted from the thing they proxy. Opens once tracked attention; MPP severed that link, so an opens move no longer maps to any reliable action. A metric that can rise without the underlying value rising is a vanity metric whatever it used to be.

Most dashboards carry more vanity than decision metrics. The work is demoting the decoration, not adding more of it.

## A North Star and its guardrails

Pick one North Star metric that best proxies the value the programme creates, low enough in the tree to be honest and high enough to matter, often incremental revenue per recipient or a retention measure.

## How to choose a North Star

A candidate metric earns the role only if it passes each of these tests. Treat them as a decision rule, not a wish list.

* **In the causal path to value.** Moving it should move the business, not just a dashboard. Incremental revenue per recipient and repeat purchase rate sit on the path; open rate does not, because a programme can lift opens without lifting a thing the business sells.
* **Movable by the programme.** The team must be able to shift it with the levers it actually controls: content, targeting, timing, frequency. Total company revenue fails here, because pricing, product, and acquisition swamp anything CRM does. A North Star you cannot move is a report, not a goal.
* **Not a vanity proxy.** It must fail the demotion test above: a real change in it should force a real change in action. A metric that can be inflated without creating value, like opens after MPP, disqualifies itself.

| Candidate | In causal path | Movable by programme | Not a vanity proxy | Verdict |
| --- | --- | --- | --- | --- |
| Incremental revenue per recipient | Yes | Yes | Yes | Good North Star |
| Repeat purchase or retention rate | Yes | Yes | Yes | Good, especially retention-led programmes |
| Open rate | No | Partly | No, post-MPP | Bad, vanity proxy |
| Total company revenue | Yes | No | Yes | Bad, programme cannot move it |
| Emails sent | No | Yes | No | Bad, an activity count, not value |

Prefer the version of a good metric that is measured incrementally, against a holdout, rather than as a gross total a last-touch report would claim. See [uplift and incrementality](/measurement/uplift-and-incrementality.md) and [holdouts and control groups](/measurement/holdouts-and-control-groups.md).

## How to set guardrails

Any single optimised number can be hit by gaming the things it ignores. Guardrails are counter-metrics you cap so the North Star cannot be won by harm. Pick a North Star, then ask how a lazy optimiser would cheat it, and put a ceiling on each cheat.

* **Unsubscribe rate.** Caps the urge to lift short-term conversion by mailing harder. If unsubscribes breach the cap, the win is borrowed against future reach.
* **Spam complaint rate.** Caps annoyance that does not show up as an unsubscribe. Complaints damage sender reputation directly. See [deliverability](/foundations/deliverability.md).
* **Deliverability and inbox placement.** Caps the temptation to chase engaged-looking volume at the cost of landing in spam. Engagement is deliverability, so this guardrail protects the channel itself. See [engagement is deliverability](/principles/engagement-is-deliverability.md).
* **Frequency or sends per recipient.** Caps list-burning. A North Star hit by tripling volume is not a real gain. See [orchestration and frequency](/foundations/orchestration-and-frequency.md).

The rule: a North Star move only counts if every guardrail stayed inside its cap. Optimising a North Star without guardrails is how a programme hits its target by burning the list to do it. Set the cap levels from your own baseline and tolerance, not from invented benchmarks; see [volume thresholds](/measurement/volume-thresholds.md) and [sample size and power](/measurement/sample-size-and-power.md).

## Tie metrics to the lifecycle

Different stages are judged on different levels of the tree. A single blended dashboard hides all of this, because a stage doing its job and a stage failing average out to a flat number. Give each stage one decision metric it lives or dies on.

| Stage | Decision metric | The question it answers |
| --- | --- | --- |
| Onboarding | Activation rate | Did the new user reach first value? |
| Engagement (mid-lifecycle) | Active rate | Are existing users still acting, not just present? |
| Retention | Cohort retention | Does a cohort stay across months, not just the first week? |
| Winback | Reactivation rate | Did a lapsed user come back and do something? |

Read retention as a cohort, not a snapshot, so a flood of new users cannot mask churn in older ones. See [lifecycle mapping](/foundations/lifecycle-mapping.md) and [retention and LTV](/measurement/retention-and-ltv.md).

## Leading and lagging indicators

A North Star like incremental revenue per recipient or cohort retention is a lagging indicator: it tells you the truth, but late, after the cohort has had time to stay or leave. You cannot steer a quarter on a number you only learn at the end of it.

So watch leading indicators alongside it: earlier, movable signals that tend to precede the lagging one. Activation in week one leads retention at month three; click-to-conversion on a flow leads its incremental revenue. The discipline is using leading indicators to act fast and lagging indicators to confirm the action worked, never trusting a leading move until the lagging number follows. A leading indicator that stops predicting its lagging partner has decayed into a vanity metric, and the demotion test applies again.

## Related

* [Metrics are directional](/principles/metrics-are-directional.md)
* [Uplift and incrementality](/measurement/uplift-and-incrementality.md)
* [Retention and LTV](/measurement/retention-and-ltv.md)
* [Impact sizing](/measurement/impact-sizing.md)
* [Volume thresholds](/measurement/volume-thresholds.md)
* [Sample size and power](/measurement/sample-size-and-power.md)
* [Lifecycle mapping](/foundations/lifecycle-mapping.md)
* [Orchestration and frequency](/foundations/orchestration-and-frequency.md)

## Citations

[1] [Apple, Mail Privacy Protection (Apple Support)](https://support.apple.com/guide/iphone/protect-mail-activity-iphd22a4a3a8/ios)
