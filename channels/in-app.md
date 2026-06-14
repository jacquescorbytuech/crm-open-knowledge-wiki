---
type: Channel
title: In-app
description: An owned in product surface with no editor in the pipe and full sender visibility, reaching only the user who is already active in the app.
tags: [channel, in-app, owned, in-product, onboarding]
timestamp: 2026-06-14T00:00:00Z
---

# What it is

In app messaging is everything you can show inside your own product: passive cards in a feed the user reaches deliberately, a persistent message centre or inbox, modal and slide up messages triggered on session events, and messaging primitives embedded in the product flows themselves. It is the highest fidelity owned surface most brands have.

# Permission and reach

No per channel opt in, because the user is already inside a product they chose to open. The hard limit is the opposite of push: in app reaches only the active user. Someone who has not opened the app in a fortnight cannot be reached this way at all, which is precisely the gap push and email cover.

# Filtering and editing

None. Nothing passes through APNs, FCM, or a mailbox provider, so nothing summarises, ranks, bundles, or silences it, and you see every render, dismiss, and interaction. It is the most fully owned and observable surface in the channel mix. See [the channel mix](/channels/index.md).

# Formats and how it fires

In-app spans a range of intrusiveness, from interruptive to ambient.

* **Modal / full-screen.** A centred dialog or takeover for a high-priority moment; the most interruptive, use sparingly.
* **Slide-up / banner.** A lighter prompt that does not block the screen.
* **Embedded cards / content feed.** Passive content in a surface the user reaches deliberately; the least interruptive.
* **Message centre / inbox.** A persistent in-product inbox the user opens on demand, which (unlike the others) can also hold a message for a user to find later.

How it fires is the key mechanism: in-app messages are typically cached on the device at session start and displayed when the user meets a trigger condition (viewing a screen, completing an action, reaching a session count). Because the message is evaluated on-device during a live session, it cannot reach a user who is not currently in the app.

# Best-fit jobs

Everything that does not need to reach a dormant user: onboarding and activation, feature education and discovery, cross sell and upsell, contextual prompts at the moment of relevant action, and surveys. Because it interrupts a session the user chose, relevance and timing matter more than reach.

# Constraints

It cannot initiate contact; it can only act on a session the user started. Over using modals and interstitials degrades the product experience, which is a steeper cost here than an ignored email, because it sits on the surface the relationship is actually built on. See [respect the subscriber](/principles/respect-the-subscriber.md).

# Measurement

The cleanest measurement of any channel. The SDK records impression, dismiss, and interaction with no platform mediated gap, so render to conversion is fully attributable end to end. This is where holdout based incrementality testing is easiest to run honestly. See [holdouts and control groups](/measurement/holdouts-and-control-groups.md).

# Lifecycle role

The destination the other channels drive toward. Push and email bring the user back; in app does the work once they arrive. Run them as one portfolio, not as rivals.

# Related

* [Push](/channels/push.md)
* [The channel mix](/channels/index.md)
* [Orchestration and frequency](/foundations/orchestration-and-frequency.md)
* [Holdouts and control groups](/measurement/holdouts-and-control-groups.md)

# Citations

[1] [Braze, in-app messages reach only active users](https://www.braze.com/docs/user_guide/channels/in_app_messages/faq)
[2] [Airship, in-app automation cached and displayed on trigger conditions](https://www.airship.com/docs/guides/features/messaging/in-app-automation/)
