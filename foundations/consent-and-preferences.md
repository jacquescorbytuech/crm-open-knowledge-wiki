---
type: Playbook
title: Consent and Preferences
description: How to capture permission that holds up across every channel, run a preference centre that reduces churn, and operate suppression so the programme stays both compliant and deliverable.
tags: [consent, preferences, permission, suppression, compliance, gdpr, pecr, can-spam, tcpa]
timestamp: 2026-06-14T00:00:00Z
---

# Why permission is a foundation, not a footnote

Permission is the asset the whole programme rests on. It decides who you may contact, it decides deliverability because complaint rates follow weak consent, and it decides trust. The regimes differ by region, but a programme built to the strictest standard it touches satisfies the rest by construction. This is operational guidance, not legal advice; see [legislation and compliance](/references/legislation-and-compliance.md).

# Two consent models, and the channels they govern

The world splits into opt out and opt in, and the split runs by channel and region rather than uniformly.

* **Opt out (United States email).** Under CAN-SPAM you may email without prior consent, provided every message has accurate headers, an ad identification, a valid physical postal address, and a working opt out you honour within ten business days. The FTC enforces this and treats you as responsible for anyone mailing on your behalf.
* **Opt in (United Kingdom and EU, and SMS broadly).** Under PECR and the GDPR you generally need consent before marketing to an individual by electronic mail, with a narrow soft opt in for existing customers being sold similar products who were given an opt out at collection and in every message. PECR defines electronic mail broadly, so email, SMS, in-app messages, and social direct messages all fall under it.
* **Express written consent (United States SMS).** The TCPA sets a higher bar for marketing texts: prior express written consent, honouring of STOP and other reasonable opt out methods, and quiet hours. Treat SMS consent as a separate, stronger grant than email consent, never as inherited.

Consent under the GDPR standard means freely given, specific, informed, and unambiguous, by a clear affirmative action. A pre ticked box is not consent.

# Capture that holds up

Collect consent you can evidence: what they agreed to, when, and how. Keep channel grants separate, because email permission is not SMS permission and is not push permission. State who you are and what they will receive at the point of capture. Prefer an explicit, granular opt in wherever an opt in regime applies, and record the source so a weak channel can be traced and fixed. See [list building](/foundations/list-building.md).

# The preference centre

A preference centre lets a subscriber choose channels, topics, and frequency instead of facing a binary stay or leave. Offered at the moment someone reaches for unsubscribe, it converts a total loss into a reduced, still permissioned relationship: fewer emails rather than none, one channel dropped rather than all. It is one of the few retention tools that is also a compliance asset, because a genuine, easy choice is exactly what the regimes ask for. Honour the choices immediately in the sending logic, not eventually.

# Suppression

A suppression list is the set of addresses and numbers that must never be mailed: the unsubscribed, hard bounces, complainers, and legal suppressions. It is mailed against on every send and is never purged for volume. Suppression is where compliance and deliverability meet, because mailing a complainer or an opt out is both a legal breach and a reputation hit. See [respect the subscriber](/principles/respect-the-subscriber.md) and [engagement is the new deliverability](/principles/engagement-is-deliverability.md).

# Related

* [Legislation and compliance](/references/legislation-and-compliance.md)
* [List building](/foundations/list-building.md)
* [Segmentation and data](/foundations/segmentation-and-data.md)
* [Orchestration and frequency](/foundations/orchestration-and-frequency.md)

# Citations

[1] [ICO, electronic mail marketing under PECR](https://ico.org.uk/for-organisations/direct-marketing-and-privacy-and-electronic-communications/guide-to-pecr/electronic-and-telephone-marketing/electronic-mail-marketing/)
[2] [FTC, CAN-SPAM Act compliance guide for business](https://www.ftc.gov/business-guidance/resources/can-spam-act-compliance-guide-business)
[3] [FCC, Telephone Consumer Protection Act rules](https://www.fcc.gov/general/telemarketing-and-robocall-rules)
