---
type: Principle
title: Device channels are leased, not owned
description: Push, browser push, and wallet passes run on capabilities iOS and Android grant and can revoke, so the platform sets the ceiling on what you can do and moves it without notice.
tags: [principle, push, browser-push, wallet, platform, ios, android, capabilities, permission]
timestamp: 2026-06-15T00:00:00Z
---

## Stance

The on-device channels are not yours. Push, browser push, and wallet passes all run on a small set of capabilities the operating system grants and can withdraw, so what you can do on them is whatever iOS and Android currently allow, no more. You hold no list, you own no surface, and the permission lives inside one install on one device behind a token the platform can invalidate. Treat these channels as leased: useful, but operated inside a boundary you do not set and that shifts under you.

## Where the boundary sits

You control the proposition, the payload you compose, the trigger logic you choose, and the tie back to the customer record. The platform controls everything that decides whether the message reaches a human and how it looks when it does: whether the permission is granted, which surface it lands on, how much interruption it is allowed, whether an on-device model rewrites it, and whether a Focus mode or a per-channel mute silences it without a signal back. Effort spent fighting the platform's half is wasted; the levers that work are the ones you control.

[In-app](/channels/in-app.md) is the exception. It has no platform editor and no permission gate, because it runs inside a product the user already opened, which is what makes it the cleanest surface to measure. Every other on-device channel is subject to the platform's editing.

## The capabilities the platform grants

What you can actually do resolves into a handful of capability classes, each one a discrete grant the OS defines, polices, and revises. The specifics belong on the channel pages; none of them are yours to set.

* **Interruption and priority.** How loudly a message may arrive is the platform's call, not yours. iOS fixes four interruption levels (`passive`, `active`, `time-sensitive`, `critical`), and only time-sensitive can break through Focus, only with the user's leave and never for marketing; critical needs an Apple entitlement you will not get. Android routes every notification through a channel whose importance the user, not you, controls once it exists. You request a level; the user and the OS decide whether you get it.
* **Rich content.** Media beyond text, an image, a custom layout, an action button, is allowed only through the platform's own mechanism: a notification service extension and attachment on iOS, the expanded notification styles on Android. The 4KB payload ceiling caps how much you can include, so the proposition has to lead and the platform may or may not render the rest.
* **Relevance and triggering.** Surfacing a message by time or place is a platform feature you configure, not code you run. A wallet pass declares a geofence and a time and the OS raises it on the lock screen with no send; you set the trigger, but the OS decides whether and when it fires.
* **Background update.** Changing state on the device without interrupting the user, a silent push that refreshes app state, a pass field that updates a points balance over the wire, is permitted but throttled and revocable, and the OS may defer or drop it with no delivery guarantee.
* **Identity and addressability.** The token is the address, and it is the platform's to issue and to invalidate. It is scoped to one install on one device, the user can reset it, and the OS can expire it, so the reachable audience is only ever the set of currently valid grants, rebuilt continuously rather than held.

## The ceiling moves

The capability set is revised on the platform's schedule. Android turned notification permission into an explicit runtime grant and opt-in rates fell; iOS added interruption levels and Focus; on-device models now summarise and reorder the lock screen with no API to tell you which happened. Each change narrows or reshapes what the channel can do, and you learn about it when it ships. Build so a withdrawn capability degrades rather than breaks, and treat each change as a dated natural experiment to measure a before-and-after against; the timeline is in [platform interventions](/references/platform-interventions.md).

The desktop works the same way. Reach there runs through [browser push](/channels/browser-push.md), so the grant is held with the browser and the OS together: the browser controls the prompt and the per-site block, while macOS Notification Centre and Windows notification settings and their Focus modes silence delivery the same way the phone does. The editing is lighter than the mobile lock screen today, but the arrangement is the same.

## Consequences

* The reachable audience shrinks on its own. Tokens expire and grants are revoked, so a device list is only as large as its currently valid permissions, and the count you hold overstates the count you can reach.
* The scarce permission is spent once. The OS prompt is effectively one-shot, so prime it behind your own soft ask tied to a value moment rather than firing it cold; the pattern is the same for mobile push, browser push, location, and tracking consent. See [consent and preferences](/foundations/consent-and-preferences.md).
* Design to the capability you are granted, not the one you wish you had. Lead with the proposition inside the payload ceiling, pick the honest interruption level, and let rich content be enhancement the platform may strip.
* Measure past the platform's editing. Opens and clicks sit downstream of suppression and rewriting you cannot see, so the only honest read is the downstream action against a randomised holdout, where both arms sit behind the same boundary. See [holdouts and control groups](/measurement/holdouts-and-control-groups.md).

## Related

* [Push](/channels/push.md)
* [Browser push](/channels/browser-push.md)
* [Wallet passes](/channels/wallet-passes.md)
* [In-app](/channels/in-app.md)
* [Platform interventions](/references/platform-interventions.md)
* [Consent and preferences](/foundations/consent-and-preferences.md)
* [Holdouts and control groups](/measurement/holdouts-and-control-groups.md)

## Citations

[1] [Apple, UNNotificationInterruptionLevel (passive, active, time-sensitive, critical)](https://developer.apple.com/documentation/usernotifications/unnotificationinterruptionlevel)
[2] [Android Developers, create and manage notification channels](https://developer.android.com/develop/ui/views/notifications/channels)
[3] [Android Developers, notification runtime permission](https://developer.android.com/develop/ui/views/notifications/notification-permission)
[4] [Apple, UNNotificationAttachment (rich notification media)](https://developer.apple.com/documentation/usernotifications/unnotificationattachment)
[5] [Android Developers, create an expanded notification](https://developer.android.com/develop/ui/views/notifications/expanded)
[6] [Apple, APNs payload size limit (4KB; 5KB VoIP)](https://developer.apple.com/library/archive/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/CommunicatingwithAPNs.html)
[7] [Apple, asking permission to use notifications (request in response to value, not at launch)](https://developer.apple.com/documentation/usernotifications/asking-permission-to-use-notifications)
