---
type: Method
title: Impact Sizing
description: How to size the potential impact of an experiment so experiments can be ranked, using three model types and a shared core formula.
tags: [impact-sizing, prioritisation, modelling, experiments]
timestamp: 2026-06-14T00:00:00Z
---

# What it is

Impact sizing answers one question: how many incremental actions will this experiment drive? That number lets you rank experiments, set stakeholder expectations, and judge afterward whether an experiment delivered. It is not forecasting. It is a calculator that says if we achieve X% lift on metric Y for Z users, the result is N incremental actions. The model is only as good as its inputs, but even rough inputs give useful prioritisation signal.

# Three model types

* **Single metric**, the default. One metric to move (activation, adoption, conversion). Take the audience, apply the baseline rate, apply a lift, calculate incremental actions.
* **Two metric funnel.** An upfunnel action that feeds a downstream outcome. If someone says we want to improve X because it drives Y, the because signals a funnel. Needs the upfunnel rate and the downstream conversion rate.
* **Promotional.** Free months, discounts, credits. The question is not how many incremental actions but whether you gain more than the promotion costs, and on what time frame. Needs plan mix, per plan gross profit, promo cost, and a retention adjustment for promo acquired users.

# The core formula

```
Non-actors          = Audience x (1 - Baseline rate)
Target rate         = Baseline rate x (1 + Relative lift)
Incremental actions = (Target rate - Baseline rate) x Non-actors
```

Funnel adds: `Incremental downstream = Incremental upfunnel x Downstream conversion rate`.

Promotional shifts to net value: `(Incremental subs x Retention-adjusted GP) - (Incremental subs x Weighted promo cost)`, revenue positive when above zero.

The relative lift is the one variable you change to model scenarios. Everything else is an observed input.

# Getting inputs right

* **Metric definition.** Confirm numerator, denominator, and time window. A 7 day rate is a different model from a 30 day rate.
* **Baseline.** Ask where it came from and when. A holiday period or post launch baseline skews the model.
* **Flow versus stock.** A flow targets new users entering each week (incremental actions per week). A stock targets a fixed existing pool (a total). Mixing them up inflates or deflates the estimate dramatically.
* **Segment overlap.** Confirm segments are mutually exclusive before adding them, or you double count.
* **Lift target.** Use precedent if you have it. Otherwise 5% relative is a reasonable conservative default, flagged clearly as an assumption.

# Common mistakes

* Sizing without defining the metric first.
* Using stale baselines.
* Ignoring the flow versus stock distinction.
* Over segmenting small audiences below the point where lift is detectable.
* Treating the model output as a commitment. It says plausible if assumptions hold, not this will happen. Do not set OKR targets from it.

# Related

* [Sample size and power](/measurement/sample-size-and-power.md)
* [Set a goal before you build](/principles/goal-before-build.md)
* [Uplift and incrementality](/measurement/uplift-and-incrementality.md)

# Citations

[1] [Kohavi, Tang & Xu, Trustworthy Online Controlled Experiments (effect sizing and prioritising experiments)](https://experimentguide.com/)
