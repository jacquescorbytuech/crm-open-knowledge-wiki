---
type: Framework
title: Segmentation Models
description: The models a programme uses to divide an audience, RFM, value and lifetime-value tiers, behavioural, demographic and firmographic, lifecycle-stage, and propensity, with how to compute RFM and a simple CLV, how to combine them with lifecycle stage, and how to choose between them for a given job.
tags: [segmentation, rfm, clv, propensity, behavioural, lifecycle, framework, scoring]
timestamp: 2026-06-14T00:00:00Z
---

# What this is

Where [segmentation and data](/foundations/segmentation-and-data.md) covers the operational how, dynamic versus static segments, hygiene, and the cost of slicing too thin, this covers the what: the models that decide how an audience is divided in the first place. The model you pick should follow the job. A reactivation campaign wants a recency model; a VIP programme wants a value model; a cross-sell wants a propensity model.

# RFM

RFM scores each customer on three axes: Recency (how recently they bought), Frequency (how often), and Monetary value (how much). It originated in mid-twentieth-century direct and catalogue marketing and remains the most durable behavioural model because it needs only transaction data and predicts future behaviour well. Customers who score high on all three are your core; high-monetary but low-recency are your at-risk best customers, the most valuable reactivation target you have.

# How to compute RFM

Fix a lookback window first, the period of transaction history you score against. A year is a common default for most retail; shorter for high-frequency categories, longer for considered purchases bought once or twice a year. Everything below is computed inside that window.

For each customer, derive three raw numbers: recency as days since last order (smaller is better), frequency as order count, monetary as total or average spend. Then score each axis independently by ranking the customer base into bands, quintiles (five bands, 1 to 5) for a large list, quartiles for a smaller one. The point of ranking rather than fixing absolute thresholds is that the bands self-calibrate to your own base and stay comparable when you recompute them.

```
R score = quintile of (days since last order), reversed so most recent = 5
F score = quintile of (order count in window), most frequent = 5
M score = quintile of (spend in window), highest spend = 5
```

That gives every customer a three-digit code from 111 to 555. You do not act on 125 distinct cells. Collapse the code into a handful of named groups and attach one action to each. The score-to-action map below is illustrative, not a benchmark; set the boundaries against your own base and revise them as you learn which groups respond.

```
RFM pattern          Example codes   Reading                     Action
high R, high F, high M  5-4-5, 5-5-5  recent, frequent, valuable  nurture, VIP track, early access
high R, low F           5-1-x         recent first-time buyer     onboard, drive second order
high F, mid R           4-5-x         loyal, slightly cooling     keep warm, reward
low R, high M           1-x-5         valuable but lapsing        win-back, strong reactivation offer
low R, low F, low M     1-1-1         dormant, low value          minimal spend or suppress
```

The recurring two patterns to separate by hand are high-RFM (nurture, do not discount what they would pay for) and high-value lapsing (win-back, where a real offer is justified because the customer is worth recovering).

# Value and lifetime-value tiers

Value segmentation tiers the audience by what each customer is worth, usually by customer lifetime value (CLV): the total past and predicted spend of a customer over the relationship. Tiering by CLV lets the programme spend where the return is, more attention and better offers to the top tier, efficient automation to the long tail. It is the model that connects segmentation to the economics in [retention and LTV](/measurement/retention-and-ltv.md).

# A simple CLV for tiering

You do not need a probabilistic model to start tiering. Two pragmatic approaches:

Historic value is just observed spend to date, the sum of past orders per customer, optionally net of returns. It is backward-looking and says nothing about the future, but it ranks the base cleanly and is enough to cut value tiers on day one.

A forward estimate uses contribution margin times expected lifetime:

```
CLV (simple) = average order value x gross margin % x purchase frequency per year x expected years retained
```

Use margin, not revenue, so the tiers reflect what a customer is actually worth to the business. Expected years retained can be seeded from your observed retention rate before you have anything better. Treat this as a tiering input, not a precise forecast. For the proper retention-curve and probabilistic methods, and the pitfalls of each, see [retention and LTV](/measurement/retention-and-ltv.md).

# Behavioural, demographic, and firmographic

* **Behavioural** segmentation divides on what customers do: purchases, product usage, browse patterns, engagement. It is usually the most actionable for lifecycle marketing because behaviour predicts behaviour.
* **Demographic** segmentation divides on who customers are: age, location, income, gender. Easy to capture, but a weaker predictor of action than behaviour.
* **Firmographic** segmentation is the B2B equivalent of demographic, dividing organisations by industry, size, and revenue.

# Lifecycle-stage

Lifecycle-stage segmentation divides the audience by where each customer sits in the journey, the acquisition, onboarding, engagement, retention, and winback stages from [lifecycle mapping](/foundations/lifecycle-mapping.md). It is less a competing model than the organising frame the others operate inside: you might run an RFM model within the engaged stage and a recency model within the lapsing one.

# Combining RFM with lifecycle stage

The clean way to combine the two is to nest, not cross. Use lifecycle stage as the outer frame and apply RFM only inside the stage where it earns its keep. Two RFM axes already encode lifecycle signal (recency separates engaged from lapsing), so crossing the full 555 code against every stage just re-splits the same customers and multiplies cells you cannot send to.

A workable pattern: let stage decide the message (onboarding sequence, retention nurture, winback), and let RFM decide priority and offer depth within that stage. In the engaged stage, RFM tier sets who gets VIP treatment; in the lapsing stage, monetary score sets how hard you bid to win them back. That keeps the segment count to stage times a few RFM tiers, not stage times 125. The same overlap discipline and dynamic-versus-static handling lives in [segmentation and data](/foundations/segmentation-and-data.md).

# Propensity

Propensity models predict the probability a customer takes a specific action, buying a category, upgrading, or churning, and segment on the score. A churn-propensity model surfaces who to intervene with before they lapse; a purchase-propensity model surfaces who to push. These are the entry point to predictive segmentation, and like all of it, they are gated by the data underneath. See [customer data and identity](/foundations/customer-data-and-identity.md) and [decisioning and personalisation](/foundations/decisioning-and-personalisation.md).

A propensity score answers who is likely to act, which is not the same as who your sending changes. The first keeps messaging people who would have acted anyway; the second is the uplift question, and it needs a randomised holdout to answer honestly. Treat propensity as the accessible first step and reach for the rigorous version when you have the volume. See [uplift and incrementality](/measurement/uplift-and-incrementality.md).

# Refresh cadence

Segments go stale at different rates, so recompute them on different clocks. RFM is behavioural and moves quickly: a recent buyer becomes a lapsing one with no new event at all, just the passage of time, so recompute it on a short, regular cadence (for many programmes weekly or monthly is a sensible default) and let customers move between tiers as they do. CLV tiers move slowly and noisily, so recompute them less often, quarterly is a reasonable default, to avoid churning customers between value tiers on a single large order. Whatever cadence you pick, make it scheduled and consistent so a customer's tier means the same thing each time you read it.

# Choosing a model

Match the model to the job, and prefer the simplest model that answers the question. Combining models multiplies segments fast, and below a list in the low thousands the slices stop being testable or sendable. See [segmentation has real costs](/principles/segmentation-has-costs.md) and [volume thresholds](/measurement/volume-thresholds.md).

# Related

* [Segmentation and data](/foundations/segmentation-and-data.md)
* [Customer data and identity](/foundations/customer-data-and-identity.md)
* [Lifecycle mapping](/foundations/lifecycle-mapping.md)
* [Retention and LTV](/measurement/retention-and-ltv.md)
* [Uplift and incrementality](/measurement/uplift-and-incrementality.md)
* [Segmentation has real costs](/principles/segmentation-has-costs.md)

# Citations

[1] [Qualtrics, market segmentation types (behavioural, demographic, firmographic)](https://www.qualtrics.com/articles/strategy-research/what-is-market-segmentation/)
[2] [Omniconvert, the RFM model and its origin in 1960s direct marketing](https://www.omniconvert.com/blog/rfm-model/)
[3] [TechTarget, RFM analysis definition](https://www.techtarget.com/searchdatamanagement/definition/RFM-analysis)
[4] [Klaviyo, segmenting by customer lifetime value](https://help.klaviyo.com/hc/en-us/articles/360013201072)
[5] [CleverTap, propensity modelling for marketers](https://clevertap.com/blog/what-is-propensity-modeling/)
[6] [Amperity, churn propensity model reference](https://docs.amperity.com/reference/model_churn_propensity.html)
