---
type: Method
title: Holdouts and Control Groups
description: The always-on global holdout and per-campaign control group, why a randomised holdout is the only honest read of programme incrementality, and how it connects to geo experiments and uplift.
tags: [holdout, control-group, incrementality, experiment, geo-lift, causal]
timestamp: 2026-06-14T00:00:00Z
---

# The question only a control group answers

Attribution tells you which messages preceded a conversion. It cannot tell you which conversions would have happened anyway. Only withholding the message from a randomly chosen, otherwise identical group, and comparing outcomes, isolates the lift the programme actually caused. The difference between the treated group and the control is incrementality, and it is the only number that proves the programme created value rather than taking credit for it.

# The always-on global holdout

Hold back a small, randomly selected share of the addressable audience from all lifecycle messaging, continuously. The gap between the holdout and the mailed population, measured on conversion, retention, and revenue, is the incremental contribution of the entire programme. It is the single most valuable measurement a CRM team can run, because it answers the question executives rarely ask out loud: what would happen to revenue if we sent nothing? Keep it small, keep it random, and keep it permanent.

# Per-campaign control groups

For an individual send, sequence, or new automation, hold out a control from the eligible audience and measure the same outcomes. This reads the incremental effect of that specific intervention rather than the programme as a whole, and it is how a new idea earns its place before it is rolled out. The discipline is the same one direct mail has always used: the mailed file against a held back control. See [direct mail](/channels/direct-mail.md).

# Geo experiments when individuals cannot be split

When you cannot randomise at the person level, for instance with brand or offline activity, randomise geographies instead: comparable regions are treated or held back and the difference is read against the controls. This is the workhorse of paid media incrementality, with open tooling such as Meta GeoLift and Google's Meridian, and the same logic applies to any channel that resists user level holdout.

# What it costs and what it returns

Incrementality is the higher bar, so incremental return reads lower than last touch return, and adjusting expectations to that is part of the method, not a failure of it. Tests are not free: they take weeks, need adequate volume to reach significance, and cannot run on everything at once. Below a volume floor a holdout returns a wide interval around zero, which is the same constraint that governs all small sample reads here. See [volume thresholds](/measurement/volume-thresholds.md) and [uplift and incrementality](/measurement/uplift-and-incrementality.md).

# Related

* [Uplift and incrementality](/measurement/uplift-and-incrementality.md)
* [Attribution](/measurement/attribution.md)
* [Retention and LTV](/measurement/retention-and-ltv.md)
* [Volume thresholds](/measurement/volume-thresholds.md)

# Citations

[1] [EMARKETER, FAQ on incrementality](https://www.emarketer.com/content/faq-on-incrementality-how-prove-your-ads-actually-work-2026)
[2] [Meta GeoLift (open source)](https://github.com/facebookincubator/GeoLift)
[3] [Google Meridian](https://developers.google.com/meridian)
