---
type: Playbook
title: Customer Data and Identity
description: The data foundation a CRM programme runs on, with the practical steps to capture first-party data, resolve identity with deterministic matching rules, consolidate a single customer view with a golden record, run a decay routine, and evaluate a CDP, and how the CRM, the CDP, and the data warehouse divide the work.
tags: [customer-data, cdp, identity-resolution, first-party-data, single-customer-view, golden-record, data-quality, data]
timestamp: 2026-06-14T00:00:00Z
---

# Why data is the foundation

Every other operation in a lifecycle programme, segmentation, automation, personalisation, measurement, is downstream of the customer data underneath it. A programme cannot target a stage it cannot see, personalise a field it has not captured, or measure a customer it cannot identify across sessions. Getting the data layer right is not a precondition for sophistication; it is the thing sophistication is made of.

# The kinds of data, by who gives it and how

* **Zero-party data** is what a customer deliberately and proactively shares: stated preferences, survey and quiz answers, a preference-centre selection. It is the cleanest and most durable signal because it was given, not inferred.
* **First-party data** is collected from a customer's direct interactions with your own properties: purchases, site and app behaviour, email engagement, support contacts.
* **Third-party data** is bought from outside aggregators. It is fading as browsers phase out third-party cookies and regulators tighten, and it is not a foundation to build on.

Build the programme on zero- and first-party data, and treat the decline of third-party data as a reason to capture more of your own. See [consent and preferences](/foundations/consent-and-preferences.md) for capturing it lawfully.

# What to capture, and from where

Most programmes under-capture, then try to personalise on fields they never collected. Work the list below before buying tooling, because the tooling can only activate what the profile already holds. Each row names the source, the events worth landing on the profile, and the identifier that ties them to a person.

* **Site and app events.** Page and screen views, product views, search terms, cart add and abandon, wishlist, checkout start. Land each with a timestamp and the anonymous id (cookie or device id) so it can be stitched to a person later.
* **Purchase history.** Order date, line items, value, category, channel, refund and return. This is the heaviest signal for segmentation and lifecycle stage; pull it from commerce, not from email clicks.
* **Email and channel engagement.** Sends, opens (read with the caveats in the channels notes), clicks, the message and journey each came from. Keyed on email address and on the internal contact id.
* **Support and service contacts.** Tickets, chat, returns, complaints, NPS or CSAT responses, last contact date. A recent unresolved ticket should suppress a promotional send, which only works if it lands on the profile.
* **Preferences and stated data.** Preference-centre selections, channel and frequency choices, declared interests, and any zero-party survey or quiz answers. The most durable fields and the cheapest to act on.

For each source, decide the identifier it arrives with (anonymous id, email, phone, account id), the refresh cadence (real-time stream, hourly, daily batch), and the destination field on the unified profile. Anything without a named destination field is data you are paying to store and cannot use.

# The single customer view

A single customer view is one unified profile per person, assembled from every source: the order history from commerce, the events from the site and app, the engagement from the [channels](/channels/), the tickets from support. Without it, each system holds a partial customer and the programme contradicts itself, mailing a discount to someone who just paid full price, or onboarding a customer who has been active for a year.

# Consolidating to one record

Once identity resolution has decided which records belong to one person, you still have to fold several rows into a single profile and pick which value wins when they disagree. A workable approach:

1. **Dedup on a stable key.** Group records by the strongest identifier present, normalised first: lowercase and trim the email, strip formatting and country-code the phone, exact-match the account id. Normalisation before comparison catches the bulk of duplicates that look distinct only because of casing or punctuation.
2. **Choose a resolution rule per field, not per record.** Different fields want different rules. Last-write-wins suits volatile fields like address, current channel preference, or last-seen device, where the newest value is simply the truth. Merge suits accumulating fields like total order count, lifetime value, or the union of product categories viewed, where you sum or union across sources rather than overwrite.
3. **Define the golden record fields explicitly.** List the fields that downstream systems read, name the source of record for each, and store provenance and a timestamp alongside the value. Example: email from the commerce account, name from the latest order, marketing consent from the preference centre, lifetime value computed from all orders. When two sources disagree on a golden field, the named source of record wins; everything else is reference data.
4. **Keep the source rows.** Consolidate into a golden record but retain the underlying records and their lineage, so a wrong merge can be reversed and a disputed value traced to where it came from.

# Identity resolution

Identity resolution is the work of deciding that the anonymous browser, the app login, the email address, and the loyalty number are all the same person, and stitching their activity into one profile. It is what turns scattered identifiers into the single customer view. Done well, anonymous behaviour before signup attaches to the customer once they identify themselves; done badly, the same person appears as several, and frequency caps, suppression, and measurement all leak.

# Matching rules in practice

Resolution comes down to a matching rule: given two records, decide same person or not. Two families of rule, and most stacks use deterministic first and add probabilistic only where they must.

* **Deterministic matching** joins on an exact shared identifier: the same email, the same phone, the same account or loyalty id. It is the default because it is explainable and auditable. When a user logs in, you also bind the anonymous id they were carrying to that account id, which is how pre-signup behaviour attaches to the person.
* **Probabilistic matching** infers a match from a cluster of weaker signals (name plus postal address plus device plus IP) with a confidence score. Use it only where a hard identifier is missing, treat every match as a probability, and never let it silently overwrite a deterministic field.

Merge or keep separate is the live decision, and the asymmetry of the costs should drive it:

1. **Score the candidate pair.** A shared, verified hard identifier is high confidence. A shared weak signal alone is low. Set a high threshold for an automatic merge and a lower band that flags for review rather than merging.
2. **Weigh the two failure modes, which are not equal.** A false split (one person seen as two) costs a duplicated send, a leaky frequency cap, and double-counting in measurement, all annoying but recoverable. A false merge (two people fused) is worse: it can expose one person's order history or address to another, a privacy incident, and it is hard to detect after the fact. So bias the rule toward keeping separate when confidence is below the merge threshold.
3. **Watch for shared identifiers that are not one person.** A household email, a shared family device, or a recycled phone number will pull distinct people together under a naive rule. Require a second corroborating signal before merging on an identifier known to be shareable.
4. **Make merges reversible.** Because a false merge is the expensive error, keep the source records and lineage (as above) so a merge can be unwound when a later signal contradicts it.

> [!caution] A false merge is the expensive error
> Fusing two people can expose one person's history to another, a privacy incident that is hard to detect after the fact, where a false split is merely annoying and recoverable. Bias toward keeping separate below the merge threshold, and keep merges reversible.

# CRM, CDP, and warehouse

Three systems are easy to confuse, and most stacks run more than one.

* A **CRM** manages known relationships and the interactions with them. It is built around the identified customer and the people who act on that relationship.
* A **CDP (customer data platform)** ingests data from every source, resolves identity, and maintains the unified, activation-ready profile that the channels and decisioning read from.
* A **data warehouse** is built for analysis and storage at scale, not for real-time activation.

The distinction that matters operationally: a warehouse is built for analysis, a CDP is built for activation. Which combination you need follows from the [ESP and tooling choices](/foundations/esp-selection.md), not the reverse.

# Choosing a CDP

If you decide you need a CDP, judge candidates against the jobs above rather than the feature list a vendor leads with. Vendor-neutral criteria:

* **Real-time activation.** Can it resolve a profile and push a segment change to the channels in seconds, not in the next batch? A profile that updates daily cannot drive a triggered or abandoned-session message. Ask for the actual end-to-end latency on a worked example, not the marketing claim.
* **Identity-resolution transparency.** Can you see and configure the matching rules, inspect why two records merged, and reverse a merge? A black-box resolver you cannot audit will produce false merges you cannot diagnose. Prefer deterministic-first with the rules exposed.
* **Ingestion and destination coverage.** Does it ingest from your real sources (commerce, app, support, warehouse) and activate to your real channels, with reverse-ETL to and from the warehouse so analysis and activation share one definition?
* **Governance and consent.** Does it carry consent state and lawful basis on the profile, honour suppression and deletion across destinations, and enforce field-level access? Governance you bolt on afterwards rarely holds. See [legislation and compliance](/references/legislation-and-compliance.md).
* **Data ownership and exit.** Can you export the resolved profiles and the raw events, so the resolution work is not trapped in the tool? Test the export before signing.

The data quality you feed it bounds the result more than the brand on the box, so before procuring, run the capture checklist and consolidation rules above against a real sample.

# Hygiene and governance

Data decays. A unified profile that is wrong is worse than no profile, because it fires confident, specific, incorrect messages. Run hygiene as a standing routine, not a one-off cleanup:

1. **Measure completeness by attribute.** For each field that drives messaging, track the share of profiles that have it populated and valid. Completeness varies wildly by field, and a personalisation token is only as safe as the completeness of the field behind it, so know the number before you build on the field.
2. **Set staleness thresholds per field.** A field is stale when it is older than the rate at which the real-world value changes. Address and channel preference go stale slowly; last-active and current cart go stale in days. Define the threshold per field rather than one age for the whole profile.
3. **Define refresh triggers.** Decide what re-collects or re-derives a stale field: a recompute on the next purchase, a preference-centre prompt, a re-permission email, or a recheck against the source of record. A staleness threshold with no refresh trigger just labels rot, it does not fix it.
4. **Suppress and clean continuously.** Suppress hard bounces immediately, suppress spam complaints, and run unengaged contacts through the re-engagement and sunset logic in [segmentation and data](/foundations/segmentation-and-data.md) rather than mailing a decaying list.
5. **Archive what you no longer use.** Profiles past a defined inactivity window, and fields no destination reads, should be archived or deleted under the retention policy. Holding data you do not use is cost and compliance risk with no upside. See [legislation and compliance](/references/legislation-and-compliance.md) for the retention and lawful-basis obligations.

Throughout, hold a documented lawful basis for every contact and deduplicate on the rules above. See [segmentation and data](/foundations/segmentation-and-data.md) for the operational hygiene and [legislation and compliance](/references/legislation-and-compliance.md) for the obligations.

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
