---
type: Framework
title: Lead management
description: The B2B motion the rest of this bundle's lifecycle frame does not cover: scoring leads on fit and engagement, the MQL and SQL definitions and the sales handoff that sit on top of them, nurturing the not-yet-ready, and where account-based marketing inverts the whole funnel.
tags: [b2b, lead-scoring, mql, sql, nurturing, abm, lifecycle, sales]
timestamp: 2026-06-15T00:00:00Z
---

## The B2B funnel the lifecycle frame omits

[Lifecycle mapping](/foundations/lifecycle-mapping.md) assumes a transactional relationship: someone is a customer, and the programme moves them through onboarding, engagement, retention, and winback. Considered B2B sale, where the deal is large, the cycle is long, and a buying committee decides, has a stage the consumer frame does not: a pre-customer funnel where a contact is captured, qualified, and handed to a salesperson who closes the deal in person. Lead management is the operations of that funnel, and it is the half of CRM practice the rest of this bundle, skewed to consumer lifecycle and retention, otherwise leaves out.

The data and channels are the same ones described elsewhere: first-party data, email and the owned channels, consent. What changes is the goal. The programme is not driving a purchase directly; it is producing a qualified, sales-ready contact and a clean handoff, and being measured on the revenue that closes downstream of it.

## Lead scoring

Lead scoring ranks contacts so the programme can act on the ones worth acting on. Durable models score fit and engagement, and keep them apart:

* **Fit (explicit).** How closely the contact matches the ideal customer: the [firmographic](/foundations/segmentation-models.md) attributes (industry, company size, revenue) and the person's role and seniority. Fit answers *should we want them*.
* **Engagement (implicit).** What the contact has done: content downloads, pricing-page visits, webinar attendance, email engagement. Engagement answers *are they interested now*.

Score each axis on its own rather than collapsing them into one number, because the failure modes are opposite and need different handling. A high-fit, low-engagement contact is a target to nurture; a low-fit, high-engagement contact is often a student, a competitor, or a job-seeker, and feeding them to sales burns the goodwill the handoff depends on. The score is a [propensity](/foundations/segmentation-models.md) prediction dressed in points, so the same caution applies: it predicts who looks ready, not who your contact changed, and it is only as good as the data underneath it.

## MQL, SQL, and the handoff

MQL and SQL are thresholds a team agrees on, not states a contact is objectively in:

* **Marketing-qualified lead (MQL).** A contact whose combined fit and engagement clears the threshold marketing and sales have agreed means *ready for a sales conversation*. The threshold is a decision, not a fact: set it where the leads sales actually accepts cluster, and move it when acceptance drifts.
* **Sales-qualified lead (SQL).** An MQL that a salesperson has accepted and confirmed, through their own qualification, as a genuine opportunity worth working.

The handoff between them is where most B2B programmes leak, and the fix is an explicit service-level agreement between the two teams. The SLA pins down the MQL and SQL definitions, so both sides agree what qualifies; commits sales to follow up an MQL within a fixed window (24 to 48 hours is the common default, because a lead's engagement decays the way [the welcome window](/principles/the-welcome-window.md) describes); and sets up a feedback loop where sales marks why rejected MQLs were rejected, which is the signal that recalibrates the score. Without that loop the score drifts and sales quietly stops trusting marketing's leads.

> [!warning] A lead is still personal data
> B2B does not exempt you from consent. Capture is governed by the same rules as [list building](/foundations/list-building.md) and [consent and preferences](/foundations/consent-and-preferences.md); a named individual at a company is their personal data under UK GDPR even where [cold email](/foundations/cold-email.md)'s narrow B2B window is open. Score and nurture the leads you captured lawfully, not a bought list.

## Nurturing the not-yet-ready

Most captured leads are not MQLs yet, and handing them to sales early wastes the sales time the SLA is trying to protect. Lead nurturing is the [automated sequence](/foundations/automation-and-sequences.md) that keeps a high-fit, low-engagement contact warm until their engagement clears the threshold: educational content matched to the buying stage, paced so it informs rather than pesters, with the lead score updating as they respond. The job is to move fit-without-interest toward interest, then let the score trigger the handoff. It is the same trigger-and-sequence machinery the consumer side uses for onboarding, pointed at qualification instead of retention.

## Where account-based marketing inverts the funnel

Lead scoring runs the funnel forward: capture many contacts, score them, surface the few that qualify. Account-based marketing (ABM) runs it backward. It starts from a named list of target accounts the business has already decided are worth winning, then orchestrates marketing and sales together against the buying committee inside each one, treating the account, not the individual lead, as the unit. It suits a small number of high-value accounts where the individual-lead funnel is too coarse; inbound scoring suits the opposite, a large volume of leads where you cannot pursue each by hand. Most mature B2B programmes run both, and the [audience sync](/foundations/audience-sync.md) machinery is what pushes a target-account or high-score segment into the ad platforms for the paid layer.

## Measuring it

Lead management's tempting metrics are the funnel counts (leads, MQLs, SQLs), and they are [vanity metrics](/measurement/core-metrics.md) until tied to what closes. Tie the score to downstream conversion: of the contacts scored MQL, what share sales accepted, and of those, what share became revenue. A scoring model that produces MQLs sales rejects is mis-tuned however good the count looks. The score predicts; only a [holdout](/measurement/holdouts-and-control-groups.md) tells you whether the nurturing changed the outcome rather than messaging buyers who would have converted anyway.

## Related

* [Lifecycle mapping](/foundations/lifecycle-mapping.md)
* [Segmentation models](/foundations/segmentation-models.md)
* [Automation and sequences](/foundations/automation-and-sequences.md)
* [Audience sync](/foundations/audience-sync.md)
* [Cold email](/foundations/cold-email.md)
* [Consent and preferences](/foundations/consent-and-preferences.md)
* [Decisioning and personalisation](/foundations/decisioning-and-personalisation.md)
* [Uplift and incrementality](/measurement/uplift-and-incrementality.md)

## Citations

[1] [SmartBug Media, handing leads off to sales and the MQL vs SQL difference](https://www.smartbugmedia.com/blog/handing-leads-off-to-sales-the-mql-vs-sql-difference)
[2] [Factors.ai, MQL vs SQL and sales-marketing alignment](https://www.factors.ai/blog/mql-vs-sql)
[3] [Marqeu, B2B demand waterfall implementation guide (stage definitions, entry/exit criteria, SLAs)](https://www.marqeu.com/demand-waterfall-implementation-guide)
