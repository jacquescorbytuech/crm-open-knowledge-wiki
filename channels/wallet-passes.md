---
type: Channel
title: Wallet passes
description: How to use Apple Wallet and Google Wallet passes as a persistent, updatable, location-aware loyalty surface, distribute and update them, and measure them against a holdout.
tags: [channel, wallet, apple-wallet, google-wallet, passkit, passes, loyalty, coupons, lock-screen]
timestamp: 2026-06-14T00:00:00Z
---

# What it is

A wallet pass is a loyalty card, coupon, ticket, or membership stored in Apple Wallet or Google Wallet on the phone. Its distinctive value is presence without a send: a persistent, owned object on the device that you update remotely and that can surface itself on the lock screen by time or location. Where every other channel costs a message to reach the user, a pass simply sits on the device staying current, and asks for attention only when it is relevant.

# Permission and reach

The user adds the pass deliberately, the add-to-wallet action is the opt-in, and can allow the pass to send notifications. Updating a held pass needs no fresh consent and carries no per-message cost, which is the channel's quiet advantage over the send-based channels. The trade is reach: a pass is bound to the wallet on a device, there is no portable list, and the audience is only ever the set of users who chose to add it.

# Filtering and editing

Minimal. The pass renders as you define it and remote updates land directly on the held copy. The lock-screen relevance surfacing is OS-driven by the time and geofence you set on the pass, not by an editor between you and the user. The only real gate is whether the user kept notifications enabled for that pass.

# Technical specifics

The pass is a structured object you define once and then update over the wire.

* **Pass structure.** Apple uses PassKit, a signed `.pkpass` bundle defining fields, a barcode, and appearance; Google Wallet uses a class and object created and updated through its REST API. Each pass type (loyalty, coupon, ticket, generic) has its own template.
* **Remote updates via push.** On Apple, the device registers with your web service when the pass is added, and you send a push that tells the device to pull the updated pass. On Google, you update the pass object through the API and it syncs to the device. A field change, a new points balance, an added offer, a gate change, updates the held pass and can notify the user.
* **Relevance triggers.** A pass can declare lock-screen relevance by location (a geofence around a store or venue) and by time, so it appears when the user is nearby or the event approaches, with no campaign send at all.
* **Barcode and identity.** The pass carries a scannable code that ties an in-store scan back to the customer record, closing the loop between the digital pass and the physical redemption.

# Best-fit jobs

Anything with a card, a balance, or a redeemable token: loyalty cards whose points balance stays current on the phone, coupons and offers as location-aware redeemable tokens, event and booking tickets, and membership credentials. It is a natural extension of a [loyalty programme](/foundations/loyalty-and-retention-programs.md). Its worst job is free-form proactive messaging, the pass is an updatable object and a location trigger, not a conversation, so news and persuasion belong on the send-based channels.

# Wallet versus push versus email

The pass is the persistent owned object; [push](/channels/push.md) and [email](/channels/email.md) are the sends that drive adoption of it and re-engage around it. Use the pass to keep a live token on the device, a balance, a coupon, a ticket, and to catch the user by location; use push and email to deliver news and bring the user back. They are complementary rather than competing: email the offer, drop it into the wallet, and let the lock-screen relevance finish the job when the user is near the store.

# Constraints

Adoption is the limiter. The user must add the pass, so you need a clear reason and a prompt at every touch, and the channel's reach is only ever as good as your distribution funnel. Two platforms mean two separate implementations to build and maintain. Notifications can be disabled per pass, and a pass left un-added is simply absent. None of this is editorial interference, it is a ceiling on who you can reach.

# Measurement

Scans and redemptions are first-party and clean, the barcode ties each one to the customer record, but a redemption count is not the channel's incremental effect. The honest read is still a holdout: hold back a slice from the pass programme and compare redemption rate and repeat purchase against it, so a pass that would have been redeemed anyway is not credited to the channel. Watch add rate and on-device retention as the programme's health metrics. See [holdouts and control groups](/measurement/holdouts-and-control-groups.md).

# Lifecycle role

The retention and loyalty surface that persists between sends, strongest for programmes that have a card, a balance, or a redeemable offer to keep current. It both feeds and is fed by the [loyalty programme](/foundations/loyalty-and-retention-programs.md): the programme gives the pass something to display, and the pass keeps the programme present on the device.

# Related

* [Push](/channels/push.md)
* [Email](/channels/email.md)
* [Loyalty and retention programs](/foundations/loyalty-and-retention-programs.md)
* [Offers and incentives](/foundations/offers-and-incentives.md)
* [Holdouts and control groups](/measurement/holdouts-and-control-groups.md)

# Citations

[1] [Apple, Wallet Developer Guide (PassKit)](https://developer.apple.com/library/archive/documentation/UserExperience/Conceptual/PassKit_PG/index.html)
[2] [Apple, updating a pass with push notifications](https://developer.apple.com/library/archive/documentation/UserExperience/Conceptual/PassKit_PG/Updating.html)
[3] [Google, Google Wallet API](https://developers.google.com/wallet)
[4] [Google, Google Wallet generic pass](https://developers.google.com/wallet/generic)
