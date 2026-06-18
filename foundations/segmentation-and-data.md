---
type: Playbook
title: Segmentation and Data
description: How to define dynamic and static segments, spot and resolve overlap, run hygiene to an SLA, QA merge tags and dynamic content, and audit consent on a cadence, with the segmentation models and the wider data layer treated separately.
tags: [segmentation, data, personalisation, privacy, merge-tags, hygiene, dynamic-segments, overlap, data-quality]
timestamp: 2026-06-14T00:00:00Z
---

## Building and running segments

Once a model has chosen how to cut the audience, the operational work is defining segments that hold, keeping them correct and current, and keeping the data under them clean enough to send on. The models that decide how you divide an audience in the first place, RFM, value, behavioural, propensity, live in [segmentation models](/foundations/segmentation-models.md), and the data layer underneath all of it, capture, identity, and the single customer view, lives in [customer data and identity](/foundations/customer-data-and-identity.md).

## Dynamic versus static segments

A dynamic segment updates automatically as subscriber data changes: membership is a rule the platform re-evaluates, so contacts join and leave without anyone touching the list. A static segment has fixed membership set at creation and changes only when someone edits it.

Prefer dynamic segments for anything driven by behaviour or state, because they keep themselves current and cannot drift out of date. Reserve static segments for the cases a rule cannot express or should not: a fixed test or holdout cell whose membership must not move mid-experiment, a one-off list from an external source (an event attendee export), or a manually curated VIP list.

A dynamic segment is a rule expression over profile and event fields. Write the rule, not a vague description. Worked definitions:

* **Recently engaged buyers.** `opened_email within last 30 days AND lifetime_value > [your high-value cutoff]`. A value-weighted re-engagement audience.
* **Lapsing best customers.** `last_purchase_date between 90 and 180 days ago AND lifetime_value in top quartile`. The at-risk best-customer cut from [segmentation models](/foundations/segmentation-models.md), made sendable.
* **Onboarding incomplete.** `signup_date within last 14 days AND onboarding_completed = false AND email_consent = true`. Drives the welcome flow in [automation and sequences](/foundations/automation-and-sequences.md).
* **Active SMS-permissioned.** `sms_consent = true AND last_click within last 60 days AND country = [region]`. Channel grant plus engagement, so an SMS send only ever reaches the permissioned and warm.

When writing expressions, be explicit about time windows (last 30 days, not recently), because a vague window becomes a different segment on every platform, and always carry the consent and suppression conditions into the rule itself, so a segment can never resolve to a contact you may not message.

## Segment overlap and the cascade into frequency

Confirm whether segments overlap before combining or sending them together. Free users and users who have not completed onboarding are not mutually exclusive; adding them double-counts the audience, and worse, a contact who sits in several concurrently scheduled segments receives several sends in the same window. Overlap is therefore not just a counting error, it is a frequency problem: it is one of the main ways a programme over-contacts a subset of its list without any single campaign looking heavy.

How to check for overlap before a send window:

1. List every segment scheduled to send in the same window (say the coming week).
2. For each pair, compute the intersection: count the contacts that appear in both. Most platforms expose this as an AND of the two segment rules, or an audience-overlap report.
3. Flag any contact landing in more than the per-tier cap from [orchestration and frequency](/foundations/orchestration-and-frequency.md). The cap, not the overlap count, is the threshold that matters.
4. Resolve, do not just observe. Apply the contact strategy: let the frequency cap and the priority order decide which send that contact actually receives, and suppress the rest for the window. Transactional always wins; promotional yields first. The detailed priority order lives in [orchestration and frequency](/foundations/orchestration-and-frequency.md).

The fix is not to redraw every segment to be mutually exclusive, which is rarely possible. It is to let a single contact strategy arbitrate overlap at send time, so the cap is enforced across all segments at once rather than within each one.

## The cost of segmentation

Segmentation trades statistical power for relevance. Below list sizes in the low thousands the trade is usually a loss, because each segment becomes too small to test or to send to reliably. Targeted segments do earn their keep when they are large enough to send to, consistently outperforming undifferentiated broadcasts on engagement and revenue per recipient. For the minimum cell a test actually needs, defer to [volume thresholds](/measurement/volume-thresholds.md) rather than any fixed number; size a test cell to a realistic win before you split, not after. See also [segmentation has real costs](/principles/segmentation-has-costs.md).

## Data hygiene and SLAs

Hygiene is the foundation the rest sits on: a clean list is what makes segments accurate and sends deliverable. Run it to a service level, not on remembering to, so the standard is a written threshold rather than a habit.

* **Hard bounces: suppress immediately.** A hard bounce means the address is dead. Auto-suppress it the moment it is reported and never re-send, certainly before the next send to that segment fires. A hard bounce that is still in the audience on the following send is an SLA breach.
* **Complaints and unsubscribes: suppress immediately, treat as permanent.** Feed both into the suppression list at once and never reactivate. These are also legal obligations, not just hygiene; see the suppression workflow in [consent and preferences](/foundations/consent-and-preferences.md). Suppression has to travel beyond the sending channels too: a contact removed here must also drop out of any ad-platform [audience sync](/foundations/audience-sync.md), or you are pursuing in paid someone you stopped emailing.
* **Sunset by inactivity window.** Move contacts with no engagement across a set window into the re-engagement sequence, then suppress from broadcast any who do not respond. Set the window from your own sending cadence and engagement distribution rather than a flat number, since the same span is many sends for a daily sender and only a handful for a monthly one. Keep the dormancy criteria identical to the sunset logic in [automation and sequences](/foundations/automation-and-sequences.md) so the flow and the segment agree. The full decay, re-engagement and sunset lifecycle this hygiene step sits inside, including why suppressing dormant contacts protects sender-level reach, is [database health and sunsetting](/foundations/database-health.md).

See [engagement is the new deliverability](/principles/engagement-is-deliverability.md).

## Merge identities carefully

When two records resolve to one person and get merged, the merge itself is a data-quality risk: a bad merge tag mapping, or a merge that picks the wrong field as the survivor, silently corrupts the profile that every downstream segment and merge field reads. Treat merge and dedup as a controlled operation, not a background convenience: define which record wins per field, preserve the consent and suppression state of both records (a merge must never resurrect a suppressed contact), and spot-check merged profiles. The identity mechanics live in [customer data and identity](/foundations/customer-data-and-identity.md).

## Personalisation and merge tags

A merge tag is a placeholder replaced with subscriber-specific data at send time. A dynamic content block displays differently based on subscriber data. Personalisation is a real lever, but it depends on clean data: a merge tag firing a blank, a default, or a wrong value is worse than no personalisation at all, which is why the [data layer](/foundations/customer-data-and-identity.md) comes first.

QA every merge field and dynamic block before a send goes live. The checklist:

1. **Test for blanks and defaults.** Send to seed contacts that deliberately have the field missing, empty, and populated. Confirm the missing and empty cases render the fallback, not `Hi ,` or a raw `[FIRST_NAME]` token.
2. **Confirm fallback content exists for every tag.** Every merge field needs a sensible default. `Hi {{ first_name | default: "there" }}` renders `Hi there` when the name is missing, never `Hi`.
3. **Validate field mapping.** Confirm the tag points at the field you think it does. A common failure is a tag mapped to the wrong source field, so it renders a real but wrong value (someone else's first name, a stale address), which no blank-check catches.
4. **Check dynamic-content branches.** Each branch must have a defined audience and a fallback branch for contacts who match none, so nobody receives an empty block. Worked example: a block showing a recommended category renders the recommended category when `top_category` is set, and a default best-sellers block when it is empty, so the slot is never blank.

This is the same merge-field check the pre-launch testing list in [automation and sequences](/foundations/automation-and-sequences.md) calls for; run it for broadcasts too, not only flows.

## Privacy and the consent audit cadence

Privacy is integral to operations, not a separate compliance task bolted on after. Every segment and every send reads contact data, so the lawful basis and consent state must be correct in the same records the segments query. Hold a documented lawful basis for every contact, keep records of how and when consent was obtained, and honour opt-outs immediately. The capture mechanics, the suppression workflow, and the regime details live in [consent and preferences](/foundations/consent-and-preferences.md); declared preferences captured there are also zero-party data you can target on.

Audit the data and consent state on a cadence rather than waiting for a problem to surface it:

* **Profile completeness.** Track the fill rate of the fields your segments depend on (consent flags, engagement dates, value fields). A field your targeting relies on that is blank for much of the list is a silent segmentation failure.
* **Deduplication.** Periodically scan for duplicate identities and merge them under the controlled process above, so one person is not counted, contacted, or suppressed as two.
* **Lawful basis and consent date.** Confirm every contact carries a recorded lawful basis and a consent timestamp, and that channel grants are stored separately (email permission is not SMS permission). Flag any contact missing a basis for review or suppression.
* **Tracking-derived fields.** The engagement and behavioural fields many segments target are collected under a separate tracking consent, and that consent travels with the data: a contact who withheld it cannot be targeted on those fields even with a clean sending permission. Carry the tracking-consent state alongside the channel grants. See [tracking and measurement consent](/references/tracking-and-measurement-consent.md).

Set the cadence to your volume and risk; the point is that it is scheduled, with a written threshold, not triggered by an incident.

## Related

* [Segmentation models](/foundations/segmentation-models.md)
* [Customer data and identity](/foundations/customer-data-and-identity.md)
* [Orchestration and frequency](/foundations/orchestration-and-frequency.md)
* [Automation and sequences](/foundations/automation-and-sequences.md)
* [Database health and sunsetting](/foundations/database-health.md)
* [Audience sync](/foundations/audience-sync.md)
* [Consent and preferences](/foundations/consent-and-preferences.md)
* [Tracking and measurement consent](/references/tracking-and-measurement-consent.md)
* [Segmentation has real costs](/principles/segmentation-has-costs.md)
* [Volume thresholds](/measurement/volume-thresholds.md)
* [Legislation and compliance](/references/legislation-and-compliance.md)

## Citations

[1] [Klaviyo, ecommerce benchmarks (targeted segments outperform broad sends on engagement and revenue per recipient)](https://www.klaviyo.com/marketing-resources/ecommerce-benchmarks)
