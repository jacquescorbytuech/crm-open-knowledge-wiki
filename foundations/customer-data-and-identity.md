---
type: Playbook
title: Customer Data and Identity
description: The data foundation a CRM programme runs on, how first-party data is captured, unified into a single customer view, and resolved to one identity across devices and channels, and how the CRM, the CDP, and the data warehouse divide the work.
tags: [customer-data, cdp, identity-resolution, first-party-data, single-customer-view, data]
timestamp: 2026-06-14T00:00:00Z
---

# Why data is the foundation

Every other operation in a lifecycle programme, segmentation, automation, personalisation, measurement, is downstream of the customer data underneath it. A programme cannot target a stage it cannot see, personalise a field it has not captured, or measure a customer it cannot identify across sessions. Getting the data layer right is not a precondition for sophistication; it is the thing sophistication is made of.

# The kinds of data, by who gives it and how

* **Zero-party data** is what a customer deliberately and proactively shares: stated preferences, survey and quiz answers, a preference-centre selection. It is the cleanest and most durable signal because it was given, not inferred.
* **First-party data** is collected from a customer's direct interactions with your own properties: purchases, site and app behaviour, email engagement, support contacts.
* **Third-party data** is bought from outside aggregators. It is fading as browsers phase out third-party cookies and regulators tighten, and it is not a foundation to build on.

Build the programme on zero- and first-party data, and treat the decline of third-party data as a reason to capture more of your own. See [consent and preferences](/foundations/consent-and-preferences.md) for capturing it lawfully.

# The single customer view

A single customer view is one unified profile per person, assembled from every source: the order history from commerce, the events from the site and app, the engagement from the [channels](/channels/), the tickets from support. Without it, each system holds a partial customer and the programme contradicts itself, mailing a discount to someone who just paid full price, or onboarding a customer who has been active for a year.

# Identity resolution

Identity resolution is the work of deciding that the anonymous browser, the app login, the email address, and the loyalty number are all the same person, and stitching their activity into one profile. It is what turns scattered identifiers into the single customer view. Done well, anonymous behaviour before signup attaches to the customer once they identify themselves; done badly, the same person appears as several, and frequency caps, suppression, and measurement all leak.

# CRM, CDP, and warehouse

Three systems are easy to confuse, and most stacks run more than one.

* A **CRM** manages known relationships and the interactions with them. It is built around the identified customer and the people who act on that relationship.
* A **CDP (customer data platform)** ingests data from every source, resolves identity, and maintains the unified, activation-ready profile that the channels and decisioning read from.
* A **data warehouse** is built for analysis and storage at scale, not for real-time activation.

The distinction that matters operationally: a warehouse is built for analysis, a CDP is built for activation. Which combination you need follows from the [ESP and tooling choices](/foundations/esp-selection.md), not the reverse.

# Hygiene and governance

Data decays. Maintain it: deduplicate profiles, suppress hard bounces immediately, decay or refresh stale attributes, and hold a documented lawful basis for every contact. A unified profile that is wrong is worse than no profile, because it fires confident, specific, incorrect messages. See [segmentation and data](/foundations/segmentation-and-data.md) for the operational hygiene and [legislation and compliance](/references/legislation-and-compliance.md) for the obligations.

# The decisioning link

Unified, training-ready customer data is also the prerequisite for the AI personalisation and decisioning that platforms and vendors now sell: the data quality underneath usually limits the outcome more than the tooling does. This is treated in [decisioning and personalisation](/foundations/decisioning-and-personalisation.md); for the foundation, the point is simpler: capture and unify your first-party data well, and the advanced options stay open.

# Related

* [Segmentation and data](/foundations/segmentation-and-data.md)
* [Segmentation models](/foundations/segmentation-models.md)
* [Consent and preferences](/foundations/consent-and-preferences.md)
* [Decisioning and personalisation](/foundations/decisioning-and-personalisation.md)
* [Legislation and compliance](/references/legislation-and-compliance.md)

# Citations

[1] [Customer data platform (David Raab, "persistent, unified customer view")](https://en.wikipedia.org/wiki/Customer_data_platform)
[2] [Tealium, what is a CDP (a warehouse is built for analysis, a CDP for activation)](https://tealium.com/resource/fundamentals/what-is-a-cdp/)
[3] [Twilio, identity resolution explained](https://www.twilio.com/en-us/blog/insights/identity-resolution)
[4] [Adobe Experience League, identity stitching across anonymous and authenticated profiles](https://experienceleague.adobe.com/en/docs/journey-optimizer-learn/tutorial-on-identity-stitching-in-aep/introduction)
[5] [Twilio, zero-party vs first-party data](https://www.twilio.com/en-us/blog/insights/data/first-vs-zero-party-data)
[6] [Twilio, first-party vs third-party data and the third-party cookie phase-out](https://www.twilio.com/en-us/blog/insights/data/first-vs-third-party-data)
[7] [Forrester, Google's third-party cookie deprecation](https://www.forrester.com/blogs/google-makes-good-on-third-party-cookie-deprecation/)
