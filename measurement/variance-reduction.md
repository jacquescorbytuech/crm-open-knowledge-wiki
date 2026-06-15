---
type: Method
title: Variance Reduction and Sequential Testing
description: The two standard ways to get more out of the volume you already have, CUPED variance reduction using pre-experiment data and sequential testing that lets you monitor without inflating false positives, and the limit that neither repeals the volume floor.
tags: [statistics, cuped, variance-reduction, sequential, always-valid, power, experiments]
timestamp: 2026-06-15T00:00:00Z
---

## Why it belongs with sizing

[Volume thresholds](/measurement/volume-thresholds.md) and [sample size and power](/measurement/sample-size-and-power.md) keep delivering the same deflating verdict: a small list cannot read a small effect, so most senders are told to chase bigger swings, pool, or lengthen. That advice is sound but incomplete, because it treats the noise as fixed. Variance reduction and sequential testing lower the requirement instead of working around it. Variance reduction cuts the noise for a given sample; sequential testing lets you stop as soon as the evidence arrives rather than waiting out a fixed horizon. Neither manufactures signal, and neither repeals the floor. They lower it, sometimes enough to make a test that was theatre into one worth running.

## Variance reduction (CUPED)

The reason a test needs volume is the variance of the estimate: the lift is a difference of two noisy rates, and the interval around it shrinks only as the sample grows. CUPED, controlled experiment using pre-experiment data, attacks the variance directly. If you have a pre-experiment metric correlated with the outcome, each user's spend or activity in the period *before* the test, you can subtract the part of the result that the pre-period already explains, leaving a cleaner estimate of the effect the test actually caused.

The gain is not marginal. The variance reduction is roughly the square of the correlation between the pre-period covariate and the outcome, so a covariate correlated at 0.6 removes about a third of the variance, equivalent to running the test on a third more users for free. This is a particularly good fit for a CRM programme, because the asset it already holds, a rich per-customer history on a known, identified base, is exactly the correlated pre-period data CUPED needs. The requirements are real but modest: the covariate must be measured on the same users before treatment, must not itself be affected by the test, and the stronger its correlation with the outcome the larger the gain.

## Sequential testing

The [peeking trap](/measurement/frequentist-vs-bayesian.md) is why a fixed-horizon test can be read only once: watch it run and stop the moment it crosses significance, and you inflate the false-positive rate far above the nominal 5%, because noise was given many chances to cross the line. Sequential methods are built to remove that constraint. Always-valid p-values, group-sequential designs, and the mixture sequential probability ratio tests behind several commercial stats engines are constructed so the error rate holds *no matter how often you look*, which means you can monitor a running test continuously and stop as soon as there is enough evidence, or enough evidence of no effect, to decide.

The trade is explicit: to buy the right to peek, a sequential test is slightly more conservative than a fixed test at any given sample size, so a winner that would have cleared a fixed horizon takes marginally longer to confirm under sequential rules. The technique earns that cost back when stopping early has real value, cutting the withheld revenue of a [holdout](/measurement/holdouts-and-control-groups.md) the moment the read is clear, or killing a losing variant before it has run its full course. If you would have run to a fixed sample and read it once regardless, the plain fixed test is the more powerful choice.

## What it cannot do

Variance reduction needs a pre-period covariate genuinely correlated with the outcome, and gives little when none exists. Sequential testing needs the discipline to use a method designed for repeated looks rather than peeking at a naive dashboard and calling it sequential. And a list that cannot detect a 1% effect with the plain test will not detect it by halving the variance or by watching more carefully; it will detect a 1.4% effect instead of a 2% one. Use these to make a borderline test viable, not to pretend a list has volume it does not. The constraint in [volume thresholds](/measurement/volume-thresholds.md) still governs; these only ease it.

## Related

* [Sample size and power](/measurement/sample-size-and-power.md)
* [Volume thresholds](/measurement/volume-thresholds.md)
* [Frequentist and Bayesian testing](/measurement/frequentist-vs-bayesian.md)
* [Holdouts and control groups](/measurement/holdouts-and-control-groups.md)
* [Test rigorously](/principles/test-rigorously.md)

## Citations

[1] [Deng, Xu, Kohavi & Walker, Improving the Sensitivity of Online Controlled Experiments by Utilizing Pre-Experiment Data (CUPED), WSDM 2013](https://exp-platform.com/Documents/2013-02-CUPED-ImprovingSensitivityOfControlledExperiments.pdf)
[2] [Johari, Pekelis, Koomen & Walsh, Always Valid Inference: Continuous Monitoring of A/B Tests](https://arxiv.org/abs/1512.04922)
[3] [Kohavi, Tang & Xu, Trustworthy Online Controlled Experiments](https://experimentguide.com/)
