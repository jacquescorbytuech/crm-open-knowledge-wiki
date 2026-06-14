---
type: Principle
title: Test constantly, but test rigorously
description: Most email A/B tests run on samples too small to produce reliable conclusions. Call this out when relevant.
tags: [principle, testing, statistics, power]
timestamp: 2026-06-14T00:00:00Z
---

# Stance

Test constantly, but test rigorously. Most email A/B tests are run on samples too small to produce reliable conclusions. Say so when it is true.

# The volume reality

A 2% campaign click rate baseline needs roughly 80,000 sends per cell to detect a 10% relative shift at 95% confidence and 80% power, and around 315,000 to detect a 5% shift. The platform intermediation effects people argue about are usually smaller than that. If your list is in the tens of thousands or low six figures, most elaborate tests give you a wide confidence interval around zero. See [volume thresholds](/measurement/volume-thresholds.md) and [sample size and power](/measurement/sample-size-and-power.md).

# What rigour requires

* A real holdout, and the discipline to trust it over the dashboard.
* Comfort with a distribution rather than a verdict. This is the harder half, and it is a hiring and culture problem, not a software one.

# Related

* [Sample size and power](/measurement/sample-size-and-power.md)
* [Uplift and incrementality](/measurement/uplift-and-incrementality.md)
