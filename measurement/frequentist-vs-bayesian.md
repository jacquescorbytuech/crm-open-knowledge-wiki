---
type: Concept
title: Frequentist and Bayesian Testing
description: The two ways to read an A/B test, what each one actually tells you, the peeking trap that catches both, and which to reach for in a low-volume CRM programme.
tags: [statistics, bayesian, frequentist, ab-testing, significance, sequential]
timestamp: 2026-06-14T00:00:00Z
---

# Two ways to read the same test

A test gives you two conversion rates and the question of whether the difference is real. There are two schools of answer, and they answer subtly different questions. Knowing which one a tool is giving you prevents the most common misreading in marketing analytics: treating a p-value as the probability the variant is better, which it is not.

# The frequentist reading

The frequentist approach asks: if there were truly no difference, how surprising is the data I observed? The p-value is that surprise, and a result is called significant when it falls below a threshold, conventionally 5%. The confidence interval is the companion: a 95% interval is a range produced by a procedure that brackets the true effect 95% of the time over many repeats.

The discipline it demands is that you fix the sample size in advance and read the result once, at the end. Every method in [sample size and power](/measurement/sample-size-and-power.md) and [volume thresholds](/measurement/volume-thresholds.md) is frequentist. This is the default for good reason: it is well understood, needs no assumptions about prior belief, and the planning maths is simple.

What it does not give you is the thing stakeholders actually want to say.

> [!warning] A p-value is not the probability of winning
> A p-value of 0.03 does not mean a 97% chance the variant wins. It means the data would be this extreme only 3% of the time if the variant were identical, which is a more slippery statement and routinely misreported.

# The Bayesian reading

The Bayesian approach starts from a prior belief about the effect, updates it with the data, and returns a posterior: a full probability distribution over how large the effect is. From that you can read the statements people instinctively reach for, such as the probability that B beats A is 92%, or the expected loss from picking B is 0.1%. For a decision maker that framing is direct, and the expected loss version maps cleanly onto when it is safe to ship.

The cost is the prior. A weak or default prior gives results close to the frequentist ones; a strong prior pulls the answer toward it, which is powerful when you genuinely have prior knowledge and misleading when you smuggle in a guess. The other cost is that the machinery is heavier and fewer practitioners can explain it, so it is easier to trust a number nobody in the room can defend.

# The peeking trap that catches both

The single most common way to get a false win is to watch a running test and stop the moment it crosses significance. Doing this inflates the false positive rate far above the nominal 5%, because you have given the noise many chances to cross the line. A fixed-sample frequentist test is only valid if you read it once; repeatedly peeking quietly breaks it. Evan Miller's [How Not To Run an A/B Test](https://www.evanmiller.org/how-not-to-run-an-ab-test.html) is the canonical explanation.

Naive Bayesian dashboards are not automatically immune: stopping as soon as probability to be best crosses 95% has the same problem unless the method was designed for it. The honest fixes are to fix the sample in advance, or to use a method built for repeated looks: sequential testing, always-valid p-values, or a properly specified Bayesian decision rule with a loss threshold.

# Which to reach for in CRM

* **Default to frequentist with a fixed sample.** It is the lingua franca, the planning is simple, and it forces the volume discipline a small list most needs. Size the test, run it, read it once. See [test rigorously](/principles/test-rigorously.md).
* **Reach for Bayesian when the framing earns its keep.** When you must communicate to non-statisticians, probability to be best and expected loss are far easier to act on than a p-value. The expected-loss rule also gives a principled way to ship a marginal winner rather than declaring no result.
* **Bayesian shrinkage helps when you run many small tests.** A hierarchical model pools information across campaigns and pulls extreme small-sample estimates toward the group average, which damps the false dramatic wins a low-volume programme throws off. This is one of the few places it materially beats the frequentist default for a typical sender.
* **Either way, do not peek without a method that allows it.** The choice of school does not rescue you from optional stopping; only the right procedure does.

The deeper point sits underneath both: every method here hands you a distribution, not a verdict, and below a volume floor that distribution is a wide band around zero whichever school drew it. See [volume thresholds](/measurement/volume-thresholds.md).

# Related

* [Sample size and power](/measurement/sample-size-and-power.md)
* [Volume thresholds](/measurement/volume-thresholds.md)
* [Holdouts and control groups](/measurement/holdouts-and-control-groups.md)
* [Uplift and incrementality](/measurement/uplift-and-incrementality.md)
* [Test rigorously](/principles/test-rigorously.md)

# Citations

[1] [Evan Miller, How Not To Run An A/B Test (the peeking problem)](https://www.evanmiller.org/how-not-to-run-an-ab-test.html)
[2] [Evan Miller, Sample size calculator](https://www.evanmiller.org/ab-testing/sample-size.html)
[3] [Kohavi, Tang & Xu, Trustworthy Online Controlled Experiments](https://experimentguide.com/)
[4] [Stucchio, Bayesian A/B testing at VWO (expected loss decision rule)](https://vwo.com/downloads/VWO_SmartStats_technical_whitepaper.pdf)
