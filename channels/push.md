---
type: Channel
title: Push
description: How to reach a dormant app user with push, choose interruption levels and notification channels, decide push versus in-app versus email, and measure it against a holdout.
tags: [channel, push, apns, fcm, on-device, dormant-users, interruption-levels, re-engagement]
timestamp: 2026-06-14T00:00:00Z
---

## What it is

A push notification is a short message delivered to a device through APNs on iOS or FCM on Android, surfacing on the lock screen or in the notification tray. Its distinctive value is reach: it is the one channel that can pull back a user who has not opened the app in weeks.

## Permission and reach

Permission lives inside a specific install on a specific device, tied to a token the platform can invalidate. Since Android made notification permission an explicit runtime grant, opt in rates have fallen, so the permission is scarce and should be requested in context after showing value, not on first launch. You hold no list you can take elsewhere.

## The pre-permission prompt

The platform permission dialog is effectively one-shot. On iOS a denial can only be reversed by the user in Settings, and Android's runtime grant behaves the same way once dismissed, so firing the OS prompt cold spends the single ask on a user who has no reason yet to say yes. Prime it instead: show your own in-app screen first, framed in the value the user came for, "get told the moment your size is back in stock", and trigger the real OS dialog only after they accept that soft ask. A decline on the soft ask costs nothing, you keep the OS prompt for a better moment and can re-prime later; a decline on the OS prompt is the grant gone. Tie the ask to a moment that earns it, just after the user sets a price alert or completes a first order, not on first launch before any value has landed. The same one-shot trap and the same fix govern every scarce permission you hold, [browser push](/channels/browser-push.md), location, and App Tracking Transparency, and the consent asks on owned channels share the logic; see [consent and preferences](/foundations/consent-and-preferences.md).

## Filtering and editing

Push is the most opaque channel. On recent devices an on-device model can summarise, reorder, and on some surfaces rewrite a notification before the lock screen, and user controls like Focus can suppress it, with no API to tell you which happened. Apple Intelligence and Google's Gemini Nano run these models locally; the dated rollout is in [platform interventions](/references/platform-interventions.md) and the published models in [notification and decisioning research](/references/notification-and-decisioning-research.md).

## Technical specifics

The payload is small and the prioritisation controls are explicit.

* **Payload size.** Both APNs and FCM cap a notification payload at roughly 4KB (4096 bytes); APNs allows 5KB for VoIP. There is no room for a long message, so the proposition has to lead.
* **iOS interruption levels.** Notifications declare one of four levels, passive, active, time-sensitive, and critical. Set the `interruption-level` key in the payload `aps` dictionary. Use them by message type. Passive for things that can wait silently in the tray, a digest or a soft offer, delivered without sound or wake. Active, the default, for ordinary timely notifications. Time-sensitive only for messages the user genuinely needs now, a delivery arriving, a security event, a price alert they set, since it can break through Focus and a scheduled summary; do not use it for marketing, and the user can switch it off per app, which spends trust you will want later. Critical is reserved for safety and health and requires a special Apple entitlement, never available for marketing.
* **Android notification channels.** Since Android 8.0 (Oreo) every notification must be assigned to a channel created at runtime, and the user, not you, controls importance, sound, and behaviour per channel once it exists. Define a small set of meaningful categories the user can reason about, for example transactional, shipping, and offers, so they can mute offers without losing shipping updates, which protects the rest of the opt-in. The risk is in the categorisation, not the count. Over-categorising buries the user in toggles; mis-categorising, routing an offer through a channel the user kept on for transactional messages, gets the whole channel muted and is hard to undo since a channel's importance cannot be raised again in code once the user has set it.
* **Rich and silent push.** Both platforms support media attachments (image, etc.) via a notification service extension, and silent/background pushes that update app state without surfacing to the user.

## Best-fit jobs

Two jobs survive the editor by design. Waking dormant users, which only push can do. And messages tied to the recipient's own activity or requests: a price or back in stock alert they set, a delivery status, a reply on their work, a job that finished. Broadcast promotion competes worst for the interruption budget and usually does more on a surface the user opened on purpose.

## Push versus in-app versus email

The channels do different jobs, so pick by where the user is and how the message earns its interruption. Push to bring an absent user back; it is the only channel that reaches a closed app, so spend it on getting them through the door. In-app to do the work once they are in, where there is room, context, and no interruption tax. Email for rich or non-urgent content, where summary distortion is acceptable and the recipient reads on their own schedule. The default heuristic: if the user is dormant and the message carries enough value to justify breaking into their day, push; if they are active or in session, let [in-app](/channels/in-app.md) carry it; if it is neither urgent nor worth an interruption, email it. When unsure, ask whether the message needs the user to come back right now. If not, it is not a push.

## Re-engaging dormant users

The one job push owns, done in steps. Segment by dormancy rather than blasting the lapsed list, since a user three days quiet and one ninety days gone need different messages and a ninety-day user may have churned for good. Give a concrete reason to return tied to what changed since they left, a price drop on something they viewed, a reply waiting, new content in a topic they followed, not a generic "we miss you" that the editor and the user both discount. Respect quiet hours and send in the recipient's local daytime, and hold frequency down, since a re-engagement push that annoys is the last one before the opt-out. Cap attempts: if a dormancy segment does not respond to a small sequence, stop pushing them and fall back to email, which carries no per-device permission to lose. See [orchestration and frequency](/foundations/orchestration-and-frequency.md).

## Constraints

Visibility is poor and worsening. Confirmed delivery fires when the OS hands the payload to the app, not when the user sees it, so it diagnoses Focus and silent kills, not summarisation. The collapsed view is template bound, so the proposition must lead with the fact. See [copywriting](/foundations/copywriting.md).

## Measurement

Treat the dashboard with doubt. Opens and clicks sit downstream of an editor you cannot see, and conversions are a biased sample of the notifications the platform favoured. The clean read is downstream conversion against a randomised holdout: hold back a slice of the eligible segment, send to the rest, and measure the difference in the action you actually wanted, app return, purchase, task resumed, not the open. That difference is the incremental effect of the push and the only number that survives the editor, since both arms sit behind the same suppression. See [holdouts and control groups](/measurement/holdouts-and-control-groups.md). Note what stays invisible even so: delivery and on-device suppression effects are not reported back. Confirmed delivery fires when the OS takes the payload, not when the user sees it, and Focus suppression, scheduled summaries, and summarisation leave no signal, so the holdout tells you whether the programme worked without telling you why a given send underperformed. Confirm render through the SDK where you can, pool campaigns and lengthen windows, and weight downstream conversion. See [measuring intermediation](/measurement/measuring-intermediation.md).

## Lifecycle role

The re engagement and time critical channel for app audiences. Once the user is back in the app, the [in app](/channels/in-app.md) surfaces take over.

## Related

* [Browser push](/channels/browser-push.md)
* [In-app](/channels/in-app.md)
* [Consent and preferences](/foundations/consent-and-preferences.md)
* [Platform interventions](/references/platform-interventions.md)
* [Copywriting](/foundations/copywriting.md)
* [Orchestration and frequency](/foundations/orchestration-and-frequency.md)
* [Holdouts and control groups](/measurement/holdouts-and-control-groups.md)
* [Measuring intermediation](/measurement/measuring-intermediation.md)

## Citations

[1] [Apple, on-device and server foundation models (~3B-parameter on-device model)](https://machinelearning.apple.com/research/introducing-apple-foundation-models)
[2] [Android Developers, Gemini Nano on-device model](https://developer.android.com/ai/gemini-nano)
[3] [Apple, APNs payload size limit (4KB; 5KB VoIP)](https://developer.apple.com/library/archive/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/CommunicatingwithAPNs.html)
[4] [Firebase, FCM message types and payload size](https://firebase.google.com/docs/cloud-messaging/customize-messages/set-message-type)
[5] [Apple, UNNotificationInterruptionLevel (passive, active, time-sensitive, critical)](https://developer.apple.com/documentation/usernotifications/unnotificationinterruptionlevel)
[6] [Android Developers, create and manage notification channels](https://developer.android.com/develop/ui/views/notifications/channels)
[7] [Apple, asking permission to use notifications (request in response to value, not at launch)](https://developer.apple.com/documentation/usernotifications/asking-permission-to-use-notifications)
