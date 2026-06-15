---
type: Method
title: Sample Size and Power
description: The two proportion z-test for planning experiments, how to turn a required sample into a test duration, and the companion test for reading significance once the experiment has run.
tags: [statistics, power, sample-size, z-test, experiments]
timestamp: 2026-06-14T00:00:00Z
---

## Why it belongs with sizing

A sizing model without a sample size estimate is incomplete. It tells you what you could achieve, not whether you can detect it. A compelling opportunity that needs sixteen weeks of test time to confirm may be a worse use of resources than a faster test on a smaller prize.

The reason this matters more than the formula does: the sample required to detect an effect grows explosively as the effect shrinks, so sub-percent effects like platform intermediation sit in a zone where the required n is infeasible for most teams. The real use of sizing is not to plan the test you will run, it is to decide in advance which tests are not worth running. Read the formula below as a filter, not a recipe.

## The standard approach

Once you have decided the test is worth running, the standard form is a two proportion z-test, one sided, 80% power, 95% confidence:

```
Users per variant = (Z_a + Z_b)^2 x (p1(1-p1) + p2(1-p2)) / (p2 - p1)^2
```

where `Z_a = 1.6449` and `Z_b = 0.8416`, giving `(Z_a + Z_b)^2` of about 6.18. Then:

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

## The hard truth in the numbers

The required n grows fast as the effect you want to detect shrinks. Platform intermediation effects are usually small, in the low single percent or below, which is exactly where the sample requirement explodes. The cleaner techniques used to read intermediation, difference in differences in particular, demand more than a simple two proportion test because they difference several noisy quantities, so treat this formula as the optimistic floor. See [volume thresholds](/measurement/volume-thresholds.md).

## Related

* [Volume thresholds](/measurement/volume-thresholds.md)
* [Impact sizing](/measurement/impact-sizing.md)
* [Test rigorously](/principles/test-rigorously.md)

## Citations

[1] [Kohavi, Tang & Xu, Trustworthy Online Controlled Experiments (statistical power and sample size)](https://experimentguide.com/)
