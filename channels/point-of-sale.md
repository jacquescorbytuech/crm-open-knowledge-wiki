---
type: Channel
title: Point of sale
description: How to use the checkout as a CRM surface: resolve identity at the lane, deliver an offer or an enrolment at the moment of purchase, hand off to the digital channels between visits, and measure it against a holdout.
tags: [channel, point-of-sale, pos, in-store, loyalty, identity-resolution, receipt, clienteling, control-group]
timestamp: 2026-06-15T00:00:00Z
---

## What it is

Point of sale is the checkout used as a delivery surface: an offer presented on the terminal or the customer-facing display, a coupon or message printed on the receipt, a loyalty enrolment captured at the lane, a next-best-action surfaced to the associate as they ring the sale. The message lands in person, at the moment of purchase, with intent already proven by the transaction in front of you.

POS as a *source* is the transaction event flowing into the customer record, the purchase, the basket, the store and time, which belongs to [customer data and identity](/foundations/customer-data-and-identity.md). POS as a *channel* is the platform pushing something back out at the till. It assumes the source side is already wired up, because you cannot personalise anything at the lane until the transaction is resolved to a known customer.

## Permission and reach

Reach is whoever is physically at the till, or whoever the associate is serving. There is no standing list and no way to reach an absent customer, so like [in-app](/channels/in-app.md) the channel acts on a visit the customer started rather than initiating contact. The gate is identity: a cash transaction with no loyalty lookup is anonymous and unaddressable, and everything personalised depends on the customer presenting a loyalty ID, a phone number, a card, or an app barcode at the lane.

The transaction itself sits under a lighter regime than the electronic channels, but the moment you capture an email or mobile number to send a digital receipt or to start a relationship, that capture and any later send fall under the same [consent and preferences](/foundations/consent-and-preferences.md) rules as every other channel. The opt-in taken at the till is a real opt-in and has to be recorded as one.

## Filtering and editing

What stands between you and the customer here is a person, not a model. Where a mailbox provider or `APNs` ranks and filters algorithmically, the cashier or associate decides whether to mention the offer, hand over the coupon, or pitch the loyalty signup at all, which makes the mediation discretionary, inconsistent, and dependent on training and incentives rather than on a model you can reason about. The rest of the surface is tightly constrained: receipt and terminal real estate is small and shared with operational content the transaction needs, so a message competes with the total, the change due, and the return policy for a few lines of attention.

## Technical specifics

The channel lives or dies on the integration to the POS system and on resolving identity fast enough to act before the customer leaves the lane.

* **Identity resolution at the lane.** Everything downstream depends on tying the transaction to a known record in the seconds the sale takes. The common keys are a loyalty number, a phone number typed at the keypad, a payment card token, or a barcode scanned from the customer's app or [wallet pass](/channels/wallet-passes.md). Without one of these the visit is anonymous and only generic content can fire.
* **Where the message can land.** The printed or digital receipt (a coupon, a survey link, a next-purchase incentive); the customer-facing terminal display; a register-issued coupon decisioned at checkout from the basket and the customer history; and the associate's clienteling or POS app, which surfaces the customer's profile and a recommended action to a human rather than to the customer directly.
* **Real-time decisioning versus pre-print.** An offer can be decisioned live at checkout, the platform returns a next-best-action from the basket and the record while the sale rings, or pre-generated and merged onto the receipt template. Live decisioning needs a low-latency call out to the CRM or CDP and a POS that can render the response; pre-print is simpler and slower to react.
* **The integration is the hard part.** POS estates are frequently legacy, on-premise, and fragmented across franchises, and the vendor API is often the slowest and most constrained integration in the stack. What you can deliver at the lane is bounded by what the terminal software exposes, not by what the CRM can decide.

## Best-fit jobs

Capturing identity at the moment of first purchase, turning an anonymous transaction into an addressable customer and starting the digital relationship; loyalty enrolment while the customer is already engaged and the value is concrete; redeeming an offer issued on another channel and closing the loop on it; printing a next-visit incentive on the receipt; and arming the associate with history and a recommendation for higher-value, considered purchases. Its worst job is anything aimed at a customer who is not in the store, which is the entire job of the send-based channels.

## Point of sale versus the digital channels

POS is the bridge between the offline transaction and the addressable record, and the one surface that catches the customer in person with intent already demonstrated. Use it for what only it can do: convert an anonymous shopper into a known, consented customer, and act at the instant of purchase. Hand everything between visits to the channels built for it, the receipt offer drops into the [wallet](/channels/wallet-passes.md), the follow-up arrives by [email](/channels/email.md) or [SMS](/channels/sms-and-rcs.md), and [orchestration and frequency](/foundations/orchestration-and-frequency.md) decides which of them carries the next message. The pass is the natural companion: the barcode the lane scans is the same token the digital programme updates.

## Constraints

The channel is bounded by the POS integration, by the human editor, and by physical presence. The vendor API limits what can render and how fast; the associate is an unreliable conduit who may never surface the message; the receipt and terminal carry only a few lines and share them with operational content; and identity resolution fails on any transaction where the customer presents no loyalty key, leaving a large anonymous tail you cannot personalise to. None of this reaches an absent customer at all.

## Measurement

Redemptions and scans are first-party and clean, the loyalty key ties each one to the record, but a redemption count is not the channel's incremental effect, exactly as it is not for [direct mail](/channels/direct-mail.md) or the [wallet](/channels/wallet-passes.md). The incremental read is a holdout: hold back a slice of the eligible customers from the lane treatment and compare redemption and repeat purchase against it, so an offer that would have been taken anyway is not credited to the channel. Match the issued offer back to the redeemed one by the unique code, and watch enrolment rate and identity-capture rate as the programme's health metrics. See [holdouts and control groups](/measurement/holdouts-and-control-groups.md) and [uplift and incrementality](/measurement/uplift-and-incrementality.md).

## Lifecycle role

The acquisition-into-the-programme and redemption surface, where the offline customer becomes an addressable one and where an online offer gets closed in person. It feeds the customer record and is fed by the [loyalty programme](/foundations/loyalty-and-retention-programs.md), and it pairs with the wallet pass to keep one identity live across the lane and the device. It is a capture-and-close surface, not a place to hold a relationship between visits.

## Related

* [The channel mix](/channels/index.md)
* [Wallet passes](/channels/wallet-passes.md)
* [Customer data and identity](/foundations/customer-data-and-identity.md)
* [Loyalty and retention programs](/foundations/loyalty-and-retention-programs.md)
* [Offers and incentives](/foundations/offers-and-incentives.md)
* [Holdouts and control groups](/measurement/holdouts-and-control-groups.md)

## Citations

[1] [Square, Loyalty API overview (identity and rewards at the point of sale)](https://developer.squareup.com/docs/loyalty-api/overview)
[2] [Square, Terminal API (rendering at the customer-facing terminal)](https://developer.squareup.com/docs/terminal-api/overview)
