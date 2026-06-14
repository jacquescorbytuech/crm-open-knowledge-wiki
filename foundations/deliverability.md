---
type: Playbook
title: Deliverability and Metrics
description: How inbox placement works, how to warm an IP or domain, how to recover from spam, how to monitor complaint rate, the full metrics reference, the Gmail Promotions tab, and MIME structure.
tags: [deliverability, spam, ip-warming, metrics, promotions-tab, mime, postmaster-tools, snds]
timestamp: 2026-06-14T00:00:00Z
---

## How placement works

Inbox placement is decided by machine learning, not rules, and has been since Bayesian spam filtering in the late 1990s. Authentication is the price of entry, set it up before your first send, see [authentication](/foundations/authentication.md). Above that, sender reputation and per recipient engagement decide whether you reach the inbox, which tab, and where inside the tab. Classical deliverability, inbox versus spam, is no longer the whole story: a category- and relevance-aware sorting layer sits above the spam decision and increasingly governs whether an inboxed message is actually seen. The research and platform changes behind that layer are in [email intelligence research](/references/email-intelligence-research.md) and [platform interventions](/references/platform-interventions.md); for day-to-day operations, the levers below are what you act on.

## How to warm a new IP or domain

Reputation is built from a clean engagement signal at rising volume. A cold IP or domain that suddenly emits a large volume looks exactly like a compromised one, so you ramp. Start with your most engaged subscribers (recent openers and clickers), send a small volume, and increase it gradually over days and weeks while watching the complaint rate at each step.

There is no single official schedule. The principle is the schedule: small start, geometric-ish increases, slow down the moment complaints rise. A concrete default ramp to adapt to your list size:

| Day | Volume to most-engaged segment | Check before next step |
| --- | --- | --- |
| 1 to 2 | ~50 to 200 | Complaint rate, hard bounces |
| 3 to 5 | ~500 to 1,000 | Complaint rate, spam folder placement |
| 6 to 10 | ~5,000 | Reputation tier in Postmaster Tools |
| 11 to 20 | ~10,000 to 25,000 | Complaint rate holding under 0.1% |
| 21 onward | Roughly double every few days | Tier stable, complaints flat |

Rules for the ramp:

1. Send only to engaged subscribers until the IP or domain has a stable reputation, then widen.
2. Roughly double volume only when the previous step's complaint rate stayed well under 0.1% and placement held.
3. If complaint rate rises or placement drops, hold or step back a level, do not push through it.
4. Keep sending cadence steady, gaps reset trust, erratic volume reads as suspicious.
5. Warm each sending domain and each IP independently, reputation is tracked per sending domain and per IP, not per brand. See the subdomain strategy in [authentication](/foundations/authentication.md).

## How to recover from spam

If you are landing in spam, work the causes in order.

> [!warning] Pushing more volume never fixes spam placement
> It deepens it. The engaged core is what you rebuild on, not a bigger send.

1. Fix authentication first. Confirm SPF, DKIM, and aligned DMARC all pass with an end-to-end test, this is the price of entry and a silent failure here caps everything else. See the troubleshooting checklist in [authentication](/foundations/authentication.md).
2. Auto-suppress hard bounces immediately, before the next send (see below). Bouncing into dead addresses is a strong negative signal.
3. Prune the disengaged. Remove or suppress addresses with no opens or clicks over a long window, they drag reputation and inflate complaint rate. Done routinely rather than only in a crisis, this is the sunset step of [database health](/foundations/database-health.md).
4. Reduce volume to the engaged core. Cut back to recent openers and clickers only, so the provider sees a clean engagement signal again.
5. Rebuild slowly. Treat the engaged core as a warming exercise and ramp volume back up on the schedule above, widening only as reputation recovers.
6. Monitor at every step in Postmaster Tools and SNDS, watch complaint rate and reputation tier, and slow down the moment either worsens.

Recovery is the warming ramp run on a list that already burned trust, so it is slower. Do not re-add the pruned addresses, they are what put you in spam.

## How to monitor complaint rate

Complaint rate (recipients marking your mail as spam) is a hard deliverability limit. The bulk sender rules cap the reported spam rate at 0.3%, and 0.1% is the safe target you manage to, see [authentication](/foundations/authentication.md) and [platform interventions](/references/platform-interventions.md).

* Watch it in Google Postmaster Tools (the Spam Rate dashboard) and Microsoft SNDS, per sending domain and IP.
* Track it weekly in steady state, and per send while warming or recovering.
* Act before 0.1%, not at it. A rising trend below the line is the warning, treat 0.1% as a ceiling you never reach, not a budget you spend.

> [!danger] 0.3% is a hard breach, not a target
> The bulk sender rules cap the reported spam rate at 0.3%. At or above it you are in breach, expect blocking, and must run the spam-recovery procedure. Manage to 0.1% as the safe ceiling, well below the line.

Action thresholds:

| Spam rate | Action |
| --- | --- |
| Under 0.1% and flat | Normal, continue |
| Rising trend, still under 0.1% | Investigate the recent change (new segment, cadence, content), hold volume |
| At or near 0.1% | Stop widening, cut to the engaged core, prune disengaged |
| At or above 0.3% | You are in breach of bulk sender rules, expect blocking, run the spam-recovery procedure |

A single bad send spikes the rate, so read the trend, but a sustained climb is reputation damage in progress.

## Postmaster Tools and SNDS setup

Set these up before you scale, they are the only platform-cooperative signal you get. They report aggregate deliverability, not per message placement or summarisation.

- [ ] Create a Google Postmaster Tools account and add every sending domain.
- [ ] Verify each domain by publishing the TXT record Postmaster Tools provides.
- [ ] Confirm DMARC is published so Postmaster Tools can attribute and report (see [authentication](/foundations/authentication.md)).
- [ ] Register for Microsoft SNDS and request access for every sending IP range.
- [ ] Add the JMRP (Junk Mail Reporting Program) feedback loop for Microsoft so complaints flow back to suppression.
- [ ] Confirm data is populating, both tools need a few days and a minimum volume before dashboards fill.
- [ ] Set a weekly review and alert on complaint rate and reputation tier changes.

## Hard-bounce auto-suppression

A hard bounce is a permanent failure (the address does not exist). Add hard-bounced addresses to a suppression list automatically and immediately, before the next send, and never mail them again. Continuing to send to dead addresses is a clear negative reputation signal and is one of the fastest ways into spam. Soft bounces (temporary, for example a full mailbox) can be retried, but suppress them too after repeated failures.

## The Promotions tab

Being in Promotions is not a failure: deal seekers actively browse it. Since September 2025 Gmail sorts Promotions by relevance rather than recency by default, so within tab placement is engagement weighted. Engaged senders pin near the top of an actively scanned surface; weak senders sink below the fold and become functionally invisible. The outcome is bimodal, and per sender engagement history decides which half you land in.

## The metrics reference

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

The engagement rows are the ones to distrust. An open is an image load, not a read, and the load can be triggered by privacy proxies, prefetch, or filters in the delivery path rather than by a person. Clicks can be inflated by automated security scanners that follow links at scale, seen most sharply at Microsoft properties, so treat clicks in the first few minutes after delivery with suspicion and lean on later, human looking clicks and downstream conversion. The engagement a provider actually acts on, dwell time, scrolling, replies, and folder moves, is richer than either and is not visible to you. See [email metrics are directional](/principles/metrics-are-directional.md).

## Platform diagnostics

Gmail Postmaster Tools and Microsoft SNDS, set up per the checklist above, are tracked weekly with alerts on complaint rate and reputation tier changes. They report aggregate deliverability, not per message placement or summarisation, but they are the only platform cooperative signal you get. See [platform interventions](/references/platform-interventions.md).

## MIME structure

Send a proper multipart message. Use a `multipart/alternative` container holding both a plain text part and an HTML part, in that order, so a client that prefers text gets a real text version and one that prefers HTML gets the rich version. A missing or empty plain text part is a spam signal and degrades rendering in clients that prefer it. Keep the image to text ratio sane, because a heavy image to text ratio is a Promotions classifier signal, and an all-image email with no real text is a classic spam pattern. If you embed inline images, wrap the alternative part and its images in a `multipart/related` container. The wider rendering question, mobile, dark mode, accessibility, and alt text, is covered in [message design and rendering](/foundations/message-design-and-rendering.md).

## Related

* [Authentication](/foundations/authentication.md)
* [Database health and sunsetting](/foundations/database-health.md)
* [Transactional messaging](/foundations/transactional-messaging.md)
* [Engagement is the new deliverability](/principles/engagement-is-deliverability.md)
* [Message design and rendering](/foundations/message-design-and-rendering.md)
* [Email intelligence research](/references/email-intelligence-research.md)
* [Measuring intermediation](/measurement/measuring-intermediation.md)

## Citations

[1] [Word to the Wise, deliveries and opens and clicks (opens and clicks are noisy, directional signals)](https://www.wordtothewise.com/2024/06/deliveries-and-opens-and-clicks/)
[2] [Google, email sender guidelines (authentication, spam-rate threshold, one-click unsubscribe)](https://support.google.com/a/answer/81126)
[3] [RFC 2046, multipart/alternative (include a plain-text part)](https://www.rfc-editor.org/rfc/rfc2046.html)
[4] [Google Postmaster Tools, spam rate and reputation dashboards](https://support.google.com/mail/answer/9981691)
[5] [Microsoft SNDS, Smart Network Data Services](https://sendersupport.olc.protection.outlook.com/snds/)
[6] [M3AAWG, sender best practices and reputation guidance](https://www.m3aawg.org/published-documents)
