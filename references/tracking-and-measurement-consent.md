---
type: Reference
title: Tracking and Measurement Consent
description: Why the right to track is a separate permission from the right to send, resting on the GDPR, which governs the tracking data as personal data, together with Article 5(3) of the ePrivacy Directive where the measurement reads or writes on the device, read through the 2026 French and Italian rulings on email tracking pixels, and how the split runs across web, app, push and the other channels.
tags: [legislation, compliance, gdpr, eprivacy, tracking-pixel, consent, cnil, garante, measurement, cookies, app-tracking, att]
generated:
  by: human:jacquescorbytuech
  at: 2026-06-14T00:00:00Z
stale_after: 2027-08-20
sources:
  - id: edpb-guidelines-2-2023-on-the-technical
    resource: https://www.edpb.europa.eu/our-work-tools/our-documents/guidelines/guidelines-22023-technical-scope-art-53-eprivacy-directive_en
    title: "EDPB, Guidelines 2/2023 on the technical scope of Article 5(3) of the ePrivacy Directive"
  - id: hogan-lovells-french-dpa-establishes-heightened-consent
    resource: https://www.hoganlovells.com/en/publications/french-data-protection-authority-establishes-heightened-consent-rules-for-tracking-pixels-in-emails
    title: "Hogan Lovells, French DPA establishes heightened consent rules for tracking pixels in emails"
  - id: twilio-consent-needed-for-open-tracking-pixels
    resource: https://www.twilio.com/en-us/blog/insights/tracking-consent-cnil-france
    title: "Twilio, consent needed for open tracking pixels: CNIL says yes"
  - id: covington-global-policy-watch-italian-dpa-publishes
    resource: https://www.globalpolicywatch.com/2026/05/italian-dpa-publishes-guidelines-on-email-tracking-pixels/
    title: "Covington Global Policy Watch, Italian DPA publishes guidelines on email tracking pixels"
  - id: a-o-shearman-tracking-pixels-in-emails
    resource: https://www.aoshearman.com/en/insights/tracking-pixels-in-emails-the-garantes-new-guidelines-and-requirements-for-businesses
    title: "A&O Shearman, tracking pixels in emails: the Garante's new guidelines and requirements for businesses"
  - id: cms-tracking-according-to-the-eprivacy-directive
    resource: https://cms.law/en/deu/insight/e-privacy/tracking-according-to-the-eprivacy-directive-and-german-law
    title: "CMS, tracking according to the ePrivacy Directive and German law"
  - id: apple-user-privacy-and-data-use-app
    resource: https://developer.apple.com/app-store/user-privacy-and-data-use/
    title: "Apple, User Privacy and Data Use (App Tracking Transparency and the IDFA prompt)"
  - id: trackier-gaid-and-mobile-attribution-in-2026
    resource: https://trackier.com/everything-you-need-to-know-about-gaid/
    title: "Trackier, GAID and mobile attribution in 2026 (the advertising-identifier phase-out)"
  - id: edpb-opinion-5-2019-on-the-interplay
    resource: https://www.edpb.europa.eu/our-work-tools/our-documents/opinion-board-art-64/opinion-52019-interplay-between-eprivacy_en
    title: "EDPB, Opinion 5/2019 on the interplay between the ePrivacy Directive and the GDPR"
---

> [!caution] This is not legal advice
> This orients you to a fast-moving area; it is not legal advice. These rulings are recent and obligations turn on where your recipients are. Take qualified advice for your specific situation.

See [legislation and compliance](/references/legislation-and-compliance.md) for the sending-consent regimes this sits alongside.

## Two different consents: to send, and to track

Most compliance discussion is about the right to *send*: may you put a marketing message in this person's inbox. That is governed by [PECR, the GDPR, CAN-SPAM and the rest](/references/legislation-and-compliance.md). There is a second, separate question that owned-channel programmes routinely overlook: may you *track* what the recipient does with the message, the open pixel that fires when images load and the redirect that records a click.

In the EU these are not the same permission, and tracking is not governed by a single regime that replaces the one behind sending. The GDPR governs both. Sending a marketing message and measuring what the recipient does with it are each processing of personal data, so each needs its own lawful basis and has to respect the GDPR's principles and rights. What sets tracking apart is a further requirement that applies only when the measurement touches the device. An open pixel reads from and writes to the recipient's device exactly as a cookie does, so it also falls under **Article 5(3) of the ePrivacy Directive**, the provision behind the cookie banner, and that rule requires prior consent for the access in its own right. Tracking that reaches the device therefore needs both Article 5(3) consent and a GDPR basis; tracking that never touches the device, such as a server-side click redirect, needs only the GDPR basis.

> [!important] The right to send is not the right to track
> You can have a clean, fully consented right to email someone and still have no lawful basis to measure their opens.

## The Article 5(3) baseline

Article 5(3) of the ePrivacy Directive requires consent before storing information on, or accessing information already stored on, a user's terminal equipment, unless it is strictly necessary to provide a service the user requested. The European Data Protection Board's **Guidelines 2/2023** on the technical scope of Article 5(3) confirmed that the provision is technology-neutral and reaches email tracking pixels, not only browser cookies. Because every EU and EEA member state transposes the same directive, this baseline applies across the bloc, and national authorities cite each other's reasoning when they apply it.

So an open pixel in the EU is presumptively a consent activity under Article 5(3), with a narrow strictly-necessary exemption, regardless of how solid your sending consent is.

Article 5(3) applying does not remove the GDPR; both govern the same measurement. Recording who opened or clicked is processing of personal data, so it always needs a lawful basis under Article 6 and must meet the GDPR's transparency, purpose-limitation and data-subject-rights obligations. Where Article 5(3) requires consent for the access to the device, that consent is also the operative GDPR basis for the collection: the EDPB's **Opinion 5/2019** on the interplay between the two instruments treats Article 5(3) as the more specific rule, so you cannot place the pixel on consent and then reclassify the same collection as legitimate interest to avoid the consent requirement. Click tracking runs the other way. It usually works by rewriting the link through a redirect that logs the click on the server before forwarding, which stores and reads nothing on the recipient's device, so Article 5(3) is not necessarily engaged. The GDPR still is, because the click tied to a person is personal data. Every open and click therefore raises a GDPR question; the open pixel raises an ePrivacy one as well.

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

The email pixel is one instance of a rule that is not about email. On any channel, measurement tied to an identifiable person is processing of personal data, so the GDPR applies, which is why the permission to reach someone and the permission to measure them are separate grants everywhere, device or not. Article 5(3) is the added requirement, and it applies wherever the measurement stores information on, or reads information already on, the recipient's device. EDPB Guidelines 2/2023 read that as technology-neutral, and the terminal equipment it protects is the smartphone, laptop or connected TV, not the inbox. So where the measurement touches the device, ePrivacy requires consent for the access as well as the GDPR obligations; where it does not, only the GDPR applies. The channels differ mainly in how much of the measurement touches the device.

* **Web and onsite.** Cookies, local storage and browser fingerprinting are the original case of Article 5(3), and the consent banner is where that access is asked for. Not all web measurement is that: server-side analytics and first-party server logs that record a page view or an on-site click without reading or writing the visitor's device raise no Article 5(3) question, only the GDPR one, the same split the email click follows. Where the device is read and consent is refused, the visitor cannot be profiled, a legal cap on what [website personalisation](/channels/website-personalisation.md) can do rather than a technical one, and it is the same grant the email pixel needs, asked at a different surface.
* **Mobile app, push and in-app.** An app SDK that reads a device identifier or writes to local storage falls squarely within Article 5(3), and platform rules add a gate of their own: Apple's App Tracking Transparency requires a prompt before an app may access the IDFA to track across apps, and Android has been moving to restrict its advertising identifier on a similar path. Event tracking the app reports server-side against a signed-in account, without reading device storage, may not engage Article 5(3), but the GDPR governs it as it governs any behavioural data. The OS permission to send a [push](/channels/push.md) is a separate grant again, distinct from the right to track and from the analytics the SDK records inside [in-app](/channels/in-app.md).
* **SMS and RCS.** There is no open pixel. A tracking link records the [click](/channels/sms-and-rcs.md) on the redirect server as it resolves, which stores and reads nothing on the device, so Article 5(3) is not necessarily engaged the way it is for a pixel. The GDPR is: the click tied to a number is personal data, so click measurement still needs a lawful basis and clear disclosure even where ePrivacy requires no consent for it.
* **Wallet and point of sale.** A scanned barcode and pass analytics are first-party and tied to an identity the customer presented, a lighter position than third-party device tracking, but the data is still processed under the GDPR even where Article 5(3) is not engaged. See [wallet passes](/channels/wallet-passes.md) and [point of sale](/channels/point-of-sale.md).
* **Direct mail.** No device, no Article 5(3): the match-back and the per-recipient code are ordinary personal-data processing under the GDPR and nothing more. See [direct mail](/channels/direct-mail.md).

Across all of them, the right to reach someone on a channel never carries the right to measure what they did there. The GDPR governs the measurement data on every channel. On the device-based channels Article 5(3) adds a consent requirement for the device access, and a platform gate, the tracking prompt, the advertising-identifier phase-out or the push opt-in, is a further condition again; on the channels that never touch the device, only the GDPR's processing rules apply.

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
