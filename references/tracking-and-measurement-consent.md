---
type: Reference
title: Tracking and Measurement Consent
description: Why the right to track is a separate consent from the right to send, grounded in Article 5(3) of the ePrivacy Directive and the 2026 French and Italian rulings on email tracking pixels, and how the same split runs across web, app, push and the other channels.
tags: [legislation, compliance, gdpr, eprivacy, tracking-pixel, consent, cnil, garante, measurement, cookies, app-tracking, att]
timestamp: 2026-06-14T00:00:00Z
---

> [!caution] This is not legal advice
> This orients you to a fast-moving area; it is not legal advice. These rulings are recent and obligations turn on where your recipients are. Take qualified advice for your specific situation.

See [legislation and compliance](/references/legislation-and-compliance.md) for the sending-consent regimes this sits alongside.

## Two different consents: to send, and to track

Most compliance discussion is about the right to *send*: may you put a marketing message in this person's inbox. That is governed by [PECR, the GDPR, CAN-SPAM and the rest](/references/legislation-and-compliance.md). There is a second, separate question that owned-channel programmes routinely overlook: may you *track* what the recipient does with the message, the open pixel that fires when images load and the redirect that records a click.

In the EU these are not the same permission. The right to send rests on consent or a lawful basis under the GDPR; the right to drop a tracking pixel rests on **Article 5(3) of the ePrivacy Directive**, the same provision that governs cookies. A pixel reads from and writes to the recipient's device, so it falls under the cookie rule, and that rule generally requires prior consent of its own.

> [!important] The right to send is not the right to track
> You can have a clean, fully consented right to email someone and still have no lawful basis to measure their opens.

## The Article 5(3) baseline

Article 5(3) of the ePrivacy Directive requires consent before storing information on, or accessing information already stored on, a user's terminal equipment, unless it is strictly necessary to provide a service the user requested. The European Data Protection Board's **Guidelines 2/2023** on the technical scope of Article 5(3) confirmed that the provision is technology-neutral and reaches email tracking pixels, not only browser cookies. Because every EU and EEA member state transposes the same directive, this baseline applies across the bloc, and national authorities cite each other's reasoning when they apply it.

So open and click tracking in the EU is presumptively a consent activity, with a narrow strictly-necessary exemption, regardless of how solid your sending consent is.

## France: the CNIL recommendation

In April 2026 the CNIL adopted a recommendation on tracking pixels in email (Decision No. 2026-042), applying Article 82 of the French Data Protection Act, France's transposition of Article 5(3). Its core positions:

* **Two independent consents.** One to receive marketing email, and a *separate* consent for the deployment of the tracking pixel. One does not imply the other, and bundling them is not valid.
* **Consent is the default for analytics uses.** Prior, specific consent is required wherever pixels are used for campaign performance analysis (measuring open rates to tune frequency, content or channel), recipient profiling, fraud or bot detection, or individual-level open tracking beyond what deliverability strictly needs.
* **A narrow exemption.** Limited security purposes and basic list hygiene can fall outside the consent requirement, but most marketing and analytics uses do not.

The CNIL stressed it was clarifying rules in force since the GDPR applied in 2018, not creating new ones.

## Italy: the Garante guidelines

Days later, in April 2026, the Italian Garante adopted guidelines on tracking pixels in email under the ePrivacy Directive, the Italian Data Protection Code and the GDPR. Its positions track the CNIL's with one notable difference on aggregate measurement:

* **Consent at collection, no bundling.** Pixels are prohibited unless prior consent is obtained or an exemption applies. Consent should be taken when the email address is collected, after clear information about the pixel and its purpose. A "take it or leave it" bundle with the newsletter subscription will not meet the standard.
* **An anonymous-aggregate exemption.** Consent is not required where the pixel serves only an anonymised statistical count of the overall open rate, provided standardised pixels are used and related technical data are anonymised. Authentication-related security measures and legally required service messages are also exempt.
* **A compliance deadline.** The guidelines opened a six-month window expiring **28 October 2026**. Fines reach the GDPR ceiling of €20 million or 4% of worldwide annual turnover.

## Germany and the wider bloc

Germany transposes Article 5(3) through §25 of the TDDDG (the renamed TTDSG). The German Data Protection Conference's guidance, supplementing EDPB Guidelines 2/2023, treats email pixel tracking as requiring consent on the same basis. France and Italy are simply the authorities that have published the most explicit email-specific guidance; the underlying obligation exists in every member state, and the Dutch, Spanish and other DPAs apply the same logic. Treat the French and Italian texts as the clearest statement of a rule that holds bloc-wide, not as two national quirks.

## The same split, across the channels

The email pixel is one instance of a rule that is not about email. EDPB Guidelines 2/2023 read Article 5(3) as technology-neutral: it governs any storing of information on, or access to information already on, a user's terminal equipment, and that terminal equipment is the smartphone, laptop, or connected TV, not the inbox. So the divide between the permission to deliver and the permission to track recurs in every channel that reaches the device, and the deeper the reach, the sharper it gets.

* **Web and onsite.** Cookies and local storage are the original case of Article 5(3), and the consent banner is where it is asked. A visitor who declines tracking consent cannot be profiled, which is a legal cap on what [website personalisation](/channels/website-personalisation.md) can do rather than a technical one, and it is the same grant the email pixel needs, asked at a different surface.
* **Mobile app, push and in-app.** An app SDK that reads a device identifier or writes to local storage sits squarely within Article 5(3), and platform rules stack on top of the law: Apple's App Tracking Transparency requires a prompt before an app may access the IDFA to track across apps, and Android has been moving to restrict its advertising identifier on a similar path. The OS permission to send a [push](/channels/push.md) is a separate grant again, distinct from both the right to track and the analytics the SDK records inside [in-app](/channels/in-app.md).
* **SMS and RCS.** There is no open pixel, but the tracking link that records a [click](/channels/sms-and-rcs.md) resolves on the device's browser and raises the same storage-and-access question once it lands, so click measurement carries a tracking-consent question the bare delivery does not.
* **Wallet and point of sale.** A scanned barcode and pass analytics are first-party and tied to an identity the customer presented, a lighter position than third-party device tracking, but the data is still processed under the GDPR even where Article 5(3) is not engaged. See [wallet passes](/channels/wallet-passes.md) and [point of sale](/channels/point-of-sale.md).
* **Direct mail.** No device, no Article 5(3): the match-back and the per-recipient code are ordinary personal-data processing under the GDPR and nothing more. See [direct mail](/channels/direct-mail.md).

Across all of them, the right to reach someone on a channel never carries the right to measure what they did there. On the device-based channels a platform gate, the tracking prompt, the advertising-identifier phase-out, the push opt-in, sits on top of the legal one; on the channels that never touch the device, only the GDPR's processing rules apply.

## What this means for measurement

This is not only a legal note; it changes how to read your numbers. The bundle already warns that open rate is corrupted by Mail Privacy Protection and is directional at best; see [metrics are directional](/principles/metrics-are-directional.md) and [core metrics](/measurement/core-metrics.md). Tracking consent adds a second, structural source of missingness: in strict-consent jurisdictions a slice of your EU audience may never be measured at all, and that slice is not random, so EU open and click rates understate true engagement and can skew segment and cohort comparisons. The sound response is the one the measurement layer already argues for: lean on outcomes you can observe without the pixel, clicks to first-party destinations, on-site and in-app conversion, and incrementality via [holdouts](/measurement/holdouts-and-control-groups.md), rather than on the open as a primary metric. See [deliverability](/foundations/deliverability.md) for how the open signal degrades on the delivery side too.

## The practical minimum

* Treat tracking consent as a distinct grant from sending consent, captured and recorded separately at the point the address is collected; see the form mechanics in [consent and preferences](/foundations/consent-and-preferences.md).
* Do not bundle pixel consent into the newsletter opt-in or the terms.
* Keep a strictly-necessary tier (deliverability, security) separate from the analytics tier that needs consent, and, where you rely on Italy's exemption, ensure the aggregate count is genuinely anonymised.
* Suppress tracking, not sending, for EU recipients who consent to mail but not to measurement, and design reporting that tolerates an unmeasured EU slice.
* Operate to the strictest regime your list touches, exactly as for sending consent.

## Related

* [Legislation and compliance](/references/legislation-and-compliance.md)
* [Consent and preferences](/foundations/consent-and-preferences.md)
* [Metrics are directional](/principles/metrics-are-directional.md)
* [Core metrics](/measurement/core-metrics.md)
* [Deliverability](/foundations/deliverability.md)
* [Website personalisation](/channels/website-personalisation.md)
* [The channel mix](/channels/index.md)

## Citations

[1] [EDPB, Guidelines 2/2023 on the technical scope of Article 5(3) of the ePrivacy Directive](https://www.edpb.europa.eu/our-work-tools/our-documents/guidelines/guidelines-22023-technical-scope-art-53-eprivacy-directive_en)
[2] [Hogan Lovells, French DPA establishes heightened consent rules for tracking pixels in emails](https://www.hoganlovells.com/en/publications/french-data-protection-authority-establishes-heightened-consent-rules-for-tracking-pixels-in-emails)
[3] [Twilio, consent needed for open tracking pixels: CNIL says yes](https://www.twilio.com/en-us/blog/insights/tracking-consent-cnil-france)
[4] [Covington Global Policy Watch, Italian DPA publishes guidelines on email tracking pixels](https://www.globalpolicywatch.com/2026/05/italian-dpa-publishes-guidelines-on-email-tracking-pixels/)
[5] [A&O Shearman, tracking pixels in emails: the Garante's new guidelines and requirements for businesses](https://www.aoshearman.com/en/insights/tracking-pixels-in-emails-the-garantes-new-guidelines-and-requirements-for-businesses)
[6] [CMS, tracking according to the ePrivacy Directive and German law](https://cms.law/en/deu/insight/e-privacy/tracking-according-to-the-eprivacy-directive-and-german-law)
[7] [Apple, User Privacy and Data Use (App Tracking Transparency and the IDFA prompt)](https://developer.apple.com/app-store/user-privacy-and-data-use/)
[8] [Trackier, GAID and mobile attribution in 2026 (the advertising-identifier phase-out)](https://trackier.com/everything-you-need-to-know-about-gaid/)
