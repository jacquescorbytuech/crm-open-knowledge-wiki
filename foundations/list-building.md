---
type: Playbook
title: List Building
description: How to build forms, choose single versus double opt in, design a confirmation flow, deliver a lead magnet through automation, and tag acquisition source so it stays attributable.
tags: [list-building, forms, lead-magnets, opt-in, double-opt-in, utm, attribution]
timestamp: 2026-06-14T00:00:00Z
---

## Forms

Build forms natively in your ESP where possible, which removes the data plumbing failure point. A good form has six essentials: a clear value proposition headline (what the subscriber gets, specifically), the right expectations (frequency and content type), a clear action oriented CTA, clear field labels rather than placeholder text alone, minimal fields, and a brief human privacy assurance. Always test on mobile.

Fewer fields convert better, so collect the minimum that makes the subscriber usable and ask for the rest later through progressive profiling. To do that concretely:

1. Order fields by how much each one costs the subscriber to give and how much you need it now. Email first, then at most one field you will actually use to personalise the first send.
2. At the start, capture email only. A name field is optional, not default; add it only if your first email genuinely uses it.
3. Defer everything else. Collect preferences, segment data, and qualifying detail later through a preference centre, follow up emails, or behaviour, not the signup form. See [consent and preferences](/foundations/consent-and-preferences.md) and [segmentation and data](/foundations/segmentation-and-data.md).

Be deliberate about mode. A handful of fields is collecting subscribers; many fields is qualifying leads, and you should only do the second when sales need the qualification.

## Placement

Rank placements by the intent of the moment they fire, not by how prominent they are. Inline forms inside relevant content and exit intent overlays catch a reader who has already engaged, so they convert better than a form buried in the footer or sidebar that nobody is looking for. Order to reach for, highest intent first:

1. In content embedded forms, placed next to the content that earned the interest.
2. Exit intent overlays, fired as the visitor leaves a page they engaged with.
3. Timed or scroll triggered popups, shown once the visitor has read enough to want more.
4. Permission priming overlays and sticky banners, which set up a later ask.
5. Footer or sidebar forms, the fallback for visitors who go looking.

Off site, use link in bio tools, Meta lead generation ads, video callouts, and QR codes to tracked landing pages. Run several placements at once rather than relying on one form in one location, and tag each so you can tell which earns subscribers (see [Source tracking](#source-tracking)).

## Lead magnets

A lead magnet is an incentive offered for contact details. Good ones are relevant (they attract your actual target profile), useful (they solve a real problem), and valuable (not freely available elsewhere). Avoid discount code lead magnets: they inflate signups with deal seekers who churn immediately, which works against [list quality over size](/principles/list-quality-over-size.md) and the discipline in [offers and incentives](/foundations/offers-and-incentives.md). Deliver on the lead magnet promise in the first email, without exception.

## Delivering the lead magnet

Deliver the magnet through automation, not by hand, so it arrives instantly while intent is highest. Wire the capture to an event the ESP can trigger on:

1. The signup writes the new contact and a tag or field marking which magnet they asked for.
2. That signup event triggers an automation. With double opt in, the confirmation click is the trigger; with single opt in, the form submission is.
3. The first email delivers the magnet (the asset, a link, or the promised content) immediately, with no marketing wrapped around it.
4. The same automation drops them into the welcome sequence so the magnet email is step one, not a dead end. See [automation and sequences](/foundations/automation-and-sequences.md) and [the welcome window](/principles/the-welcome-window.md).

Branch the sequence on which magnet was requested where the magnets imply different interests, so the welcome content matches what they signed up for.

## Single versus double opt in

Single opt in adds the subscriber the moment the form is submitted. Double opt in adds them only after they click a confirmation link in a follow up email, which proves the address is real and the consent is theirs. Choose by what you are optimising for:

| Priority | Recommendation |
| --- | --- |
| List quality and deliverability | Double opt in |
| GDPR regulated jurisdiction | Double opt in, for the consent record |
| Volume growth where single opt in is the norm | Single opt in, with strong bounce management |
| Ecommerce with incentivised signups | Single opt in, with careful bounce suppression |

## The double opt in flow

When you run double opt in, the confirmation is a short flow, not just one email:

1. On submit, create the contact in a pending or unconfirmed state. Do not send them marketing yet, and do not count them as a subscriber.
2. Send the confirmation email immediately. One clear purpose, one button, restating what they signed up for so the click is informed consent.
3. The confirmation link sets the contact to confirmed and stamps the consent record (timestamp, source, and what they agreed to). See [consent and preferences](/foundations/consent-and-preferences.md).
4. Confirmation is the trigger that delivers the lead magnet and starts the welcome sequence (see [Delivering the lead magnet](#delivering-the-lead-magnet)).
5. Set the link to expire after 24 to 48 hours and send one reminder before it lapses. Unconfirmed contacts get no marketing and should be purged on a schedule so they never inflate list size or skew engagement rates.

## Source tracking

Knowing where a subscriber came from is as valuable as knowing how many you have. Use UTM parameters, dedicated landing pages, hidden form fields, custom ESP fields, and QR codes, and combine methods because attribution is always incomplete. Use a consistent naming convention from day one, or the data is useless within months.

Fix a convention and apply it everywhere. The standard UTM trio carries it:

* `utm_source`, where the click came from (the platform or site): `instagram`, `newsletter`, `partner-site`.
* `utm_medium`, the channel type: `social`, `email`, `cpc`, `qr`.
* `utm_campaign`, the specific effort or magnet: `2026-spring-guide`, `exit-popup-pricing`.

Lock the rules so the values stay clean: lowercase only, hyphens not spaces, a fixed vocabulary for source and medium, and a date or theme in the campaign. A full example tag on an Instagram bio link to a guide download:

```
https://example.com/guide?utm_source=instagram&utm_medium=social&utm_campaign=2026-spring-guide
```

Capture those values into hidden form fields so they land on the contact record as the acquisition source, alongside the magnet tag from [Delivering the lead magnet](#delivering-the-lead-magnet). Now every subscriber carries where they came from, what brought them in, and which sequence they entered, which is what makes acquisition source attributable later.

## Related

* [List quality over size](/principles/list-quality-over-size.md)
* [The welcome window](/principles/the-welcome-window.md)
* [Offers and incentives](/foundations/offers-and-incentives.md)
* [Segmentation and data](/foundations/segmentation-and-data.md)
* [Consent and preferences](/foundations/consent-and-preferences.md)
* [Automation and sequences](/foundations/automation-and-sequences.md)

## Citations

[1] [Baymard Institute, fewer form fields reduce abandonment](https://baymard.com/blog/checkout-flow-average-form-fields)
[2] [Mailjet, double opt-in improves list quality, deliverability, and gives a consent record](https://www.mailjet.com/blog/deliverability/double-opt-in-should-i-or-shouldnt-i/)
[3] [The Good, discount-led acquisition attracts bargain hunters who churn](https://thegood.com/insights/discounting-for-ecommerce/)
