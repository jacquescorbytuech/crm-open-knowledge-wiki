---
type: Reference
title: Cold email
description: Why cold email sits outside the consent-first discipline the rest of this bundle describes, why it is spam by that standard, the narrow legal window where it is nonetheless permitted (US CAN-SPAM and UK B2B to corporate or role-based addresses under PECR), and why lawful is not the same as effective.
tags: [cold-email, spam, consent, can-spam, pecr, deliverability, b2b]
timestamp: 2026-06-15T00:00:00Z
---

## The exception to consent

Every other page here assumes consent. The list is built from people who asked to hear from you, the data is first-party, and the whole programme is downstream of someone opting in. Cold email is the inverse: unsolicited messaging to people who never gave you their address for this purpose and have no relationship with you. It contradicts that assumption, and the contradiction is the point. Measured against the standard the rest of this bundle holds, cold email is spam.

## Why it is spam by this bundle's own standard

[Respect the recipient](/principles/respect-the-recipient.md) starts from being honest about what someone signed up for. With cold email there is nothing they signed up for; the relationship begins with a message they did not ask for, optimised for your goal rather than any expectation of theirs. The legitimate way to reach a stranger is to earn the opt in, which is the entire subject of [list building](/foundations/list-building.md): a value proposition, a clear ask, and a consent record you can evidence. Cold email skips that and treats the absence of a relationship as a thing to be exploited rather than built. That it can be done at volume does not change what it is.

## The legal window

Spam in the moral sense is not the same as unlawful, and the regimes diverge sharply on this exact point. The mechanics are in [legislation and compliance](/references/legislation-and-compliance.md); what matters here is where the window is open.

* **United States.** CAN-SPAM is an opt-out regime, not an opt-in one. There is no prior consent requirement for commercial email, so cold email to US recipients is lawful provided the message uses accurate headers and a truthful subject, identifies itself as an advertisement, carries a valid physical postal address, and offers an opt out honoured within ten business days. This is the widest window of any major regime.
* **United Kingdom, business addresses.** PECR regulation 22's consent requirement applies to *individual* subscribers. Marketing to *corporate* subscribers (companies, LLPs, public bodies) does not require consent, so B2B cold email has a lawful path the consumer channel does not. It is cleanest at role-based addresses such as `info@`, `sales@`, or `enquiries@`, which are not personal data and sit unambiguously on the corporate side of the line. A message to a named individual at a company (`jane.smith@`) is still that person's personal data under UK GDPR, so the right to object and a lawful basis apply even there.

> [!warning] The window does not cover consumers in opt-in regimes
> Cold email to individuals under UK GDPR and PECR, to consumers in the EU, or under CASL in Canada is unlawful without consent or a recognised exception. The two openings above are narrow: US recipients, and UK business or role-based addresses. Obligations follow the recipient's location, not yours, so one campaign can be lawful for part of a list and a breach for the rest.

## Lawful is not the same as effective

Even inside the window, cold email works against the asset the rest of this programme spends its effort building. A cold list has no engagement history, so the provider has nothing good to weigh, and the early complaints and spam-trap hits that cold sending attracts feed straight into the sender-level reputation that decides placement. That is the mechanism in [engagement is the new deliverability](/principles/engagement-is-deliverability.md): weak engagement is read as a property of the sender, so a cold campaign does not only underperform on its own, it drags the placement of the warmed, consented programme sharing that reputation. The complaint thresholds the bulk-sender rules enforce are easy to breach with a list that never opted in.

In practice, if cold outreach is run at all, it is run on separate sending infrastructure (a distinct domain and IP) so it cannot poison the warmed estate, at low volume, to genuinely relevant recipients, with the opt out honoured instantly. Those are damage-limitation guardrails, not a recipe for it working well. In short, the lawful window is real and narrow, and even within it cold email earns less and risks more than the consent-first path it bypasses.

## Related

* [Respect the recipient](/principles/respect-the-recipient.md)
* [List building](/foundations/list-building.md)
* [Legislation and compliance](/references/legislation-and-compliance.md)
* [Engagement is the new deliverability](/principles/engagement-is-deliverability.md)
* [Deliverability](/foundations/deliverability.md)
* [Consent and preferences](/foundations/consent-and-preferences.md)

## Citations

[1] [FTC, CAN-SPAM Act compliance guide for business](https://www.ftc.gov/business-guidance/resources/can-spam-act-compliance-guide-business)
[2] [ICO, electronic mail marketing under PECR](https://ico.org.uk/for-organisations/direct-marketing-and-privacy-and-electronic-communications/guide-to-pecr/electronic-and-telephone-marketing/electronic-mail-marketing/)
[3] [ICO, business-to-business direct marketing under PECR](https://ico.org.uk/for-organisations/direct-marketing-and-privacy-and-electronic-communications/guide-to-pecr/electronic-and-telephone-marketing/business-to-business-direct-marketing/)
