---
type: Method
title: Sample Size and Power
description: The two proportion z-test for planning experiments, how to turn a required sample into a test duration, and the companion test for reading significance once the experiment has run.
tags: [statistics, power, sample-size, z-test, experiments]
generated:
  by: human:jacquescorbytuech
  at: 2026-06-14T00:00:00Z
sources:
  - id: kohavi-tang-xu-trustworthy-online-controlled-experiments
    resource: https://experimentguide.com/
    title: "Kohavi, Tang & Xu, Trustworthy Online Controlled Experiments (statistical power and sample size)"
---

## Why it belongs with sizing

A sizing model without a sample size estimate is incomplete. It tells you what you could achieve, not whether you can detect it. A compelling opportunity that needs sixteen weeks of test time to confirm may be a worse use of resources than a faster test on a smaller prize.

The reason this matters more than the formula does: as the effect shrinks, the sample required to detect it grows explosively, leaving sub-percent effects like platform intermediation in a zone where the required n is infeasible for most teams. The main use of sizing is ruling tests out before anyone builds them, rather than planning the test you will run.

## The standard approach

Once you have decided the test is worth running, the standard form is a two proportion z-test, two sided, 80% power, 95% confidence:

```
Users per variant = (Z_a + Z_b)^2 x (p1(1-p1) + p2(1-p2)) / (p2 - p1)^2
```

where `Z_a = 1.96` (two sided, 95% confidence) and `Z_b = 0.8416` (80% power), giving `(Z_a + Z_b)^2` of about 7.85. Two sided is the right default, both because you do not know in advance which variant wins and because it keeps the planning test consistent with the reading test below, which also uses 1.96. Then:

```
Test duration = (Users per variant x 2) / Users entering per week
```

You do not have to compute this by hand. Evan Miller's [sample size calculator](https://www.evanmiller.org/ab-testing/sample-size.html) does the proportion case interactively and is the quickest way to sanity check a plan before building a test; the page also explains why fixing the sample in advance, rather than stopping when the result looks good, is what keeps the false positive rate honest. See [frequentist and Bayesian testing](/measurement/frequentist-vs-bayesian.md) for that distinction.

## Reading the result once it has run

Planning sizes the test; reading it asks whether the gap you observed is real. This is the test the [holdout](/measurement/holdouts-and-control-groups.md), [uplift](/measurement/uplift-and-incrementality.md), and incrementality reads refer back to. For two observed proportions `p1` and `p2` over `n1` and `n2` users, the difference `p2 - p1` has a standard error:

```
SE = sqrt( p1(1-p1)/n1 + p2(1-p2)/n2 )
```

The 95% confidence interval on the difference is `(p2 - p1) ± 1.96 x SE`. The effect is significant at that level when the interval excludes zero, equivalently when `|p2 - p1| / SE` exceeds 1.96. Report the interval, not just the point estimate: it is the range the other measurement pages mean by "attach an interval." Below the [volume floor](/measurement/volume-thresholds.md) that interval is a wide band around zero whatever the point looks like, which is the frequentist reason small lists cannot read small effects. The Bayesian alternative reading is in [frequentist and Bayesian testing](/measurement/frequentist-vs-bayesian.md).

## Why small effects need huge samples

The required n grows fast as the effect you want to detect shrinks. Platform intermediation effects are usually small, in the low single percent or below, which is exactly where the sample requirement explodes. The cleaner techniques used to read intermediation, difference in differences in particular, demand more than a simple two proportion test because they difference several noisy quantities, which makes this formula the optimistic floor. See [volume thresholds](/measurement/volume-thresholds.md).

## Related

* [Volume thresholds](/measurement/volume-thresholds.md)
* [Variance reduction and sequential testing](/measurement/variance-reduction.md)
* [Impact sizing](/measurement/impact-sizing.md)
* [Test rigorously](/principles/test-rigorously.md)
