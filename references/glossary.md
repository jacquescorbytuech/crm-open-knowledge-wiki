---
type: Glossary
title: Glossary
description: The working vocabulary of email, lifecycle, and CRM marketing used across this bundle, from customer data and segmentation through channels, design, and measurement.
tags: [glossary, terminology, reference]
timestamp: 2026-06-14T00:00:00Z
---

# Authentication and delivery

| Term | Meaning |
| --- | --- |
| SPF | Sender Policy Framework. DNS record authorising which servers may send for your domain. |
| DKIM | DomainKeys Identified Mail. A cryptographic signature verifying the message was not altered and came from an authorised source. |
| DMARC | Policy telling receivers what to do on SPF or DKIM alignment failure, with aggregate reporting. |
| BIMI | Brand Indicators for Message Identification. Puts a verified logo into supporting clients, on top of aligned DMARC. |
| MPP | Apple Mail Privacy Protection. Prefetches images through Apple proxies, inflating and corrupting the open metric. |
| Deliverability | Whether mail reaches the inbox rather than spam. One layer below the category aware retrieval gate. |
| Bounce | A failed delivery. Hard bounces are permanent and must be suppressed immediately; soft bounces are transient. |
| Sender reputation | The provider's running assessment of a sending domain and IP, driven heavily by engagement. |

# List and data

| Term | Meaning |
| --- | --- |
| Single opt in | Subscriber added on form submission, no confirmation step. |
| Double opt in | Subscriber must confirm via a link before being added. Better for quality and consent records. |
| Lead magnet | An incentive offered in exchange for contact details. |
| Segment | A subset of the list, dynamic (auto updating) or static (fixed at creation). |
| Merge tag | A placeholder replaced with subscriber specific data at send time. |
| Suppression list | Addresses that must never receive mail: unsubscribes, complaints, hard bounces. |
| Zero party data | Data a customer proactively and voluntarily shares. The cleanest signal. |
| First party data | Data from direct interactions with your own platforms. |
| Third party data | Data bought from outside aggregators. Fading as third-party cookies are phased out. |

# Customer data and CRM

| Term | Meaning |
| --- | --- |
| CRM | Customer relationship management. The system of record for known customers and the interactions with them. |
| CDP | Customer data platform. Ingests data from every source, resolves identity, and maintains an activation-ready unified profile. |
| Data warehouse | Central store built for analysis and reporting at scale, not real-time activation. |
| Single customer view | One unified profile per person, assembled from every source. |
| Identity resolution | Stitching identifiers across devices and channels into one customer profile. |

# Segmentation and lifecycle

| Term | Meaning |
| --- | --- |
| RFM | Recency, Frequency, Monetary. A behavioural segmentation model scoring customers on how recently, how often, and how much they buy. |
| CLV / LTV | Customer lifetime value. The total past and predicted value of a customer over the relationship. |
| Propensity model | A model predicting the probability a customer takes an action, such as buying or churning. |
| Churn | A customer lapsing or ending the relationship; churn rate is the share who do so in a period. |
| Retention rate | The share of customers retained over a period; its inverse is churn. |
| Lifecycle stage | Where a customer sits in the journey: acquisition, onboarding, engagement, retention, or winback. |
| Loyalty program | A structured points, tier, or referral scheme that rewards repeat business. |
| Referral | Acquisition through an existing customer recommending the brand. |

# Channels and design

| Term | Meaning |
| --- | --- |
| Triggered (behavioural) message | A send fired by a customer's behaviour or state, rather than a schedule. |
| Broadcast (batch) | A send to a segment on a schedule. |
| Orchestration | Deciding, per customer and moment, which message goes on which channel, and whether to send. |
| Frequency cap | A hard ceiling on messages per channel and in total over a rolling window. |
| Preheader (preview text) | The snippet shown after the subject line in the inbox; the third part of the envelope. |
| Responsive design | Layout that adapts to the screen it renders on; most email opens are on mobile. |
| Dark mode | A client display mode that recolours messages; designs must survive the inversion. |
| Alt text | Text shown in place of an image that is blocked or fails to load. |
| A2P 10DLC | The US registration standard for application-to-person SMS over long codes. |
| RCS | Rich Communication Services. The richer successor to SMS, with branding, cards, and read receipts. |
| APNs / FCM | Apple Push Notification service and Firebase Cloud Messaging, the two push delivery pipes. |

# Metrics

| Term | Meaning |
| --- | --- |
| Open rate | Share of delivered mail where the pixel fired. Corrupted by MPP; directional only. |
| Click through rate | Share of delivered mail that produced a link click. The workhorse metric. |
| Click to open rate (CTOR) | Clicks divided by opens. Content engagement, independent of open noise. |
| Conversion rate | Share that produced the downstream target action. The metric that pays. |
| Complaint rate | Share marked as spam. A hard deliverability limit; keep under 0.1%. |
| Reply rate | Share that replied. A strong positive inbox signal even at 1 to 2%. |

# Decisioning and measurement

| Term | Meaning |
| --- | --- |
| Decision support | Machine learning that assists a journey the marketer designed. |
| Decisioning | Machine learning that decides per user what to send, when, and whether to send at all. |
| Holdout | A randomised group deliberately left unmessaged, to measure incremental effect. |
| Uplift | The incremental effect of sending, against an identical user left alone. |
| Persuadable | A user a message wins over who would not have acted otherwise. |
| Contextual bandit | An algorithm that balances exploring uncertain options against exploiting known good ones. |
| CUPED | Controlled experiment using pre experiment data. A variance reduction technique. |
| DiD | Difference in differences. Estimates an effect by comparing change across treated and untreated cohorts over a date. |

# Related

* [Customer data and identity](/foundations/customer-data-and-identity.md)
* [Segmentation models](/foundations/segmentation-models.md)
* [ESP selection](/foundations/esp-selection.md)
* [Legislation and compliance](/references/legislation-and-compliance.md)

# Citations

[1] [Tealium, what is a CDP](https://tealium.com/resource/fundamentals/what-is-a-cdp/)
[2] [TechTarget, RFM analysis](https://www.techtarget.com/searchdatamanagement/definition/RFM-analysis)
[3] [Litmus, email preview text](https://www.litmus.com/blog/the-ultimate-guide-to-preview-text-support)
