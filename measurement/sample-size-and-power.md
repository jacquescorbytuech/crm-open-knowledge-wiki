---
type: Method
title: Sample Size and Power
description: The two proportion z-test for planning experiments, and how to turn a required sample into a test duration.
tags: [statistics, power, sample-size, z-test, experiments]
timestamp: 2026-06-14T00:00:00Z
---

# Why it belongs with sizing

A sizing model without a sample size estimate is incomplete. It tells you what you could achieve, not whether you can detect it. A compelling opportunity that needs sixteen weeks of test time to confirm may be a worse use of resources than a faster test on a smaller prize.

# The standard approach

A two proportion z-test, one sided, 80% power, 95% confidence:

```
Users per variant = (Z_a + Z_b)^2 x (p1(1-p1) + p2(1-p2)) / (p2 - p1)^2
```

where `Z_a = 1.6449` and `Z_b = 0.8416`, giving `(Z_a + Z_b)^2` of about 6.18. Then:

```
Test duration = (Users per variant x 2) / Users entering per week
```

# The hard truth this surfaces

The required n grows fast as the effect you want to detect shrinks. Platform intermediation effects are usually small, in the low single percent or below, which is exactly where the sample requirement explodes. The cleaner techniques used to read intermediation, difference in differences in particular, demand more than a simple two proportion test because they difference several noisy quantities, so treat this formula as the optimistic floor. See [volume thresholds](/measurement/volume-thresholds.md).

# Related

* [Volume thresholds](/measurement/volume-thresholds.md)
* [Impact sizing](/measurement/impact-sizing.md)
* [Test rigorously](/principles/test-rigorously.md)

# Citations

[1] [Kohavi, Tang & Xu, Trustworthy Online Controlled Experiments (statistical power and sample size)](https://experimentguide.com/)
