---
type: Playbook
title: Audience sync
description: How to activate CRM segments as audiences on the ad platforms for targeting and suppression, what matching and consent require, and why it extends the owned channels rather than being one.
tags: [audience-sync, customer-match, custom-audiences, paid-media, retargeting, suppression, crm-activation, hashed-match]
timestamp: 2026-06-14T00:00:00Z
---

# What it is

Audience sync is pushing a CRM segment to an ad platform, Meta Custom Audiences, Google Customer Match, and their equivalents, so you can target, or suppress, those customers in paid media. It is the bridge between the owned database and bought reach: the same segment logic that drives an email becomes an ad audience. It is not an owned messaging channel, because you are renting the platform's reach against your list rather than holding a grant to message anyone, which is why it sits in foundations next to the data and segmentation it draws on, not in [channels](/channels/).

# Why it belongs in the contact strategy

Paid media usually runs on a separate team and a separate logic, which is exactly how a customer ends up chased by an acquisition ad the day after they bought. Audience sync brings paid under the one contact strategy. It does two distinct jobs. It extends a lifecycle message into paid media, reinforcing a winback or a launch in the feed alongside the email. And, often more valuable, it suppresses: excluding existing customers from acquisition spend, recent buyers from a promotion, and the unsubscribed from being pursued in paid. Treating paid as a CRM-governed surface is what stops the owned and bought channels from contradicting each other. See [orchestration and frequency](/foundations/orchestration-and-frequency.md).

# How the match works

You upload customer identifiers, email, phone, and sometimes name and address, hashed with SHA-256 before they leave your system or hashed by the platform on upload, and the platform matches them against its own accounts. Only a fraction match, so the addressable audience is always smaller than the list you sent, and the match rate is the number to watch. The audience is rebuilt as you re-sync, so a stale upload targets people whose state has since changed.

# Consent and the privacy line

Syncing identifiers to an ad platform is a data-sharing act, so treat it as processing that needs a lawful basis and that your privacy notice must disclose, not a free internal use of the list. Honour suppression and withdrawal here as you do on the sending channels: a contact who unsubscribed or withdrew consent should be removed from synced audiences, not just from email, or you are pursuing in paid someone who asked you to stop. Match on hashed identifiers, and govern the sync list with the same suppression source as the channels. See [consent and preferences](/foundations/consent-and-preferences.md).

# Operating it

Run it as a governed, scheduled activation rather than a one-off upload.

* **Sync segments, not the whole list.** Push the segment that matches the paid objective, a winback cohort, a high-value seed, a suppression set, not an undifferentiated dump.
* **Refresh on a schedule.** Audiences go stale; re-sync regularly so a customer who just bought or unsubscribed leaves the targeted set promptly.
* **Make suppression a first-class use.** Excluding existing customers from acquisition campaigns and the unsubscribed from retargeting is the cheapest win and the most defensible, and it often beats any targeting gain.
* **Seed lookalikes from your best segment.** A high-value or high-[LTV](/measurement/retention-and-ltv.md) segment is a far better lookalike seed than a generic all-buyers list.
* **Measure incrementally.** Paid audiences are where attribution flatters itself most; hold out and measure lift rather than crediting the platform's reported conversions. See [holdouts and control groups](/measurement/holdouts-and-control-groups.md) and [uplift and incrementality](/measurement/uplift-and-incrementality.md).

# Limits

Match rates cap reach, so the synced audience is always a subset of the segment. The platform owns the audience and sets the matching and policy rules, which keep tightening as privacy regimes constrain identifier matching. And it is bought reach, not an owned grant, so it can extend or refine the owned channels but cannot replace them; the relationship still lives in the customer record, not in the ad account.

# Related

* [Consent and preferences](/foundations/consent-and-preferences.md)
* [Segmentation and data](/foundations/segmentation-and-data.md)
* [Customer data and identity](/foundations/customer-data-and-identity.md)
* [Orchestration and frequency](/foundations/orchestration-and-frequency.md)
* [Holdouts and control groups](/measurement/holdouts-and-control-groups.md)
* [Uplift and incrementality](/measurement/uplift-and-incrementality.md)

# Citations

[1] [Google, get started with Customer Match](https://developers.google.com/google-ads/api/docs/remarketing/audience-segments/customer-match/get-started)
[2] [Google Ads Help, create a customer list](https://support.google.com/google-ads/answer/6276125)
[3] [Meta Business Help Center, about Customer List Custom Audiences](https://www.facebook.com/business/help/341425252616329)
[4] [Meta Business Help Center, customer list formatting and hashing guidelines](https://www.facebook.com/business/help/2082575038703844)
