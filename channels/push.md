---
type: Channel
title: Push
description: The only channel that reaches a dormant app user, edited on device by a model before it reaches the lock screen, with poor sender visibility.
tags: [channel, push, apns, fcm, on-device, dormant-users]
timestamp: 2026-06-14T00:00:00Z
---

# What it is

A push notification is a short message delivered to a device through APNs on iOS or FCM on Android, surfacing on the lock screen or in the notification tray. Its distinctive value is reach: it is the one channel that can pull back a user who has not opened the app in weeks.

# Permission and reach

Permission lives inside a specific install on a specific device, tied to a token the platform can invalidate. Since Android made notification permission an explicit runtime grant, opt in rates have fallen, so the permission is scarce and should be requested in context after showing value, not on first launch. You hold no list you can take elsewhere.

# Filtering and editing

Push is the most opaque channel. On recent devices an on-device model can summarise, reorder, and on some surfaces rewrite a notification before the lock screen, and user controls like Focus can suppress it, with no API to tell you which happened. Apple Intelligence and Google's Gemini Nano run these models locally; the dated rollout is in [platform interventions](/references/platform-interventions.md) and the published models in [notification and decisioning research](/references/notification-and-decisioning-research.md).

# Technical specifics

The payload is small and the prioritisation controls are explicit.

* **Payload size.** Both APNs and FCM cap a notification payload at roughly 4KB (4096 bytes); APNs allows 5KB for VoIP. There is no room for a long message, so the proposition has to lead.
* **iOS interruption levels.** Notifications declare one of four levels, passive, active, time-sensitive, and critical. Time-sensitive can break through Focus but must not be used for marketing, and the user can switch it off per app. Critical is reserved and entitlement-gated.
* **Android notification channels.** Since Android 8 every notification must be assigned to a channel, and users control importance, sound, and behaviour per channel. Split your notifications into meaningful channels so a user can mute transactional reminders without muting everything, which protects the opt-in.
* **Rich and silent push.** Both platforms support media attachments (image, etc.) via a notification service extension, and silent/background pushes that update app state without surfacing to the user.

# Best-fit jobs

Two jobs survive the editor by design. Waking dormant users, which only push can do. And messages tied to the recipient's own activity or requests: a price or back in stock alert they set, a delivery status, a reply on their work, a job that finished. Broadcast promotion competes worst for the interruption budget and usually does more on a surface the user opened on purpose.

# Constraints

Visibility is poor and worsening. Confirmed delivery fires when the OS hands the payload to the app, not when the user sees it, so it diagnoses Focus and silent kills, not summarisation. The collapsed view is template bound, so the proposition must lead with the fact. See [copywriting](/foundations/copywriting.md).

# Measurement

Treat the dashboard with doubt. Opens and clicks sit downstream of an editor you cannot see, and conversions are a biased sample of the notifications the platform favoured. Confirm render through the SDK where you can, pool campaigns and lengthen windows, and weight downstream conversion. See [measuring intermediation](/measurement/measuring-intermediation.md).

# Lifecycle role

The re engagement and time critical channel for app audiences. Once the user is back in the app, the [in app](/channels/in-app.md) surfaces take over.

# Related

* [In-app](/channels/in-app.md)
* [Platform interventions](/references/platform-interventions.md)
* [Copywriting](/foundations/copywriting.md)
* [Orchestration and frequency](/foundations/orchestration-and-frequency.md)

# Citations

[1] [Apple, on-device and server foundation models (~3B-parameter on-device model)](https://machinelearning.apple.com/research/introducing-apple-foundation-models)
[2] [Android Developers, Gemini Nano on-device model](https://developer.android.com/ai/gemini-nano)
[3] [Apple, APNs payload size limit (4KB; 5KB VoIP)](https://developer.apple.com/library/archive/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/CommunicatingwithAPNs.html)
[4] [Firebase, FCM message types and payload size](https://firebase.google.com/docs/cloud-messaging/customize-messages/set-message-type)
[5] [Apple, UNNotificationInterruptionLevel (passive, active, time-sensitive, critical)](https://developer.apple.com/documentation/usernotifications/unnotificationinterruptionlevel)
[6] [Android Developers, create and manage notification channels](https://developer.android.com/develop/ui/views/notifications/channels)
