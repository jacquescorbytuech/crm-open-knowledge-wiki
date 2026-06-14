---
type: Playbook
title: Loyalty and Retention Programs
description: How to structure a loyalty programme, points earn and redemption ratios, tier ladders and progress nudges, two-sided referrals, and the enrolment, lifecycle comms, and holdout-proven metrics that justify spending on keeping customers rather than only acquiring them.
tags: [loyalty, retention, referral, repeat-purchase, ltv, programs, points, tiers, enrolment, holdout]
timestamp: 2026-06-14T00:00:00Z
---

## Why retention is where the economics sit

A loyalty programme is a CRM instrument, not a perk bolted on the side. The case for it is the case for retention generally: acquiring a new customer costs several times more than keeping an existing one, and small improvements in retention compound into large profit gains, the classic finding that a five-point lift in retention can raise profit by a quarter or more. A programme that pours its budget into acquisition and lets customers lapse is spending at the expensive end of its own economics. See [retention and LTV](/measurement/retention-and-ltv.md).

## What a loyalty program does

A loyalty programme gives a customer a structured reason to come back and a record of the relationship that makes the next purchase easier. Done well it raises repeat-purchase rate and share of wallet; loyal customers spend more and more often. The programme is also a first-party data engine: every enrolled member is an identified, consenting customer whose behaviour feeds the [single customer view](/foundations/customer-data-and-identity.md).

## Common mechanics

* **Points.** Customers earn a balance on spend or actions and redeem it for value. Simple, legible, and effective when the earn-to-reward ratio is generous enough to feel attainable.
* **Tiers.** Status levels unlock better perks as a customer spends more, giving the upper tiers something to protect and the lower tiers something to climb toward. Tiering pairs naturally with [value-based segmentation](/foundations/segmentation-models.md).
* **Referral.** Existing customers are rewarded for bringing in new ones. Referred customers are not just cheaper to acquire; the evidence is that they retain better and are worth more over their lifetime than customers from other channels, so a referral mechanic compounds rather than just topping up the funnel.

## How to structure a points programme

A points programme has two ratios to set, and the customer reads them as one number: how fast do points turn back into value. Decide the earn rate first, then the redemption rate, then check the combined value the customer actually gets back.

The two levers, as an illustrative example, not a benchmark:

| Lever | Example setting | What it controls |
|---|---|---|
| Earn rate | 10 points per 1 unit of spend | How fast the balance grows |
| Redemption | 1,000 points = 5 units of reward value | What a point is worth |

Worked through, that example returns about 5% of spend as reward value: 100 units spent earns 1,000 points, redeemable for 5 units. Set the two ratios together and sanity-check the percentage you are giving back against margin before you publish either number, because the headline earn rate is what customers remember and is painful to cut later.

The governing principle is attainability: the first reward has to feel reachable, not theoretical. A round-number earn rate and a first redemption a typical customer hits within a few purchases beats a richer-on-paper scheme whose first reward sits months away. If the only reachable reward needs an unrealistic spend, members stop tracking their balance and the programme stops changing behaviour. Use a clear point-to-value statement so a member can see what their balance is worth without doing the arithmetic.

## How to design tiers

Tiers reward cumulative spend or activity over a qualifying window with escalating benefits. Set thresholds so each tier is a stretch from the one below but visibly within reach, and make every step up unlock a benefit a member can name.

An example tier ladder, a common structure rather than a recommended set of numbers:

| Tier | Example threshold (annual spend) | Example benefits |
|---|---|---|
| Base | enrol | Points earning, member pricing |
| Silver | 250 units | Faster earn rate, early access |
| Gold | 750 units | Free shipping, priority support |
| Platinum | 2,000 units | Dedicated service, exclusive events |

Two design choices carry most of the weight. First, escalate the benefit, not just the discount, so higher tiers offer status and access the brand can sustain. Second, run the nudge mechanic: show each member their progress to the next tier, in absolute terms ("180 units to Gold") and on a visible bar, in account and in lifecycle email. Progress framing turns an abstract status into a goal a member is part-way through and reluctant to abandon, which is the mechanism that drives incremental spend near a threshold. Decide and publish how status renews (rolling window or annual reset) so a member knows what protects their tier.

## How to run referrals

A referral mechanic works when both sides are rewarded, the attribution is unambiguous, and abuse is capped before launch.

1. **Make it two-sided.** Reward the referrer and the new customer. A one-sided reward gives the advocate nothing to act on or makes the pitch feel mercenary; a two-sided reward gives the advocate a reason to share and the friend a reason to accept.
2. **Track it cleanly.** Issue each member a unique referral code or link and credit the reward on a qualifying first purchase by the referred customer, not on sign-up alone. Tying the reward to a real purchase aligns the payout with value created.
3. **Cap and screen for fraud.** Set a per-member cap on referral rewards in a period, require the referred customer to be genuinely new (not an existing account or the referrer's second address), and gate the payout behind the qualifying purchase clearing any return window. Self-referral and circular referral are the common abuse patterns; the qualifying-purchase gate and the cap defuse both.

Reward referrals with programme value (points, credit, perks) on the same logic as the rest of the programme, so they reinforce membership rather than running as a separate discount stream.

## Enrolment and lifecycle comms

A loyalty programme is delivered through the lifecycle, not separately from it. Enrolment belongs in [onboarding](/foundations/lifecycle-mapping.md), points and tier nudges belong in engagement, and an at-risk member is a retention trigger. Coordinate its messages under the one [contact strategy](/foundations/orchestration-and-frequency.md) so loyalty mail does not become an uncapped extra stream on top of the marketing calendar.

A workable comms backbone:

* **Enrol early.** Invite at or just after the first purchase, when intent is highest and the account already exists. Auto-enrol where the consent and terms allow it, and confirm the benefit in the welcome flow rather than burying it.
* **Points and tier-progress emails.** Send a periodic balance statement and a progress-to-next-tier update. These are the programme's engagement engine: they give a member a reason to return that is about their own status, not a generic offer.
* **Milestone nudges.** Trigger a message when a member is close to a redemption threshold or a tier upgrade ("you are 180 units from Gold"), when points are about to expire, and on the member's anniversary. Proximity and scarcity nudges near a threshold are where most incremental behaviour sits.

## Which programme metrics to track

Track the programme as a behaviour-change effort, not a sign-up count.

| Metric | What it tells you |
|---|---|
| Enrolment rate | Share of eligible customers who join |
| Active-member share | Share of members who earn or redeem in a period (sign-ups who never engage are not retained) |
| Member vs non-member repeat-purchase | Whether members come back more often than comparable non-members |
| Member vs non-member value lift | Whether members spend more per period than comparable non-members |

The member-versus-non-member comparisons are the headline numbers, and they are also the easiest to fool yourself with: members self-select, so the people who join were already your better customers. A raw member-versus-non-member gap overstates the programme's effect because it includes that selection. To prove the lift is caused by the programme rather than by who joins it, measure against a randomised holdout: withhold the programme (or a specific benefit or nudge) from a random slice of eligible customers and read the difference. See [holdouts and control groups](/measurement/holdouts-and-control-groups.md) and the aggregate effect it lets you read in [uplift and incrementality](/measurement/uplift-and-incrementality.md).

## A caution on discount-led loyalty

A programme that only ever rewards with discounts trains customers to wait for the discount and attracts the deal-seekers who churn when it stops. Reward with value the brand can sustain, status, access, useful perks, not only money off. See [offers and incentives](/foundations/offers-and-incentives.md).

## Related

* [Retention and LTV](/measurement/retention-and-ltv.md)
* [Holdouts and control groups](/measurement/holdouts-and-control-groups.md)
* [Uplift and incrementality](/measurement/uplift-and-incrementality.md)
* [Segmentation models](/foundations/segmentation-models.md)
* [Offers and incentives](/foundations/offers-and-incentives.md)
* [Lifecycle mapping](/foundations/lifecycle-mapping.md)
* [Customer data and identity](/foundations/customer-data-and-identity.md)
* [Orchestration and frequency](/foundations/orchestration-and-frequency.md)

## Citations

[1] [HBR, the value of keeping the right customers (retention vs acquisition cost; 5% retention to 25-95% profit)](https://hbr.org/2014/10/the-value-of-keeping-the-right-customers)
[2] [Bain & Company (Reichheld), a 5% increase in retention raises profit by more than 25%](https://media.bain.com/Images/BB_Prescription_cutting_costs.pdf)
[3] [HubSpot, customer loyalty programs and mechanics (points, tiers; loyal customers spend more)](https://blog.hubspot.com/service/customer-loyalty)
[4] [HBR, why customer referrals can drive stunning profits](https://hbr.org/2011/06/why-customer-referrals-can-drive-stunning-profits)
[5] [Schmitt, Skiera & Van den Bulte, Referral Programs and Customer Value (referred customers retain better and are worth ~16% more)](https://faculty.wharton.upenn.edu/wp-content/uploads/2012/04/Schmitt-Skiera-vandenBulte-2011-Referral-Programs-Customer-Value.pdf)
