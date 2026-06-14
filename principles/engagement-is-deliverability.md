---
type: Principle
title: Engagement is the new deliverability
description: Providers treat engagement as a property of the sender, so weak engagement from a dormant list drags placement for the engaged part of the list too.
tags: [principle, deliverability, engagement, reputation]
timestamp: 2026-06-14T00:00:00Z
---

# Stance

Sender level engagement is the currency of inbox placement. Consistently weak engagement from a dormant segment drags down placement for the engaged segment too, because the provider's classifier treats engagement as a property of the sender, not just the recipient.

# What changed

This was always partly true. What changed is that the major providers codified it. From February 2024 the Gmail and Yahoo bulk sender rules made authentication, one click unsubscribe, and a spam complaint ceiling of 0.3% (0.1% recommended) non negotiable, with Microsoft following in 2025 and Gmail escalating to rejection in November 2025. Above the explicit thresholds sits a category aware retrieval gate driven by quality and engagement: a sender can pass SPF, DKIM, and DMARC and still never be retrieved into intelligent views, search, or assistant answers. See [platform interventions](/references/platform-interventions.md).

# Which engagement this is

The engagement that moves placement is the one the provider observes directly, not the opens and clicks you measure. The principle holds on the provider's sense: it is the behaviour the provider sees, not your reported open rate, that decides placement. The full distinction between the two, and why your own metrics are the wrong instrument for it, is in [email metrics are directional](/principles/metrics-are-directional.md).

# Consequences

* The set and forget approach to disengaged segments is now actively expensive.
* List hygiene and frequency discipline are deliverability inputs, not nice to haves.
* The cost of sending to dead weight is the engagement cohort drag on active sends plus the accelerated loss of the dormant cohort to provider initiated unsubscribe.

# Related

* [Deliverability](/foundations/deliverability.md)
* [Platform interventions](/references/platform-interventions.md)
* [List quality over size](/principles/list-quality-over-size.md)

# Citations

[1] [Word to the Wise, Deliveries and Opens and Clicks](https://www.wordtothewise.com/2024/06/deliveries-and-opens-and-clicks/)
