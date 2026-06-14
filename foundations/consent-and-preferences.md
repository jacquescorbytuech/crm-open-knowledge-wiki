---
type: Playbook
title: Consent and Preferences
description: How to capture permission that holds up across every channel, run a preference centre that reduces churn, and operate suppression so the programme stays both compliant and deliverable, with the checklists and form mechanics to do each.
tags: [consent, preferences, permission, suppression, compliance, gdpr, pecr, can-spam, tcpa, preference-centre, unsubscribe]
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

# Priming the ask

Permission converts better, and the grant holds up better, when you set the expectation before you ask for it. Priming is showing the value and the terms first, what they will get, why, and roughly how often, so the opt in is a considered yes rather than a reflex, and then making the ask at the moment that value is obvious. It is both a conversion lever and a consent quality lever: a primed subscriber complains and unsubscribes less because the mail matches what they were told to expect, which is exactly the informed, specific standard the [opt in regimes](#gdpr-and-pecr-opt-in-form-mechanics) ask for. The two settings differ in mechanism but not in principle:

* **Scarce platform permissions are structurally one-shot, so priming is mandatory.** The push, [browser push](/channels/browser-push.md), location, and App Tracking Transparency dialogs can be shown once, and a denial is sticky, so a cold prompt with no context spends the only ask you get. Show your own soft prompt first, framed in the value, and fire the native dialog only when the user accepts it, so a no on the soft ask costs nothing. See [the pre-permission prompt](/channels/push.md).
* **Owned channels prime through pre opt in context.** Email and SMS let you ask again, so the failure mode is not a burned grant but a weak, complaint-prone one. Name the programme and its frequency at the point of capture, prefer a value exchange the subscriber understands over a bare "subscribe" box, and lead with what they get rather than the form. This is the same expectation setting, applied to a channel you can re-approach.

Across both, priming is why a smaller, expectation-matched list outperforms a larger cold one; see [list quality over size](/principles/list-quality-over-size.md).

# A CAN-SPAM compliance checklist

Run every US commercial email against this before it sends. None of these is optional, and a single failing send is a separate violation per recipient.

- [ ] **Accurate from, to, and routing.** The from name, from address, and reply path identify the actual sender. No spoofed or misleading origin.
- [ ] **Non deceptive subject line.** The subject reflects the content of the message; it does not bait an open with a claim the body does not deliver.
- [ ] **Identified as an advertisement.** Where the message is promotional, it is clear that it is an ad. The disclosure can be brief but must be present.
- [ ] **Valid physical postal address.** A real, current postal address for the sender appears in the message. A registered PO box or commercial mail receiving agency address is acceptable.
- [ ] **Clear, working opt out.** A conspicuous unsubscribe mechanism that works for at least 30 days after sending, requires no fee, no login, and no information beyond an email address and the choice of what to stop.
- [ ] **Opt out honoured within ten business days.** The request is processed and the address suppressed within ten business days; you may not sell or transfer an address once opt out is requested.
- [ ] **Liability for others.** If a partner or agency mails on your behalf, you are still responsible. Confirm they meet the same checklist.

# GDPR and PECR opt in: form mechanics

Where an opt in regime applies, the form is the evidence. Build it so the record itself proves the consent was valid.

1. **Unticked checkbox, always.** The consent box is empty by default and the user actively ticks it. Pre ticked boxes, silence, or inactivity are not consent. Consent cannot be bundled into the terms and conditions acceptance.
2. **Granular, per channel and per purpose.** Offer separate opt ins, for example email newsletter, SMS offers, and product research, rather than one blanket grant. Do not gate the core service on marketing consent, or it is not freely given.
3. **Informed at the point of capture.** State who you are, what they will receive, roughly how often, and link your privacy notice next to the box. The wording the user saw is part of the record.
4. **Capture the consent record at submission.** Store, against the contact:
   - Timestamp of the opt in.
   - Source or form identifier, and the channel and purpose granted.
   - The exact consent wording shown at that time, or a versioned reference to it.
   - The mechanism, for example double opt in confirmation, with the confirmation timestamp.
5. **Confirm where it strengthens the record.** Double opt in (a confirmation click on a follow up email) both proves the address is controlled by the consenter and filters mistyped or hostile signups; it is the stronger evidence and improves early deliverability.
6. **Make withdrawal as easy as granting.** Withdrawing consent must be as simple as giving it, and on withdrawal you keep the suppression record but stop the processing.

# Preference centre design

A preference centre lets a subscriber choose channels, topics, and frequency instead of facing a binary stay or leave. It is one of the few retention tools that is also a compliance asset, because a genuine, easy choice is exactly what the regimes ask for. Honour the choices immediately in the sending logic, not eventually. See [zero-party data](/foundations/segmentation-and-data.md) for using the declared preferences in targeting.

Design it with three independent controls:

* **Channel toggles.** Separate on or off switches per channel: email, SMS, push, post. Reflect the regime, so an SMS toggle off here also flags the TCPA opt out. Channels are independent grants and must toggle independently.
* **Frequency options.** A small set of clear choices rather than a slider, for example weekly, monthly, or only the essentials. A frequency down shift is the most common save, so make it the easiest one to pick.
* **Topic selection.** Let the subscriber keep the content they want and drop the rest, for example order updates yes, promotions no, or one product line only. Topic granularity also feeds segmentation.

Pre fill the centre with the subscriber's current state so they edit rather than reconstruct, and write changes to the sending logic on save so the next send already obeys them.

# The unsubscribe page: offer the down shift first

The link in the footer should not land on a bare "you are unsubscribed" confirmation. Sequence it so full opt out is the last resort, never the only option.

1. Land the user on a page that leads with the lighter alternatives: reduce frequency, pause for a period, or pick only the topics they care about.
2. Present full unsubscribe as a clearly available choice on the same page, not hidden, because the law requires it to be easy and burying it is both a breach and an annoyance.
3. If they do unsubscribe, honour it on a single click without forcing a login, and confirm plainly. Write the suppression immediately.
4. Keep a one click global opt out reachable throughout, so a frustrated user always has the simple exit and never resorts to the spam button.

The down shift converts a total loss into a reduced, still permissioned relationship: fewer emails rather than none, one channel dropped rather than all.

# TCPA SMS: opt in capture, STOP and HELP, logging

Marketing SMS in the US needs prior express written consent, which is a higher bar than email. Build the flow to produce that record and to handle the standard keywords automatically.

* **Capture the written consent explicitly.** At signup, the user takes a clear affirmative action (ticks an unticked box, or texts a keyword to your number) against disclosure language that names the programme, states that consent is not a condition of purchase, and gives message frequency and that message and data rates may apply. Capture phone number, timestamp, the exact disclosure wording, and the source.
* **Send a confirmation message first.** The opening text confirms enrolment and restates the programme name, frequency, the HELP and STOP instructions, and that rates may apply.
* **Honour STOP automatically.** On STOP (and common variants such as STOPALL, UNSUBSCRIBE, CANCEL, QUIT, END), send one final confirmation that they are opted out and then send nothing further to that number. Add the number to suppression.
* **Answer HELP automatically.** On HELP, return programme name and a contact, for example a support address or number.
* **Log every consent and opt out event.** Keep an auditable trail of the opt in, the confirmation, any HELP request, and the STOP, each with a timestamp, so you can evidence the grant and the cessation.
* **Never inherit it.** An email subscriber has not consented to SMS. Capture SMS consent on its own.

# Suppression workflow

A suppression list is the set of addresses and numbers that must never be mailed: the unsubscribed, hard bounces, complainers, and legal suppressions. It is mailed against on every send and is never purged for volume. Suppression is where compliance and deliverability meet, because mailing a complainer or an opt out is both a legal breach and a reputation hit.

Operate it as a continuous loop:

1. **Capture from every signal.** Feed the list from unsubscribe clicks and preference centre opt outs, spam complaints via feedback loops, hard bounces, STOP keywords, and any legal or manual suppressions. Record the reason and timestamp for each.
2. **Apply across all sources and channels.** Check every send against suppression regardless of which tool or list the audience came from. A suppression in one system must not be defeated by a fresh import or a second platform. Keep one authoritative list per channel and reconcile imports against it.
3. **Suppress, do not delete.** Keeping the record is what proves you honoured the opt out; deleting the contact loses that evidence and risks re mailing on the next import. Retain the consent and opt out records for as long as you might need to defend the decision.
4. **Honour promptly.** Process opt outs into suppression fast, well inside the CAN-SPAM ten business day ceiling, and immediately for STOP and preference changes.
5. **Audit periodically.** Spot check that suppressed contacts are not receiving mail and that complaint and bounce feeds are still flowing into the list.

See [respect the subscriber](/principles/respect-the-subscriber.md) and [engagement is the new deliverability](/principles/engagement-is-deliverability.md).

# Related

* [Legislation and compliance](/references/legislation-and-compliance.md)
* [Tracking and measurement consent](/references/tracking-and-measurement-consent.md)
* [List building](/foundations/list-building.md)
* [Segmentation and data](/foundations/segmentation-and-data.md)
* [Orchestration and frequency](/foundations/orchestration-and-frequency.md)
* [Respect the subscriber](/principles/respect-the-subscriber.md)
* [Engagement is the new deliverability](/principles/engagement-is-deliverability.md)

# Citations

[1] [ICO, electronic mail marketing under PECR](https://ico.org.uk/for-organisations/direct-marketing-and-privacy-and-electronic-communications/guide-to-pecr/electronic-and-telephone-marketing/electronic-mail-marketing/)
[2] [FTC, CAN-SPAM Act compliance guide for business](https://www.ftc.gov/business-guidance/resources/can-spam-act-compliance-guide-business)
[3] [FCC, Telephone Consumer Protection Act rules](https://www.fcc.gov/general/telemarketing-and-robocall-rules)
