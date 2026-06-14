---
type: Playbook
title: Deliverability and Metrics
description: How inbox placement works, getting out of spam, IP warming, the full metrics reference, the Gmail Promotions tab, and MIME structure.
tags: [deliverability, spam, ip-warming, metrics, promotions-tab, mime]
timestamp: 2026-06-14T00:00:00Z
---

# How placement works

Inbox placement is decided by machine learning, not rules, and has been since Bayesian spam filtering in the late 1990s. Authentication is the entry gate. Above it, sender reputation and per recipient engagement decide whether you reach the inbox, which tab, and where inside the tab. Classical deliverability, inbox versus spam, is no longer the whole story: a category- and relevance-aware sorting layer sits above the spam decision and increasingly governs whether an inboxed message is actually seen. The research and platform changes behind that layer are in [email intelligence research](/references/email-intelligence-research.md) and [platform interventions](/references/platform-interventions.md); for day-to-day operations, the levers below are what you act on.

# Getting out of spam

Fix authentication first. Then prune the dead weight, because complaint rate and low engagement are what put you there. Warm a new IP or domain gradually, starting with your most engaged subscribers and increasing volume over days and weeks, so the provider sees a clean engagement signal before you scale.

# The Promotions tab

Being in Promotions is not a failure: deal seekers actively browse it. Since September 2025 Gmail sorts Promotions by relevance rather than recency by default, so within tab placement is engagement weighted. Engaged senders pin near the top of an actively scanned surface; weak senders sink below the fold and become functionally invisible. The outcome is bimodal, and per sender engagement history decides which half you land in.

# The metrics reference

| Metric | What it tells you | Caveat |
| --- | --- | --- |
| Delivery rate | Accepted by the receiving server | Not the same as inbox placement |
| Open rate | An image load fired | Not a read; corrupted by MPP, prefetch, and filter fetches; directional only |
| Click through rate | Clicked a link | The workhorse engagement metric |
| Click to open rate (CTOR) | Content engagement | Independent of open noise |
| Conversion | Downstream action | The metric that pays; needs volume to read |
| Complaint rate | Marked as spam | Hard deliverability limit, keep under 0.1% |
| Unsubscribe rate and timing | Relationship decay | One click timing is a new, granular signal |
| Reply rate | Strong positive inbox signal | Even 1 to 2% improves placement |
| Bounce rate | Hard and soft delivery failures | Suppress hard bounces immediately |

Two cautions on the engagement rows. An open is an image load, not a read, and the load can be triggered by privacy proxies, prefetch, or filters in the delivery path rather than by a person. Clicks can be inflated by automated security scanners that follow links at scale, seen most sharply at Microsoft properties, so treat clicks in the first few minutes after delivery with suspicion and lean on later, human looking clicks and downstream conversion. The engagement a provider actually acts on, dwell time, scrolling, replies, and folder moves, is richer than either and is not visible to you. See [email metrics are directional](/principles/metrics-are-directional.md).

# Platform diagnostics

Set up Gmail Postmaster Tools and Microsoft SNDS for every sending IP and domain, track them weekly, and alert on complaint rate and reputation tier changes. They report aggregate deliverability, not per message placement or summarisation, but they are the only platform cooperative signal you get. See [platform interventions](/references/platform-interventions.md).

# MIME structure

Send a proper multipart MIME message with both a plain text and an HTML part. A missing or empty plain text part is a spam signal and degrades rendering in clients that prefer it. Keep image to text ratio sane, because a heavy image to text ratio is a Promotions classifier signal. The wider rendering question, mobile, dark mode, accessibility, and alt text, is covered in [message design and rendering](/foundations/message-design-and-rendering.md).

# Related

* [Engagement is the new deliverability](/principles/engagement-is-deliverability.md)
* [Message design and rendering](/foundations/message-design-and-rendering.md)
* [Email intelligence research](/references/email-intelligence-research.md)
* [Measuring intermediation](/measurement/measuring-intermediation.md)

# Citations

[1] [Word to the Wise, deliveries and opens and clicks (opens and clicks are noisy, directional signals)](https://www.wordtothewise.com/2024/06/deliveries-and-opens-and-clicks/)
[2] [Google, email sender guidelines (authentication, spam-rate threshold, one-click unsubscribe)](https://support.google.com/a/answer/81126)
[3] [RFC 2046, multipart/alternative (include a plain-text part)](https://www.rfc-editor.org/rfc/rfc2046.html)
