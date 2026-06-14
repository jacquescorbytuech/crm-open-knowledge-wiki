---
type: Playbook
title: Segmentation and Data
description: The operational craft of segmentation, dynamic versus static segments, overlap, data hygiene, personalisation and merge tags, and privacy, with the segmentation models and the wider data layer treated separately.
tags: [segmentation, data, personalisation, privacy, merge-tags, hygiene]
timestamp: 2026-06-14T00:00:00Z
---

# What this covers

This is the operational how of segmentation: keeping segments correct, current, and clean. The models that decide how you divide an audience in the first place, RFM, value, behavioural, propensity, live in [segmentation models](/foundations/segmentation-models.md), and the data layer underneath all of it, capture, identity, and the single customer view, lives in [customer data and identity](/foundations/customer-data-and-identity.md).

# Segment types

A dynamic segment updates automatically as subscriber data changes (for example, opened in the last 30 days). A static segment has fixed membership set at creation. Prefer dynamic segments for engagement-based targeting, because they keep themselves current. Confirm whether segments overlap before combining them: free users and users who have not completed onboarding are not mutually exclusive, and adding them double-counts the audience.

# The cost of segmentation

Segmentation trades statistical power for relevance. Below list sizes in the low thousands the trade is usually a loss, because each segment becomes too small to test or to send to reliably. Targeted segments do earn their keep when they are large enough to send to, consistently outperforming undifferentiated broadcasts on engagement and revenue per recipient. See [segmentation has real costs](/principles/segmentation-has-costs.md) and [volume thresholds](/measurement/volume-thresholds.md).

# Data hygiene

Auto-suppress hard bounces immediately and never re-send to them. Maintain a suppression list of unsubscribes, complaints, and hard bounces that must never receive mail. Sunset subscriptions that have gone quiet, because dormant contacts drag reach for the active ones. See [engagement is the new deliverability](/principles/engagement-is-deliverability.md).

# Personalisation and merge tags

A merge tag is a placeholder replaced with subscriber-specific data at send time. Dynamic content blocks display differently based on subscriber data. Personalisation is a real lever, but it depends on clean data: a merge tag firing a blank or a wrong value is worse than no personalisation at all, which is why the [data layer](/foundations/customer-data-and-identity.md) comes first.

# Privacy

Hold a documented lawful basis for every contact, keep records of how and when consent was obtained, and honour opt-outs immediately. See [legislation and compliance](/references/legislation-and-compliance.md).

# Related

* [Segmentation models](/foundations/segmentation-models.md)
* [Customer data and identity](/foundations/customer-data-and-identity.md)
* [Segmentation has real costs](/principles/segmentation-has-costs.md)
* [Legislation and compliance](/references/legislation-and-compliance.md)
* [Consent and preferences](/foundations/consent-and-preferences.md)

# Citations

[1] [Klaviyo, ecommerce benchmarks (targeted segments outperform broad sends on engagement and revenue per recipient)](https://www.klaviyo.com/marketing-resources/ecommerce-benchmarks)
