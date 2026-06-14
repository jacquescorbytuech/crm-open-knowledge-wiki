---
type: Channel
title: Browser push
description: How to reach a user through web push when you have no app, prime the browser permission so a cold prompt does not burn it, handle the service-worker and VAPID mechanics, and measure it against a holdout.
tags: [channel, browser-push, web-push, service-worker, vapid, notifications-api, permission-priming, desktop, re-engagement]
timestamp: 2026-06-14T00:00:00Z
---

# What it is

Browser push, or web push, is a notification delivered to a browser through the Web Push protocol and surfaced by the operating system's notification centre even when the site's tab is closed, driven by a service worker registered on your origin. Its distinctive value is reach without an install: it pulls a user back to a web product that has no app, and it is the one CRM channel that lands on the desktop, where mobile push cannot go. It works in Chrome, Firefox, and Edge across desktop and Android, and in Safari on macOS and, since iOS and iPadOS 16.4, for web apps the user has added to the Home Screen.

# Permission and reach

Permission is bound to the specific browser, on the specific device, for your origin, and is granted through the browser's `Notification.requestPermission()` against a secure (HTTPS) context. It is as scarce as the app channels and held in three places at once: a user who granted on desktop Chrome has not granted on their phone or in Firefox, and there is no list you can carry elsewhere, only per-browser subscriptions. Reach is therefore the installed base of granted browsers for your origin, rebuilt on each browser the user brings.

# The pre-permission prompt

The same one-shot trap as mobile [push](/channels/push.md), and sharper. A browser block is sticky and origin-wide, and users almost never revisit per-site browser settings to undo it, so a cold `requestPermission()` on page load does not just convert badly, it can cost the grant for good. Browsers now actively punish cold prompting: Chrome routes prompts from sites with low accept rates or a bad Safe Browsing reputation into a "quieter" UI that suppresses the dialog for everyone, and treats prompts that block content or fire in rapid succession as abusive. Safari refuses outright, the request must come from a user gesture such as a click, so an on-load prompt cannot even fire. The fix is the same priming pattern: show your own in-page invitation tied to a value moment and an explicit click, naming what the user will get, then call the native prompt only when they accept. A no on your soft ask costs nothing and you can ask again; a browser-level block is the channel closed on that browser. See [consent and preferences](/foundations/consent-and-preferences.md).

# Filtering and editing

Lighter on-device rewriting than the mobile lock screen today, but suppression is real and silent: operating-system notification settings, Focus and Do Not Disturb, and the browser's own per-site controls all drop the notification with no signal back. Delivery depends on a background process, the browser, or on Safari a system service, being able to receive, and on Safari web push is routed through Apple's Push Notification service under the hood. As with the app channels, confirmed delivery tells you the push service accepted the payload, not that the user saw it.

# Technical specifics

The plumbing is a small set of web standards, and you talk to a push service, never the device directly.

* **Service worker.** A background script registered on your origin receives the `push` event and calls `showNotification()`. Without a registered service worker there is no web push; it is what lets the notification fire while your site is closed.
* **Subscription and VAPID.** The browser returns a `PushSubscription` with a per-user endpoint URL. You identify your server to the push service with a VAPID key pair (RFC 8292, Voluntary Application Server Identification) so it accepts your messages for that endpoint.
* **Per-browser push services.** Each browser uses its own: Chrome and Edge via FCM, Firefox via Mozilla's autopush, Safari via Apple's APNs. You POST your message to the subscription endpoint and the service relays it; the differences are abstracted by the protocol.
* **Encryption and payload size.** Payloads are encrypted end to end (RFC 8291) and capped at roughly 4KB, so, as with mobile push, the proposition has to lead.
* **iOS caveat.** On iPhone and iPad, web push reaches only a web app the user has added to the Home Screen, not a page open in a Safari tab, and the permission prompt must follow a direct interaction.

# Best-fit jobs

Desktop and no-app re-engagement for web-first products: back-in-stock and price-drop alerts the user asked for, a reply or task update waiting, new content in a topic they followed, and desktop cart recovery. The economics match mobile push, broadcast promotion competes worst for the interruption budget and trains the block, while alerts tied to the user's own request or activity survive it. It is the channel to reach for when the relationship is a logged-in web session with no app behind it.

# Browser push versus mobile push versus email

Pick by where the user is and what you can reach. Mobile [push](/channels/push.md) owns the phone and the dormant app user; browser push owns the desktop and the web user who never installed an app, the gap mobile push cannot cover. They are not redundant, a user can be granted on one and not the other, so treat them as separate grants under one contact strategy rather than a single "push" channel. Against [email](/channels/email.md), browser push is the interruptive, low-capacity option for something timely the user wants now; email carries anything rich or non-urgent and reaches users on no granted browser at all. The default heuristic mirrors the rest of the channel mix: if it is timely and worth an interruption and the user is on a granted browser, push it; otherwise email it.

# Constraints

Fragmentation is the structural cost: the grant is per browser and per device, so the same person is several subscriptions and several separate asks, and the channel only ever reaches the browsers where you earned the prompt. The block is sticky and origin-wide and rarely reversed. Visibility is poor for the same reasons as the app channels, and on iOS the Home-Screen requirement caps reach sharply. The subscription carries no identity on its own, so tie it to a logged-in user at grant time or you hold an anonymous endpoint you cannot reconcile with the customer record.

# Measurement

Read it like the other interruptive, mediated channels: distrust the dashboard and measure the downstream action against a randomised holdout. Hold back a slice of the eligible, granted audience, send to the rest, and measure the difference in the action you wanted, site return, purchase, task resumed, not the click, since opens and clicks sit downstream of suppression you cannot see. Both arms sit behind the same suppression, so the difference is the channel's incremental effect. See [holdouts and control groups](/measurement/holdouts-and-control-groups.md) and [measuring intermediation](/measurement/measuring-intermediation.md).

# Lifecycle role

The web analogue of mobile push: the way back for a user who has no app to receive a notification but keeps returning to the browser. Once the user is on the site, the in-session surfaces take over; see [in-app](/channels/in-app.md).

# Related

* [Push](/channels/push.md)
* [In-app](/channels/in-app.md)
* [Email](/channels/email.md)
* [The channel mix](/channels/index.md)
* [Consent and preferences](/foundations/consent-and-preferences.md)
* [Holdouts and control groups](/measurement/holdouts-and-control-groups.md)

# Citations

[1] [W3C, Push API specification](https://www.w3.org/TR/push-api/)
[2] [MDN, Push API overview](https://developer.mozilla.org/en-US/docs/Web/API/Push_API)
[3] [MDN, Notification.requestPermission()](https://developer.mozilla.org/en-US/docs/Web/API/Notification/requestPermission_static)
[4] [IETF, RFC 8292: Voluntary Application Server Identification (VAPID) for Web Push](https://www.rfc-editor.org/rfc/rfc8292)
[5] [IETF, RFC 8291: Message Encryption for Web Push](https://www.rfc-editor.org/rfc/rfc8291)
[6] [Chromium Blog, introducing quieter permission UI for notifications](https://blog.chromium.org/2020/01/introducing-quieter-permission-ui-for.html)
[7] [Apple, sending web push notifications in web apps and browsers](https://developer.apple.com/documentation/usernotifications/sending-web-push-notifications-in-web-apps-and-browsers)
[8] [WebKit, web push for web apps on iOS and iPadOS (Home Screen requirement)](https://webkit.org/blog/13878/web-push-for-web-apps-on-ios-and-ipados/)
