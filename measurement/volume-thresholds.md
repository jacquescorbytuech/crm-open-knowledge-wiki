---
type: Method
title: Volume Thresholds
description: The sends per cell needed to detect a given relative shift at a 2% email click baseline, how to read it across channels whose base rates differ, and how a team should use that table to decide which tests are worth running.
tags: [statistics, power, volume, testing, measurement]
timestamp: 2026-06-11T00:00:00Z
---

## The floor table

Anchored on a 2% campaign click rate (a defensible round number for the typical B2C send per the 2026 Klaviyo and Mailchimp benchmarks), at 95% confidence and 80% power, the sends per cell needed to detect a given relative shift in the easiest design:

| Relative shift | Absolute change | Sends per cell | What it usually represents |
| --- | --- | --- | --- |
| 20% | +0.40pp | ~21,000 | Major creative pivot, exceptional |
| 10% | +0.20pp | ~80,000 | Strong A/B win, well run programme |
| 5% | +0.10pp | ~315,000 | Typical mature programme win |
| 3% | +0.06pp | ~870,000 | Clean intermediation effect on the affected cohort |
| 2% | +0.04pp | ~1,940,000 | Low end intermediation effect |
| 1% | +0.02pp | ~7,720,000 | Platform internal A/B territory |
| 0.5% | +0.01pp | ~30,800,000 | Meta scale notification optimisation |

These are floor numbers for the easiest design. More complex designs raise the requirement further, and splitting by cohort, segment, or channel multiplies the cells, so the requirement compounds.

## Reading the table for another channel

The 2% anchor is an email click rate, and the table is calibrated to it. The method does not change by channel, but the numbers do, because the channel-specific input that drives them is the baseline rate the test moves around. A channel measured on a higher base rate, an in-app prompt or an RCS card acted on in session, needs proportionally fewer observations to detect the same relative shift; one read on a lower base rate, a push tap-through, needs more. To size a test on any channel, take your own measured baseline for that channel in place of the 2% here and run it through the formula in [sample size and power](/measurement/sample-size-and-power.md). The table's lesson, that small relative effects need very large samples, holds wherever the baseline sits.

## How to use this table

Read the table before you design a test, not after it fails to reach significance.

* **Size the test to a realistic win.** Most genuine A/B wins are in the 5 to 10% range, which needs roughly 80,000 to 315,000 sends per cell. If a cell cannot reach that, the test cannot reliably detect a normal win, so do not run it as a test, ship the better-reasoned option and move on.
* **Do not over-segment.** Every split shrinks the cells toward the noise floor. A smaller list buys relevance with statistical power, so reserve segmentation for where the relevance gain is large. See [segmentation has real costs](/principles/segmentation-has-costs.md).
* **Pool and lengthen.** Combine comparable campaigns and widen the window to accumulate the volume a single send cannot reach.
* **Chase bigger swings.** A small list can only detect large effects, so spend test budget on changes big enough to clear the floor (a creative pivot, a new offer), not on subject-line micro-tweaks it can never read.
* **Lean on holdouts for the big questions.** Programme-level incrementality (does this automation pay at all) is a large effect and is readable at far lower volume than a per-campaign click delta. See [holdouts and control groups](/measurement/holdouts-and-control-groups.md).

## Related

* [Sample size and power](/measurement/sample-size-and-power.md)
* [Holdouts and control groups](/measurement/holdouts-and-control-groups.md)
* [Segmentation has real costs](/principles/segmentation-has-costs.md)
* [Impact sizing](/measurement/impact-sizing.md)

## Citations

[1] [Klaviyo, ecommerce email benchmarks (typical B2C click-rate baseline)](https://www.klaviyo.com/marketing-resources/ecommerce-benchmarks)
[2] [Kohavi et al., Trustworthy Online Controlled Experiments (statistical power and sample size for A/B tests)](https://experimentguide.com/)
