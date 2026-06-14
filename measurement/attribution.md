---
type: Concept
title: Attribution
description: The three families of answer to what drove a result, last-click and multi-touch attribution, marketing mix modelling, and incrementality, and why they answer different questions rather than competing for one.
tags: [attribution, mta, mmm, incrementality, measurement, cross-channel]
timestamp: 2026-06-14T00:00:00Z
---

# What attribution is for

Attribution assigns credit for an outcome to the things that may have caused it. The mistake that organises most attribution debates is treating it as one question with competing answers. It is three questions, and the methods below each answer one of them well and the others badly.

# Last-click and multi-touch

Last-click gives all credit to the final touch. It is simple, available, and systematically wrong in one direction: it over credits whatever sat closest to a conversion that was often already going to happen, and it credits nothing to the demand built earlier. Multi-touch attribution (MTA) spreads credit across the observed journey and is sharper for near real time, within channel optimisation, but it only sees the trackable slice and that slice has been eroded by cookie deprecation, Apple's App Tracking Transparency, and the walled gardens. Both are bottom up and correlational. Neither establishes cause.

# Marketing mix modelling

MMM works top down, regressing outcomes on aggregate, time series spend and external factors. It values offline and brand alongside digital, and it survives the privacy decay that breaks MTA, because it needs no user level tracking. The costs are that it is data hungry, needs real expertise to build and validate, and smooths over short term and tactical effects. It answers how to allocate budget across the portfolio, not which message to send next.

# Incrementality as the referee

Only a controlled experiment, treatment against a randomised holdout or geo control, measures causation directly. Incrementality does not replace attribution and MMM; it calibrates them, acting as the ground truth a disagreement is resolved against. When last touch says one number and MMM says another, a clean lift test is the tiebreaker. See [holdouts and control groups](/measurement/holdouts-and-control-groups.md).

# What this means for a lifecycle programme

Owned channel attribution looks easy because the click is yours to track, which is exactly the trap: a tracked click is not proof the send caused the outcome. Build the read on the authenticated cohort, where identity is deterministic and you can follow channel to destination and destination to outcome, and anchor it on a holdout rather than on the click. The destination conversion frame is also the one that survives platform intermediation and the agentic shock. See [measuring intermediation](/measurement/measuring-intermediation.md).

# Related

* [Holdouts and control groups](/measurement/holdouts-and-control-groups.md)
* [Core metrics](/measurement/core-metrics.md)
* [Measuring intermediation](/measurement/measuring-intermediation.md)
* [Uplift and incrementality](/measurement/uplift-and-incrementality.md)

# Citations

[1] [EMARKETER, FAQ on incrementality](https://www.emarketer.com/content/faq-on-incrementality-how-prove-your-ads-actually-work-2026)
[2] [Google Meridian, open source marketing mix modelling](https://developers.google.com/meridian)
