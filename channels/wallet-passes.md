---
type: Channel
title: Wallet passes
description: How to use Apple Wallet and Google Wallet passes as a persistent, updatable, location-aware loyalty surface, distribute and update them and measure them against a holdout.
tags: [channel, wallet, apple-wallet, google-wallet, passkit, passes, loyalty, coupons, lock-screen]
generated:
  by: human:jacquescorbytuech
  at: 2026-08-20T00:00:00Z
sources:
  - id: apple-wallet-developer-guide-passkit
    resource: https://developer.apple.com/library/archive/documentation/UserExperience/Conceptual/PassKit_PG/index.html
    title: "Apple, Wallet Developer Guide (PassKit)"
  - id: apple-updating-a-pass-with-push-notifications
    resource: https://developer.apple.com/library/archive/documentation/UserExperience/Conceptual/PassKit_PG/Updating.html
    title: "Apple, updating a pass with push notifications"
  - id: google-google-wallet-api
    resource: https://developers.google.com/wallet
    title: "Google, Google Wallet API"
  - id: google-google-wallet-generic-pass
    resource: https://developers.google.com/wallet/generic
    title: "Google, Google Wallet generic pass"
---

## What it is

A wallet pass is a loyalty card, coupon, ticket or membership stored in Apple Wallet or Google Wallet on the phone. Its distinctive value is presence without a send: a persistent object held on the device that you update remotely and that can surface itself on the lock screen by time or location. Where every other channel costs a message to reach the user, a pass simply sits on the device staying current and asks for attention only when it is relevant.

## Permission and reach

The add-to-wallet action is the opt-in: the user adds the pass deliberately and can allow it to send notifications. Updating a held pass needs no fresh consent and has no per-message cost, the channel's advantage over the send-based channels. The trade is reach: a pass is bound to the wallet on a device; there is no portable list; the audience is only ever the set of users who chose to add it.

## Filtering and editing

No editor touches the content: the pass renders exactly as you define it. Delivery is the weak point. A remote update rides an empty APNs wake-up push that the OS may coalesce, defer or drop before the device ever pulls the new pass; nothing guarantees it arrives. The automatic-updates setting on each pass decides whether new versions reach it at all; the notifications setting decides only whether the change is announced. The lock-screen relevance surfacing is OS-driven by the time and geofence you set on the pass. See [device channels are leased](/principles/device-channels-are-leased.md).

## Technical specifics

The pass is a structured object you define once and then update over the wire.

* **Pass structure.** Apple uses PassKit, a signed `.pkpass` bundle defining fields, a barcode and appearance; Google Wallet uses a class and object created and updated through its REST API. Each pass type (loyalty, coupon, ticket, generic) has its own template.
* **Remote updates via push.** On Apple, the device registers with your web service when the pass is added; a push from you then tells it to pull the updated pass. On Google, you update the pass object through the API and it syncs to the device. A field change, a new points balance, an added offer, a gate change, updates the held pass and can notify the user.
* **Relevance triggers.** A pass can declare lock-screen relevance by location (a geofence around a store or venue) and by time, appearing when the user is nearby or the event approaches, with no campaign send at all.
* **Barcode and identity.** The pass carries a scannable code that ties an in-store scan back to the customer record, closing the loop between the digital pass and the physical redemption.

## Best-fit jobs

Anything with a card, a balance or a redeemable token: loyalty cards whose points balance stays current on the phone; coupons and offers as location-aware redeemable tokens; event and booking tickets; membership credentials. It is a natural extension of a [loyalty programme](/foundations/loyalty-and-retention-programs.md). Its worst job is free-form proactive messaging: the pass is an updatable object and a location trigger, not a conversation. News and persuasion belong on the send-based channels.

## Wallet versus push versus email

The pass is the persistent owned object; [push](/channels/push.md) and [email](/channels/email.md) are the sends that drive adoption of it and re-engage around it. Use the pass to keep a live token on the device (a balance, a coupon, a ticket) and to catch the user by location; use push and email to deliver news and bring the user back. They are complementary rather than competing: email the offer, drop it into the wallet and let the lock-screen relevance finish the job when the user is near the store.

## Constraints

Adoption is the limiter: the user must add the pass, which means a clear reason and a prompt at every touch, with reach only ever as good as your distribution funnel. Two platforms mean two separate implementations to build and maintain. Notifications can be disabled per pass; a pass left un-added is simply absent. Each of these caps the size of the audience rather than what the pass can say.

## Measurement

Scans and redemptions are first-party and clean, since the barcode ties each one to the customer record, but a redemption count is not the channel's incremental effect. The read that isolates it is a holdout: hold back a slice from the pass programme and compare redemption rate and repeat purchase against it, so a pass that would have been redeemed anyway is not credited to the channel. Watch add rate and on-device retention as the programme's health metrics. See [holdouts and control groups](/measurement/holdouts-and-control-groups.md).

## Lifecycle role

The retention and loyalty surface that persists between sends, strongest for programmes that have a card, a balance or a redeemable offer to keep current. It both feeds and is fed by the [loyalty programme](/foundations/loyalty-and-retention-programs.md): the programme gives the pass something to display; the pass keeps the programme present on the device.

## Related

* [Push](/channels/push.md)
* [Email](/channels/email.md)
* [Loyalty and retention programs](/foundations/loyalty-and-retention-programs.md)
* [Offers and incentives](/foundations/offers-and-incentives.md)
* [Holdouts and control groups](/measurement/holdouts-and-control-groups.md)
