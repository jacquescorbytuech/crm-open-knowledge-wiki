---
type: Method
title: Measuring Intermediation
description: How to read the effect of a platform change (a new spam policy, a summarisation feature, a tab re-sort) on your own sends without platform cooperation, and the limits of each method.
tags: [measurement, did, ablation, cohort, platform-changes]
timestamp: 2026-06-11T00:00:00Z
---

## The problem

When a platform changes how it filters, ranks, or summarises mail (the dated changes in [platform interventions](/references/platform-interventions.md)), it does not report what it did to your sends. The methods below estimate the effect from your own data. They are channel-agnostic in shape and channel-specific in detail, and none reads the wording layer, what a summary kept versus what you wrote, directly.

Before reaching for any of them: most senders should not attempt to read intermediation effects at all. The methods need volume far above typical thresholds, hundreds of thousands of sends per cell and often millions, so below that floor they return wide intervals around zero whatever the platform actually did. None of this applies to you unless you operate at platform scale. Below that floor the useful output is the diagnostic, not the measurement: intermediation is bending your numbers and you cannot cleanly say by how much, so treat them with that suspicion instead of spending effort quantifying the distortion.

## The volume floor, concretely

> [!warning] Below the volume floor this kit reads zero
> Reading these effects needs hundreds of thousands of sends per cell, often millions, which is far above what a typical sender has. Below the volume threshold the kit gives wide confidence intervals around zero. Take the diagnostic and leave the methodology.

See [volume thresholds](/measurement/volume-thresholds.md).

## The shared probes

* **Difference in differences around platform release dates.** Pick a cohort the intervention affected and one it did not, compute the change in your metric across the known release date for each, and difference the two. The estimator nets out whatever else moved that quarter. Caveats: parallel trends is an assumption, not a fact (Apple heavy and Android heavy cohorts differ); your own copy shifted around the same date because everyone read the same trade press; and eligibility is not treatment, so you are reading an intent to treat effect diluted by an unmeasured compliance rate. The iOS 18.3 news disablement is the cleanest example.
* **Sender side ablation.** Hold the audience cohort constant and vary what you control (interruption level, subject structure, preheader, HTML weight, image to text ratio). The delta between two variants should be larger on the eligible cohort than the non eligible one if the layer you suspect is doing the work. The cleanest internal experiment, limited by power and by imperfect cohort identification.
* **Cohort comparison by platform eligibility.** Compare engagement across device or mailbox cohorts. The weakest probe alone, because the cohorts are not random samples of each other and selection bias swamps the signal. Use as a sanity check, not a primary estimate.
* **Transactional sends as a within user control.** Do not compare promotional to transactional ratios directly: they are not comparable. The version that survives uses transactional engagement only as a within user control in a difference in differences around a release date, to confirm general willingness to engage did not crater for an unrelated reason. A tie breaker, not a method.

## Channel specifics

For push, add interruption level ablation, bundle composition tests, confirmed delivery as a Focus and silent kill diagnostic (not a summarisation signal), time to session distribution, and MMP link conversion decomposition. For email, add Postmaster Tools and SNDS monitoring, Mozilla/5.0 segmentation for MPP, inbox provider cohort comparison, seed list tab placement testing (directional only), one click unsubscribe timing, DMARC aggregate reports, and reply rate.

## What survives

Shift measurement weight off channel-surface click-through and onto channel-to-destination conversion and destination-to-target-event conversion. The first is partly mediated by the platform; the second is not. Build the framework around the authenticated cohort, where attribution is deterministic. The destination-conversion frame is the one that holds up as more of the inbox and lock screen is summarised or acted on by assistants.

## Related

* [Platform interventions](/references/platform-interventions.md)
* [Volume thresholds](/measurement/volume-thresholds.md)
* [Holdouts and control groups](/measurement/holdouts-and-control-groups.md)
* [Attribution](/measurement/attribution.md)

## Citations

[1] [Roth et al., What's Trending in Difference-in-Differences (2023)](https://arxiv.org/abs/2201.01194)
[2] [Google, email sender guidelines (Postmaster Tools diagnostics)](https://support.google.com/a/answer/81126)
