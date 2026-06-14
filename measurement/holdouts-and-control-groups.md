---
type: Method
title: Holdouts and Control Groups
description: How to size, randomise, maintain, and read an always-on global holdout and per-campaign control groups, plus geo experiments when individuals cannot be split, so you measure programme incrementality honestly.
tags: [holdout, control-group, incrementality, experiment, geo-lift, causal, randomisation]
timestamp: 2026-06-14T00:00:00Z
---

## The question only a control group answers

Attribution tells you which messages preceded a conversion. It cannot tell you which conversions would have happened anyway. Only withholding the message from a randomly chosen, otherwise identical group, and comparing outcomes, isolates the lift the programme actually caused. The difference between the treated group and the control is incrementality, and it is the only number that proves the programme created value rather than taking credit for it.

## The always-on global holdout

Hold back a small, randomly selected share of the addressable audience from all lifecycle messaging, continuously. The gap between the holdout and the mailed population, measured on conversion, retention, and revenue, is the incremental contribution of the entire programme.

> [!important] The question a global holdout answers
> It is the single most valuable measurement a CRM team can run, because it answers the question executives rarely ask out loud: what would happen to revenue if we sent nothing?

Keep it small, keep it random, and keep it permanent.

## Per-campaign control groups

For an individual send, sequence, or new automation, hold out a control from the eligible audience and measure the same outcomes. This reads the incremental effect of that specific intervention rather than the programme as a whole, and it is how a new idea earns its place before it is rolled out. The discipline is the same one direct mail has always used: the mailed file against a held back control. See [direct mail](/channels/direct-mail.md).

## How to size and place a holdout

There is no universal percentage. The size of a holdout is a trade-off you set deliberately, not a number to copy:

* A bigger holdout tightens the read. More users on each side narrows the interval around the measured lift, so you can detect a smaller effect and see it sooner.
* A bigger holdout withholds more revenue. Everyone in the holdout gets no messaging, so the holdout itself has a cost while it runs.

Pick the smallest holdout that can still detect the effect size that would change a decision over the period you are willing to wait. The exact n is a power question, not a rule of thumb: work it from the baseline rate, the minimum effect worth detecting, and the cell volume available, per [sample size and power](/measurement/sample-size-and-power.md), and check it against the per-cell floor in [volume thresholds](/measurement/volume-thresholds.md). Two further rules hold regardless of size: the holdout must be random, and for a global holdout it must be stable over the measurement period (see maintenance below).

## How to randomise correctly

The read is only as honest as the assignment. Get this wrong and the gap you measure is selection bias, not lift.

1. Assign at the person level, not the send level. A user is in or out of the holdout as a person, so they stay out of every message, not just one.
2. Use a stable random key. Hash a durable user id and bucket on the hash, so the same user always lands in the same group. This keeps membership fixed across sends and across reporting periods without storing a flag you might forget to honour.
3. Assign before eligibility, not after. Split the whole addressable audience first, then let normal targeting run inside both arms. If you pick the treated group by who qualified for a campaign and call the rest control, the two arms differ on the thing that drives conversion.

Pitfalls that quietly break randomisation:

* Re-rolling the random assignment each run, so users drift between arms and the holdout is no longer the same people.
* Excluding the holdout from a journey's entry criteria, so it is selected differently from the treated group.
* Letting another channel or team message the holdout, so it is not actually held out.
* Splitting on something correlated with behaviour (sign-up date, region, list source) instead of a clean random key.

## Maintaining the global holdout

A global holdout is a standing measurement, so its value depends on stability over time.

1. Fix membership at the start of the measurement period and keep it fixed. The same users stay held out for the whole window, which is what the stable random key buys you.
2. Read the gap over a quarter, not a week. The point of an always-on holdout is the slow signal in retention and revenue, which a few days cannot show. Compare cumulative outcomes for the two arms across the full period.
3. Let new users flow into both arms by the same key. Because assignment is a hash of the user id, anyone who joins is bucketed the same way automatically, so the holdout stays representative without manual top-ups.
4. Refresh deliberately, rarely, and never mid-read. Re-randomise only at a clean period boundary, and only when the population has shifted enough that the old split is no longer representative, or the withheld revenue on long-held users has become hard to justify. Document the date so before and after are not compared as if continuous.

## How to read the results

Once an experiment has run, the read is the same arithmetic whether it is a global holdout or a single campaign:

1. Compute the outcome rate in each arm on the same definition and window.
2. Take the difference, treatment minus control, as the absolute incremental rate. The detailed formulas for absolute lift, relative uplift, and incremental conversions are in [uplift and incrementality](/measurement/uplift-and-incrementality.md).
3. Attach an interval. The difference is an estimate with noise around it, so report the range, not just the point.
4. Judge significance, do not eyeball it. A gap is real only if it clears the interval; use the two-proportion test in [sample size and power](/measurement/sample-size-and-power.md).

## Geo experiments when individuals cannot be split

When you cannot randomise at the person level, for instance with brand or offline activity, randomise geographies instead: comparable regions are treated or held back and the difference is read against the controls. This is the workhorse of paid media incrementality, with open tooling such as Meta GeoLift and Google's Meridian, and the same logic applies to any channel that resists user level holdout.

The setup essentials, at a practical level:

1. Pick comparable regions. Choose treated and control geographies that tracked each other closely before the test, so the control is a credible stand-in for what the treated region would have done untreated.
2. Define a pre-period. Measure both sets over a baseline window before any change, to establish the normal relationship between them.
3. Run the change in the treated regions only, holding the controls untouched for the full test window.
4. Read the difference against controls. The lift is how far the treated regions diverged from where the pre-period relationship said they should be. The tooling handles the matching and inference: see GeoLift and Meridian below.

## What it costs and what it returns

Incrementality is the higher bar, so incremental return reads lower than last touch return, and adjusting expectations to that is part of the method, not a failure of it. Tests are not free: they take weeks, need adequate volume to reach significance, and cannot run on everything at once. Below a volume floor a holdout returns a wide interval around zero, which is the same constraint that governs all small sample reads here. See [volume thresholds](/measurement/volume-thresholds.md) and [uplift and incrementality](/measurement/uplift-and-incrementality.md).

## Related

* [Uplift and incrementality](/measurement/uplift-and-incrementality.md)
* [Sample size and power](/measurement/sample-size-and-power.md)
* [Attribution](/measurement/attribution.md)
* [Retention and LTV](/measurement/retention-and-ltv.md)
* [Volume thresholds](/measurement/volume-thresholds.md)

## Citations

[1] [EMARKETER, FAQ on incrementality](https://www.emarketer.com/content/faq-on-incrementality-how-prove-your-ads-actually-work-2026)
[2] [Meta GeoLift (open source)](https://github.com/facebookincubator/GeoLift)
[3] [Google Meridian](https://developers.google.com/meridian)
