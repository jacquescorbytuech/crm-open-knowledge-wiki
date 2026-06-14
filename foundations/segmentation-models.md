---
type: Framework
title: Segmentation Models
description: The models a programme uses to divide an audience, RFM, value and lifetime-value tiers, behavioural, demographic and firmographic, lifecycle-stage, and propensity, and how to choose between them for a given job.
tags: [segmentation, rfm, clv, propensity, behavioural, lifecycle, framework]
timestamp: 2026-06-14T00:00:00Z
---

# What this is

Where [segmentation and data](/foundations/segmentation-and-data.md) covers the operational how, dynamic versus static segments, hygiene, and the cost of slicing too thin, this covers the what: the models that decide how an audience is divided in the first place. The model you pick should follow the job. A reactivation campaign wants a recency model; a VIP programme wants a value model; a cross-sell wants a propensity model.

# RFM

RFM scores each customer on three axes: Recency (how recently they bought), Frequency (how often), and Monetary value (how much). It originated in mid-twentieth-century direct and catalogue marketing and remains the most durable behavioural model because it needs only transaction data and predicts future behaviour well. Customers who score high on all three are your core; high-monetary but low-recency are your at-risk best customers, the most valuable reactivation target you have.

# Value and lifetime-value tiers

Value segmentation tiers the audience by what each customer is worth, usually by customer lifetime value (CLV): the total past and predicted spend of a customer over the relationship. Tiering by CLV lets the programme spend where the return is, more attention and better offers to the top tier, efficient automation to the long tail. It is the model that connects segmentation to the economics in [retention and LTV](/measurement/retention-and-ltv.md).

# Behavioural, demographic, and firmographic

* **Behavioural** segmentation divides on what customers do: purchases, product usage, browse patterns, engagement. It is usually the most actionable for lifecycle marketing because behaviour predicts behaviour.
* **Demographic** segmentation divides on who customers are: age, location, income, gender. Easy to capture, but a weaker predictor of action than behaviour.
* **Firmographic** segmentation is the B2B equivalent of demographic, dividing organisations by industry, size, and revenue.

# Lifecycle-stage

Lifecycle-stage segmentation divides the audience by where each customer sits in the journey, the acquisition, onboarding, engagement, retention, and winback stages from [lifecycle mapping](/foundations/lifecycle-mapping.md). It is less a competing model than the organising frame the others operate inside: you might run an RFM model within the engaged stage and a recency model within the lapsing one.

# Propensity

Propensity models predict the probability a customer takes a specific action, buying a category, upgrading, or churning, and segment on the score. A churn-propensity model surfaces who to intervene with before they lapse; a purchase-propensity model surfaces who to push. These are the entry point to predictive segmentation, and like all of it, they are gated by the data underneath. See [customer data and identity](/foundations/customer-data-and-identity.md) and [decisioning and personalisation](/foundations/decisioning-and-personalisation.md).

# Choosing a model

Match the model to the job, and prefer the simplest model that answers the question. Combining models multiplies segments fast, and below a list in the low thousands the slices stop being testable or sendable. See [segmentation has real costs](/principles/segmentation-has-costs.md) and [volume thresholds](/measurement/volume-thresholds.md).

# Related

* [Segmentation and data](/foundations/segmentation-and-data.md)
* [Customer data and identity](/foundations/customer-data-and-identity.md)
* [Lifecycle mapping](/foundations/lifecycle-mapping.md)
* [Retention and LTV](/measurement/retention-and-ltv.md)
* [Segmentation has real costs](/principles/segmentation-has-costs.md)

# Citations

[1] [Qualtrics, market segmentation types (behavioural, demographic, firmographic)](https://www.qualtrics.com/articles/strategy-research/what-is-market-segmentation/)
[2] [Omniconvert, the RFM model and its origin in 1960s direct marketing](https://www.omniconvert.com/blog/rfm-model/)
[3] [TechTarget, RFM analysis definition](https://www.techtarget.com/searchdatamanagement/definition/RFM-analysis)
[4] [Klaviyo, segmenting by customer lifetime value](https://help.klaviyo.com/hc/en-us/articles/360013201072)
[5] [CleverTap, propensity modelling for marketers](https://clevertap.com/blog/what-is-propensity-modeling/)
[6] [Amperity, churn propensity model reference](https://docs.amperity.com/reference/model_churn_propensity.html)
