---
type: Reference
title: Personalisation Mechanics
description: How a personalised value is resolved into a message: the templating languages that express it, and the range from profile-attribute substitution fixed at send, through external content fetched as the send renders, to live content resolved at the moment of open, with the freshness-versus-fragility trade each point on the timeline carries.
tags: [personalisation, dynamic-content, merge-tags, templating, liquid, connected-content, open-time, live-content]
timestamp: 2026-06-15T00:00:00Z
---

## Where the value comes from and when it resolves

[Decisioning](/foundations/decisioning-and-personalisation.md) chooses what goes in a slot. The mechanics here resolve an actual value into it, and where a given method lands comes down to where the value is drawn from, a profile attribute, an external system, a computation, and when it resolves, as the send is composed, as it renders, or at the moment the recipient opens. Those sort the personalisation methods on a feature sheet, and predict their failure modes better than the vendor's name for them does.

## The expression layer: templating languages

Every personalised message is, underneath, a template: static markup with placeholders and logic that a rendering engine resolves per recipient. The language that template is written in is the substrate the rest of this sits on, and each engagement platform ships its own. Salesforce Marketing Cloud has `AMPscript`, with `GTL` (Guide Template Language) and server-side JavaScript (`SSJS`) alongside it for heavier logic. Braze uses `Liquid`. Iterable uses `Handlebars`. Marketo runs Apache `Velocity` for its email scripting. Each platform picks a base syntax and extends it with its own functions, so a template is rarely portable between them even when the `{{ }}` placeholders look alike.

A merge field is the simplest expression in that language, a placeholder swapped for subscriber data: `Hi {{ first_name }}`. The same language also carries the logic that makes personalisation more than substitution: conditionals (`{% if %}`), loops over a collection (`{% for item in cart %}`), filters that transform a value (`{{ price | money }}`), and the fallback that protects against missing data (`{{ first_name | default: "there" }}`). Dynamic-content blocks, regions that show different markup to different audiences, are the same conditional logic applied to a layout instead of a word. The discipline of testing all of this, the blank-merge check, fallback coverage, and branch audit, lives in [segmentation and data](/foundations/segmentation-and-data.md); it is the same check whether the value is a name or a whole block.

Templating is the *how-expressed* layer and is largely independent of when the value resolves. The same `{{ }}` syntax can hold a profile attribute fixed at send or an external value fetched mid-render.

## Binding time, earliest to latest

* **Profile-attribute substitution.** The value is a stored property, first name, loyalty tier, last order, read from the [customer record](/foundations/customer-data-and-identity.md) and written into the message as the send is composed. It is the cheapest and most reliable method and the easiest to get subtly wrong: a tag mapped to the wrong field renders a real but incorrect value that no blank-check catches, and a missing attribute renders the fallback or, without one, `Hi ,`. Whatever it resolves to is frozen at send and correct only as long as the attribute was.

* **Relational or connected data.** A richer form of the same send-time method reaches past flat profile fields into related datasets the platform holds: tables of a contact's orders, catalogue items, or loyalty events, joined into personalisation and segmentation at render without an external call. Emarsys exposes this as connected (relational) data, MessageGears by querying the customer's own data warehouse directly at send, Braze through catalogs, among others. It stays first-party and resolves at send, sourced from a join rather than a single field, so it can loop over related rows (`{% for item in last_order %}`) and segment on conditions a flat profile cannot hold, such as a purchase from a given category in the last 30 days.

* **External content fetched at send.** Instead of a stored attribute, the template calls out to a live source as it renders, an inventory or pricing endpoint, a recommendation engine, a content API, and drops the response into the slot. `AMPscript`'s `HTTPGet` and `Lookup` and Braze's `Connected Content` are two examples; most platforms expose some equivalent under their own name. This gives a value current at send rather than whenever the profile was last updated, at the cost of fragility: the call adds latency to every render in a large send, and a timeout or error returns nothing, so the method is only as safe as its default value and its timeout handling. The freshness window is still the send, not the open; a price fetched at send is stale by the time a message is opened a day later.

* **Live content resolved at open.** The message embeds an image whose URL is requested only when the client loads it, and the server generating that image decides its content at request time: a countdown that is accurate when seen, a price or stock level current at the open, a map or weather tied to the recipient's context. Movable Ink and similar tools build on this. It is the freshest of these and the most constrained, because everything it personalises lives inside an image.

## The cost of resolving later

All of them trade freshness against reliability. A profile attribute is cheap and almost always renders, but its value can be out of date by the time it is read. An external fetch is current at send but adds a call that can time out. An open-time image is current when it is seen but depends on a chain of steps that can each break. Resolving later in the timeline gains freshness and adds points where the render can fail.

Open-time content carries the sharpest version of that cost, because it collides with rules that hold elsewhere in the programme. The substance of a message belongs in live text, not locked in an image, since [images are blocked by default in many clients](/foundations/message-design-and-rendering.md) and an image of an offer renders as an empty box and reads as nothing under a screen reader. Open-time personalisation requires the value to be an image, so it can only safely carry content that is secondary or decorative, never the only copy of the offer or the call to action.

It also breaks mechanically. Apple's Mail Privacy Protection prefetches images when a message is received rather than when it is opened, so the request that was meant to resolve at the open resolves at the proxy instead, at a time and from a network that are not the recipient's: the countdown freezes at prefetch, the location resolves to a data centre, and open tracking breaks in the same stroke. Image caching does the rest. Mailbox providers route images through their own proxies (Gmail through `googleusercontent.com`) and cache the fetched copy, so a live image that does not defeat the cache is rendered once and then served stale to every later open, even the same recipient reopening. Live-content tools work around this with a unique URL per request and `Cache-Control: no-store` headers, but the technique only pays off for the share of the audience whose client fetches images live and uncached, which is a shrinking one. See [deliverability](/foundations/deliverability.md).

## The same axes in other channels

These examples are drawn from email, but the source axis is channel-independent and the binding-time axis just shifts with each channel's rendering model. What changes is the latest moment a channel still lets you influence the render, and that sorts them.

* **Direct mail** is fixed at print, the earliest point and the only irreversible one. [Variable-data printing](/channels/direct-mail.md) is profile-attribute substitution rendered onto a physical page and then frozen for the days of transit, with no fallback once the press has run, so it can only safely personalise on data stable enough to survive the gap between print and delivery.
* **Email** resolves at send, with open-time live content as the fragile extension drawn above: image-only, and undercut by proxy prefetch.
* **SMS, RCS, and push** resolve at send. The platform still runs its templating dialect on the body, so profile attributes and send-time fetch apply, but there is no render-time hook to resolve content later, and the hard length limit, the [SMS segment](/channels/sms-and-rcs.md) and the lock-screen truncation on [push](/channels/push.md), constrains how much personalisation fits before it matters which method produced it.
* **In-app and onsite** resolve at view, in a live client session. This is open-time resolved properly: the device is genuinely present, so content settles at the real moment of viewing with no prefetch proxy in the way. [In-app](/channels/in-app.md) and web are where real-time personalisation engines render content live, which email can only imitate with an image.

Open-time live content is really render-time resolution on a live client. Email has no live session to render into, so it imitates this with an image and a prefetch-prone request; in-app and web have a live session and resolve content in it directly; direct mail has no render step at all.

A value's source should resolve the same across all of them, the same `loyalty_tier` in an email, an SMS, and an onsite block, but the dialect that expresses it is per-platform, so the logic is rebuilt in each channel even when the data behind it is shared. That rebuild is an [orchestration](/foundations/orchestration-and-frequency.md) cost as much as a mechanics one.

## The recipient's side of resolving at open

The open-time image request is also a disclosure. It reports that the message was opened and can carry the recipient's IP, rough location, device, and the time, the same surface that an open-tracking pixel exposes, now carrying the content as well as the metric. A method that resolves at open necessarily signals that the open happened. That is defensible when the personalisation serves the recipient, a delivery window, a genuinely current price, and harder to defend when the same channel is used to time pressure against them. What separates personalisation a recipient would accept from personalisation aimed against them is the objective it serves, the same distinction drawn in [decisioning](/foundations/decisioning-and-personalisation.md).

## How this sits with decisioning and rendering

These layers stack rather than compete. [Decisioning](/foundations/decisioning-and-personalisation.md) chooses what should fill a slot, a rules engine picking a segment's block or a bandit picking a per-customer offer. The mechanics here insert the chosen value into the message and fix when it resolves. [Message design and rendering](/foundations/message-design-and-rendering.md) decides whether the result displays intact across the client spread. A single email routinely uses all of them at once: a templated greeting from a profile attribute, a conditional block chosen by a segment, a recommendation module fetched from an API at send, and a countdown rendered at open, each resolving at a different point and each with its own way of failing.

## Related

* [Decisioning and personalisation](/foundations/decisioning-and-personalisation.md)
* [Segmentation and data](/foundations/segmentation-and-data.md)
* [Customer data and identity](/foundations/customer-data-and-identity.md)
* [Message design and rendering](/foundations/message-design-and-rendering.md)
* [Orchestration and frequency](/foundations/orchestration-and-frequency.md)
* [Direct mail](/channels/direct-mail.md)
* [In-app](/channels/in-app.md)
* [Deliverability](/foundations/deliverability.md)

## Citations

[1] [Salesforce, AMPscript for Marketing Cloud Engagement](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/ampscript.html)
[2] [Salesforce, AMPscript HTTPGet (retrieve content from an external URL at send)](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/httpget.html)
[3] [Braze, Liquid personalisation and supported tags](https://www.braze.com/docs/user_guide/personalization_and_dynamic_content/liquid)
[4] [Iterable, Handlebars personalisation syntax](https://support.iterable.com/hc/en-us/articles/205480275-Personalizing-Messages-with-Handlebars)
[5] [Marketo, Velocity email scripting (the Email Script token)](https://experienceleague.adobe.com/en/docs/marketo/using/product-docs/email-marketing/dynamic-content/velocity)
[6] [Braze, Connected Content (call an external API at message render time)](https://www.braze.com/docs/user_guide/personalization_and_dynamic_content/connected_content)
[7] [Emarsys, relational data (related data tables for personalisation and segmentation)](https://help.emarsys.com/hc/en-us/articles/115004845945)
[8] [MessageGears, warehouse-native messaging (personalise directly from the customer's data warehouse)](https://www.messagegears.com/)
[9] [Movable Ink, open-time / activate-on-open personalisation](https://movableink.com/)
[10] [Litmus, real-time and live content in email](https://www.litmus.com/blog/how-to-use-real-time-personalization-in-email)
[11] [Apple, Mail Privacy Protection (prefetches remote content at receipt)](https://support.apple.com/guide/iphone/protect-your-email-activity-iph2af30b8be/ios)
