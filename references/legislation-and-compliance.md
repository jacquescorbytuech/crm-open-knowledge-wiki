---
type: Reference
title: Legislation and Compliance
description: The main email and privacy regimes a sender operates under, grounded in the regulators' own guidance, and the practical minimum that satisfies the spirit of all of them.
tags: [legislation, compliance, gdpr, can-spam, pecr, tcpa, casl, ccpa, sender-id]
timestamp: 2026-06-14T00:00:00Z
---

> [!caution] This is not legal advice
> The following orients you to the major regimes; it is not legal advice. Obligations turn on where your recipients are, not only where you are, so a UK sender mailing EU and US recipients is subject to several at once. Take qualified advice for your specific situation.

## The main regimes

| Regime | Region | Consent model | Core obligations |
| --- | --- | --- | --- |
| CAN-SPAM | United States, email | Opt out | Accurate headers and from line, no deceptive subject, identify the message as an ad, a valid physical postal address, a clear opt out honoured within ten business days, and responsibility for anyone mailing on your behalf. |
| TCPA | United States, SMS and calls | Express written | Prior express written consent for marketing texts, STOP and any reasonable opt out method, and quiet hours of 8am to 9pm in the recipient's local time. |
| GDPR | EU and EEA | Opt in | A documented lawful basis, consent that is freely given, specific, informed, and unambiguous where relied on, records of consent, data subject rights, and prompt opt out. |
| UK GDPR and PECR | United Kingdom | Opt in, narrow soft opt in | PECR regulation 22 governs electronic marketing on top of UK GDPR; consent or the soft opt in is needed to market to individuals by electronic mail. |
| CASL | Canada | Express or implied opt in | One of the strictest regimes: express or implied consent, clear sender identification, and a working unsubscribe, with significant penalties. |
| CCPA and CPRA | California | Opt out, plus deletion right | Disclosure of data practices, a right to opt out of sale or sharing, and a right to deletion. |

## CAN-SPAM, precisely

The FTC distils CAN-SPAM into a short list that applies to every commercial email: do not use false or misleading headers; do not use a deceptive subject line; identify the message as an advertisement; tell recipients where you are located with a valid physical postal address; tell them how to opt out; honour opt outs within ten business days; and stay responsible even when a third party mails for you. There is no prior consent requirement, which is what distinguishes the US email regime from the UK and EU. Penalties run to tens of thousands of dollars per email.

## PECR and the breadth of electronic mail

> [!danger] You must not market to individuals without consent or the soft opt in
> PECR regulation 22 prohibits unsolicited electronic mail marketing to individuals unless they have consented or you meet the soft opt in: an existing customer, sold similar products, given a clear opt out both when their details were collected and in every message.

The ICO defines electronic mail broadly, covering email, text messages, picture and video messages, voicemail, in-app messages, and direct messages on social media, so SMS and in-app messaging fall under these rules, not only email. Consent takes the UK GDPR standard. Marketing to corporate subscribers does not require consent, though honouring objections is good practice.

## TCPA, the higher bar for SMS

Marketing texts in the US sit under the TCPA, which requires prior express written consent rather than the opt out model that governs email. Honour STOP and, since the FCC's 2025 rules, any reasonable opt out method, within ten business days. Observe quiet hours. Application to person traffic also runs through carrier registration via the 10DLC system; see [SMS and RCS](/channels/sms-and-rcs.md).

## Carrier-level sender registration

Consent is not the only gate on messaging. Some markets run registers that verify which organisation a message claims to come from, independently of whether the recipient consented. US application-to-person SMS requires 10DLC brand and campaign registration; Australia's SMS Sender ID Register, run by the ACMA, makes registration of branded (alphanumeric) sender IDs mandatory from 1 July 2026, after which an unregistered brand label is shown to recipients as `Unverified` alongside suspected scams. These sit on top of consent law, not in place of it: you can hold valid consent and still have your brand traffic degraded if the sender ID is unregistered. See [SMS and RCS](/channels/sms-and-rcs.md).

## The practical minimum

Operate to the strictest regime your list touches and you satisfy the rest by construction. Collect consent you can evidence, keep channel grants separate, prefer an explicit opt in wherever an opt in regime applies, identify yourself honestly in every message, include a real postal address, make opt out easy and honour it without delay, keep a suppression list that is never mailed, and hold a documented lawful basis for every contact. This is also good deliverability practice, since the bulk sender requirements enforce one click unsubscribe and a low complaint rate as a condition of reaching the inbox. See [authentication](/foundations/authentication.md) and [consent and preferences](/foundations/consent-and-preferences.md).

## Where compliance and strategy meet

Respecting the recipient is both the ethical and the commercial position. Honest expectations at opt-in, easy exit, and prompt opt out reduce complaints, which protect sender reputation, which protect reach. The regimes formalise a floor a well run programme would clear anyway. See [respect the recipient](/principles/respect-the-recipient.md).

## Related

* [Consent and preferences](/foundations/consent-and-preferences.md)
* [Cold email](/foundations/cold-email.md)
* [Tracking and measurement consent](/references/tracking-and-measurement-consent.md)
* [Authentication](/foundations/authentication.md)
* [SMS and RCS](/channels/sms-and-rcs.md)
* [Respect the recipient](/principles/respect-the-recipient.md)

## Citations

[1] [FTC, CAN-SPAM Act compliance guide for business](https://www.ftc.gov/business-guidance/resources/can-spam-act-compliance-guide-business)
[2] [ICO, electronic mail marketing under PECR](https://ico.org.uk/for-organisations/direct-marketing-and-privacy-and-electronic-communications/guide-to-pecr/electronic-and-telephone-marketing/electronic-mail-marketing/)
[3] [FCC, telemarketing and robocall rules](https://www.fcc.gov/general/telemarketing-and-robocall-rules)
[4] [ACMA, SMS Sender ID Register](https://www.acma.gov.au/sms-sender-id-register)
