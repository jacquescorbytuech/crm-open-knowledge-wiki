---
type: Channel
title: Website personalisation
description: How to use your own website as a CRM surface: adapt content and show messages to a live visitor who is anonymous until resolved, deploy it without the flicker tax, decide onsite versus in-app versus browser push, and measure it by onsite experiment against a control.
tags: [channel, website, onsite, web-personalisation, experimentation, anonymous, identity-resolution, flicker, recommendations]
timestamp: 2026-06-15T00:00:00Z
---

## What it is

Website personalisation is your own site used as a delivery surface: a hero or banner swapped for the visitor, product and content recommendations, an overlay or inline prompt, a returning-visitor greeting, the order of a listing reranked to the person looking at it. The content settles in a live browser session at the moment of view, which makes it the web counterpart of [in-app](/channels/in-app.md), with one difference that governs everything else: most of the traffic is anonymous.

The decisioning that chooses what fills a slot lives in [decisioning and personalisation](/foundations/decisioning-and-personalisation.md), and the mechanics that resolve a value into it live in [personalisation mechanics](/foundations/personalisation-mechanics.md), where onsite is the case that resolves cleanly at view because the client is genuinely present. Onsite is the surface those render onto: how the web session reaches the visitor, what mediates it, and how it is deployed and measured.

## Permission and reach

Reach is the live visitor, and only the live visitor. Like in-app the channel acts on a session the person started and cannot initiate contact, so it reaches nobody who is not currently on the site. The harder limit is identity: a first-time or logged-out visitor is an anonymous browser, known only by a cookie or device signal, so until they sign in or are matched, personalisation runs on contextual and in-session signals, the referrer, the geo, the campaign they arrived on, what they have viewed this visit, not on the [customer record](/foundations/customer-data-and-identity.md). The record only comes into play once identity resolves, which makes turning the anonymous visit into a known one one of the channel's primary jobs rather than a precondition.

Whether an anonymous visitor can be tracked at all is a consent question before it is a technical one. The same Article 5(3) cookie-consent regime set out in [tracking and measurement consent](/references/tracking-and-measurement-consent.md) governs the cookies and device signals onsite personalisation reads, so a visitor who declines tracking consent cannot be profiled and falls into the anonymous tail by law, not merely by being new. Third-party signal decay erodes the same targeting surface further over time.

## Filtering and editing

None in the delivery path, in the sense the channel mix means it: nothing ranks, bundles, or suppresses what you render, because it is your own page and the visitor is looking straight at it. The mediation is technical rather than editorial. The variant has to be computed and applied before or as the page paints, and the browser, the network, and your own tag are what stand between the decision and the pixels. That absence of an editor is what makes onsite, like in-app, a surface where a clean experimental read is possible, because both arms see the same unmediated page.

## Technical specifics

The channel is deployed into the page and the engineering question that dominates it is how to change the page without the visitor seeing the change happen.

* **Deployment.** A JavaScript snippet or SDK, usually dropped through a tag manager, loads the personalisation tool and lets it rewrite the page client-side; alternatively the variant is composed server-side and the page arrives already personalised. This is the home of the experience-optimisation tool category (Adobe Target, Optimizely, Dynamic Yield, VWO, and the like), which bundles personalisation with the onsite experiment runner.
* **Client-side versus server-side, and flicker.** Client-side rewriting is fast to deploy but causes flicker, the flash of original content, where the default page paints first and visibly snaps to the variant a moment later. Tools suppress it with a pre-hiding snippet that hides the page until the variant is ready, which trades the flicker for a delay and puts the tool on the critical path of page load. Server-side rendering avoids flicker entirely but needs engineering to build, so the choice is a page-speed and flicker trade, not a free one.
* **Identity resolution onsite.** The visitor starts as an anonymous cookie or device id and is stitched to the known record on sign-in, on a click-through from an addressed [email](/channels/email.md) or [SMS](/channels/sms-and-rcs.md) that carries an identifier, or by a match against a profile. Before that stitch, only the in-session and contextual signals above are available; after it, the full record is.
* **What renders.** Hero and banner swaps, recommendation and merchandising modules, inline content blocks chosen by segment, overlays and popups (welcome, exit-intent, promotional), and the rerank of a listing or search result. All of it resolves at view in the live session, with no prefetch proxy in the way, which is the property email cannot match.
* **Generative content, and its limit.** Large language models now author the variants, the copy, headlines, and whole page drafts, that the runner then deploys and tests, which is mature and widely shipped. Generating the page at finer grain is newer: tools generate a page per account or per ad intent ahead of the visit, pre-rendered and reviewable, which is selling into B2B account-based marketing. Generating a unique page live for the individual visitor stays largely experimental, held back by the generation call landing on the render critical path on top of flicker, by the brand-safety problem of shipping unvetted copy to a live commercial page, and by a measurement cost: a page unique to each visitor cannot be run against itself, so the clean onsite experiment collapses to a coarser generated-versus-control holdout.

## Best-fit jobs

Converting anonymous traffic, the welcome offer and email capture that turn a first visit into a consented, addressable contact, which feeds [list building](/foundations/list-building.md); merchandising and recommendations for the in-session shopper; recognising and re-orienting a returning or known visitor; and landing-page continuity, matching the page to the offer and creative the visitor clicked from so the campaign does not break at the door. It is also the native home of onsite experimentation, where layout and content tests run. Its worst job is anything aimed at someone who is not on the site, which is the job of the send-based channels and of [browser push](/channels/browser-push.md).

## Website versus in-app versus browser push

They split by where the visitor is and whether they are reachable. Onsite and [in-app](/channels/in-app.md) are the live owned surfaces and do the in-session work, the difference being that in-app acts on an authenticated user inside your product while onsite acts on a largely anonymous web visitor, so identity resolution is a job onsite owns and in-app mostly assumes. [Browser push](/channels/browser-push.md) is the web channel that reaches back out to a granted browser when the visitor has gone, the way to bring them to the site so onsite can do its work. The default: if the visitor is on the site, let onsite carry it; if they have left and you need them back, that is a browser push or an email, not an onsite change.

## Constraints

The anonymous tail is the structural limit, a large share of visitors you cannot tie to a record and can only personalise to on session signals. Client-side deployment buys speed at the cost of flicker, and the fix for flicker costs page-load time on the critical path, which is itself a conversion cost. The render depends on the visitor's tracking consent and on signals that are degrading, it reaches only the active visitor, and it cannot initiate contact.

## Measurement

The cleanest experimental surface alongside in-app, because the tooling is built around the test. Read it with an onsite A/B or holdout: split eligible traffic, show the variant to one arm and the unchanged page to the other, and measure the difference in the action you wanted. Read the response metric, conversion or click on the module, but watch the guardrails beside it, bounce rate, page-load time, and overall conversion, because a personalisation can lift its own module's click while a heavy anti-flicker snippet slows the page and costs more conversions than the module wins. The discipline is the same one in [holdouts and control groups](/measurement/holdouts-and-control-groups.md) and [uplift and incrementality](/measurement/uplift-and-incrementality.md); the advantage onsite has is that the unmediated page makes both arms clean.

## Lifecycle role

The acquisition and conversion surface for web traffic, and the landing surface the other channels drive toward, the place a click from email, push, or an ad is received and continued. It is where the anonymous visitor becomes a known one, the same identity-resolution role the [point of sale](/channels/point-of-sale.md) plays in store, and it pairs with [browser push](/channels/browser-push.md) the way in-app pairs with push: one reaches back out, the other does the work once the visitor arrives. It holds nothing between visits; that is the send-based channels' job.

## Related

* [The channel mix](/channels/index.md)
* [In-app](/channels/in-app.md)
* [Browser push](/channels/browser-push.md)
* [Decisioning and personalisation](/foundations/decisioning-and-personalisation.md)
* [Personalisation mechanics](/foundations/personalisation-mechanics.md)
* [Customer data and identity](/foundations/customer-data-and-identity.md)
* [Tracking and measurement consent](/references/tracking-and-measurement-consent.md)
* [List building](/foundations/list-building.md)
* [Holdouts and control groups](/measurement/holdouts-and-control-groups.md)

## Citations

[1] [Adobe, Target and flicker / the pre-hiding snippet](https://experienceleague.adobe.com/en/docs/target/using/implement-target/client-side/how-at-js-works/manage-flicker-with-at-js)
[2] [Optimizely, the anti-flicker snippet for client-side experiments](https://support.optimizely.com/hc/en-us/articles/4410289706253-Use-the-anti-flicker-snippet)
