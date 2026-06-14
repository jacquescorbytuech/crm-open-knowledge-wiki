---
type: Playbook
title: Offers and Incentives
description: How to use discounts and incentives without training deal-seeking or eroding margin, with the arithmetic to size an offer against margin, the holdout to measure its true effect, a price vs non-price decision rule, and offer-window targeting.
tags: [offers, incentives, discounts, promotions, margin, pricing, break-even, holdout]
timestamp: 2026-06-14T00:00:00Z
---

## The discipline, in one line

An incentive is a lever that works once you stop pulling it reflexively. Used with discipline it converts a hesitant buyer; used by default it teaches your whole audience to wait, attracts the customers who leave when it stops, and gives away margin you did not need to spend. Most of the offer mistakes in a programme are mistakes of reflex, not of generosity.

The test is one piece of arithmetic, not a feeling about generosity: an offer only pays when its measured incremental share, verified against a holdout, beats the break-even the discount sets, and most broad sends fail that math because the would-have-bought majority swamps the incremental few you actually convert. So target the offer narrow, always hold out a control, and prefer a non-price lever wherever you can name no price barrier. The sizing later down the page is where that test gets worked out; treat everything above it as the reflexes that test is meant to discipline.

## What over-discounting costs

Heavy, habitual discounting has three predictable effects. It trains customers to hold out for the next sale rather than pay full price. It attracts deal-seekers whose lifetime value is low and whose retention is worse, the opposite of the customer the programme wants. And it erodes margin directly: a broad price cut reduces the margin on everyone who would have bought anyway, not just the incremental buyers it wins. A brand that becomes a discount brand struggles to stop being one.

## When an incentive earns its place

Reserve incentives for the moments where they change a decision rather than subsidise one already made.

* **First purchase**, where a one-time, first-buyer-only offer lowers the barrier to a relationship, not a habit.
* **Genuine reactivation**, where a lapsed customer needs a reason to return and the alternative is losing them. See [automation and sequences](/foundations/automation-and-sequences.md).
* **Clearing real constraints**, end-of-season, overstock, where the discount has a reason the customer can see.

Avoid the reflexes: do not lead the [welcome sequence](/principles/the-welcome-window.md) with a discount, and do not fire one in the first [abandoned-cart](/foundations/automation-and-sequences.md) message, which simply teaches customers to abandon on purpose.

## Depth, targeting, and margin

When you do discount, the depth and the audience decide whether it pays. A shallow offer to a wide audience and a deep offer to a narrow, high-intent one can cost the same in margin and perform very differently. Target the incentive to the segment whose decision it actually changes, using the [segmentation models](/foundations/segmentation-models.md), and measure it against a [holdout](/measurement/holdouts-and-control-groups.md) so you know whether the revenue was incremental or just margin you handed to buyers who were going to convert anyway.

There is no correct discount depth, only a depth set against your margin. As a heuristic, not a benchmark: the shallowest depth that moves the decision is the right one, and a depth that exceeds your gross margin point means every redemption loses cash on the unit. Treat any depth range you see quoted elsewhere as someone else's margin, not yours.

## Does the offer pay: sizing against margin

This is the test the opener named, worked out as arithmetic. Before sending, work out whether the offer can pay for itself. A discount costs you margin on every redeemer, including the ones who would have bought anyway. It only pays if the margin won from buyers it actually converts exceeds that cost. The break-even is the share of redeemers who must be genuinely incremental.

```
offer cost per redeemer       = unit_price x discount_rate
post-offer contribution       = unit_price x gross_margin_rate - offer_cost_per_redeemer
break-even incremental share  = offer_cost_per_redeemer / post_offer_contribution
offer pays  when  measured incremental share (from holdout) > break-even incremental share
```

Worked example. A 60 pound product at 50% gross margin, offered at 20% off. Offer cost per redeemer is 60 x 0.20 = 12 pounds. Post-offer contribution is 60 x 0.50 - 12 = 18 pounds. Break-even incremental share is 12 / 18 = 0.67. So more than two thirds of everyone who redeems must be a buyer who would not have bought without the offer, otherwise the margin you handed to the would-have-bought majority outweighs the contribution from the incremental few. For a blanket send to an already-engaged list that share is rarely met, which is why the same offer that loses money sent wide can pay sent to a narrow, low-intent segment.

## Measuring the true effect with a holdout

The break-even above turns on the measured incremental share, and the only honest source of that number is a holdout: a randomised slice of the eligible audience that gets no offer. Compare redemption-driven revenue in the treated group against the control group that got nothing. Much discounted revenue would have converted anyway, so the gap between the two groups, not the gross redeemed total, is what the offer actually drove. Read [holdouts and control groups](/measurement/holdouts-and-control-groups.md) for the mechanism and [uplift and incrementality](/measurement/uplift-and-incrementality.md) for the arithmetic and for why a last-touch report on redemptions overstates the effect. Feed the resulting incremental share back into the break-even to decide whether to repeat, deepen, or kill the offer.

## Price incentive or non-price incentive

A price incentive is the right tool only when the barrier is genuinely price. Use this rule.

* If the customer wants the product but the price is the blocker, a measured discount is the direct lever, and the break-even above tells you whether it pays.
* If the barrier is anything else, reach for a non-price lever first, because it moves the decision without spending margin or training the discount habit. Hesitation about timing or stock favours early or exclusive access. Friction at checkout favours free shipping or returns. Uncertainty about fit favours an add-on, content, or a try-before-you-buy. Wanting to feel like an insider favours status in a loyalty programme. A weak basket favours a bundle that raises perceived value without cutting headline price.

> [!tip] Default to non-price unless you can name the price barrier
> A price incentive is the right tool only when the barrier is genuinely price. If you cannot name the price barrier, reach for a non-price lever first, then test the chosen lever against a holdout.

## Offer windows and targeting

Scope an offer to a moment and a segment, not to the whole list. A blanket send maximises the would-have-bought majority that the break-even punishes you for, and it broadcasts the discount habit to everyone. Bind each offer to a trigger and a window instead.

* **First-buyer window.** Fire the first-purchase offer once, time-boxed from the first qualifying event, and suppress it for anyone who has already bought, so it lowers a barrier to a relationship rather than rewarding existing buyers.
* **Reactivation trigger window.** Fire the winback offer on a lapse trigger, a defined gap since last order, inside a short window, then stop, so it reaches genuinely lapsed customers rather than the merely quiet. See [automation and sequences](/foundations/automation-and-sequences.md).
* **Constraint window.** Tie end-of-season or overstock offers to the real constraint and close them when it clears, so the discount keeps a reason the customer can see.

Narrow scope also tightens the holdout: a control drawn from inside the same triggered, eligible segment gives a cleaner incremental read than one drawn from the whole base.

## Alternatives to money off

The non-price preference the opening named is worth stating plainly. Money is the most expensive and least differentiated incentive. Often a non-price lever moves the same decision without training the discount habit: early or exclusive access, free shipping or returns, a useful add-on, content, or status in a [loyalty programme](/foundations/loyalty-and-retention-programs.md). These build the relationship rather than discounting it.

## Related

* [Loyalty and retention programs](/foundations/loyalty-and-retention-programs.md)
* [Automation and sequences](/foundations/automation-and-sequences.md)
* [The welcome window](/principles/the-welcome-window.md)
* [Holdouts and control groups](/measurement/holdouts-and-control-groups.md)
* [Segmentation models](/foundations/segmentation-models.md)

## Citations

[1] [The Good, why discounting is bad for your brand (trains deal-seeking; attracts bargain hunters)](https://thegood.com/insights/discounting-for-ecommerce/)
[2] [Competera, discount pricing strategy (depth vs margin; selective discounting)](https://competera.ai/resources/articles/discount-pricing-strategy-definition-example)
[3] [HBR, the value of keeping the right customers (low-value vs high-value customers)](https://hbr.org/2014/10/the-value-of-keeping-the-right-customers)
