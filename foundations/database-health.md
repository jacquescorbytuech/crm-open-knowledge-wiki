---
type: Playbook
title: Database Health and Sunsetting
description: The marketing database as a decaying asset, the contact lifecycle from active through dormant to sunset, how to track decay and run hygiene, re-engagement, and sunsetting as one ongoing practice, and why net list growth is acquisition minus decay.
tags: [database-health, list-decay, sunset, hygiene, re-engagement, deliverability, list-growth]
timestamp: 2026-06-14T00:00:00Z
---

## What it is

A marketing database is not a stock that only grows; it is an asset that decays continuously and has to be maintained. People change addresses, lose interest, switch the channel they read, and abandon accounts that later turn into spam traps. Database health is the ongoing practice of keeping the contactable list both deliverable and valuable: managing that decay deliberately rather than letting it accumulate as dead weight. It is the place several scattered ideas in the bundle, hygiene, re-engagement, suppression of the unresponsive, and the sunset policy, come together as one lifecycle for the contact, not the campaign.

The never-engaging tail does not sit there harmlessly, and that is what turns this from housekeeping into reach. Under sender-level reputation it actively drags inbox placement for the engaged contacts who actually convert, so the reachable list is the engaged subset, and sunsetting is a net gain in reachability, not a loss of reach. The lifecycle and running practice that follow are how you act on that, the operational consequence of it, not a reluctant trim of a healthy asset.

## Why a database decays

Decay has several independent sources, and a healthy programme expects all of them.

* **Address and channel churn.** Contacts abandon mailboxes and phone numbers, or simply stop reading the channel they signed up on. The grant is still on file; the human behind it is gone.
* **Disengagement.** A contact who was active goes quiet, then dormant. The address still accepts mail, but the person no longer opens it, which is the more dangerous case because it looks alive.
* **Hard failures.** Hard bounces and complaints remove contacts outright and must be suppressed immediately, per the hygiene SLA in [segmentation and data](/foundations/segmentation-and-data.md).
* **Spam-trap formation.** A long-abandoned address can be recycled by a provider into a spam trap. Continuing to mail the never-engaging tail is how a sender walks into one, which is why dormancy is a deliverability risk and not just a soft metric.

## The contact lifecycle inside the database

Treat each contact as moving through states, and define the transition rules once so the whole programme agrees:

1. **Active.** Engaged inside the recent window; mailed at the normal cadence.
2. **Declining.** Engagement recency slipping; a candidate for reduced frequency and a re-engagement touch.
3. **Dormant.** No engagement across the sunset window, an open or click in email, a tap or session from push and in-app, a reply to an SMS, a purchase in any (a common default is 90 days, set from your own engagement distribution, not a universal figure).
4. **Re-engagement.** Run the win-back sequence in [automation and sequences](/foundations/automation-and-sequences.md) once, as a deliberate last attempt, not an indefinite drip.
5. **Sunset.** A contact who does not respond is moved out of regular sending and suppressed from broadcast. Keep the sunset criteria identical across the flow and the segment so they never disagree, as noted in [segmentation and data](/foundations/segmentation-and-data.md).

This is a lifecycle of the database itself, parallel to the customer [lifecycle mapping](/foundations/lifecycle-mapping.md) but read from the angle of deliverability and list quality rather than the customer's journey.

## Why it pays to shrink the list on purpose

Sunsetting feels like destroying the asset you spent to build, which is why so many programmes refuse to do it. The logic runs the other way. Sender-level engagement now governs placement for the whole list, so the never-engaging tail does not sit there harmlessly; it drags inbox placement down for the engaged contacts who do convert. Removing dead weight raises the deliverability of everyone who remains. This is the operational expression of [list quality over size](/principles/list-quality-over-size.md) and the mechanism in [engagement is the new deliverability](/principles/engagement-is-deliverability.md): the reachable list is the engaged subset, and protecting it is worth more than the headline count.

## Running it

* **Track the engagement-recency distribution, not just the total.** Watch how the list splits across active, declining, and dormant over time. A list whose total is flat but whose active share is falling is decaying under a healthy-looking number.
* **Run hygiene to an SLA.** Suppress hard bounces and complaints immediately and permanently; the written thresholds live in [segmentation and data](/foundations/segmentation-and-data.md).
* **Re-engage once, then sunset.** A single, well-timed win-back attempt, then move the unresponsive to the sunset segment. Endless re-engagement to the dormant is the failure mode it is meant to prevent.
* **Suppress, do not delete, by default.** Keep sunsetted contacts on a suppression record so they are not re-imported and re-mailed later, which is how a sunset quietly undoes itself.
* **Measure net growth, not gross adds.** Net list growth is acquisition minus decay. A programme reporting only new sign-ups while ignoring decay can be shrinking its engaged base while claiming growth. Read database health alongside [list building](/foundations/list-building.md), which feeds the top of the same pipe.

## Related

* [List quality over size](/principles/list-quality-over-size.md)
* [Engagement is the new deliverability](/principles/engagement-is-deliverability.md)
* [List building](/foundations/list-building.md)
* [Segmentation and data](/foundations/segmentation-and-data.md)
* [Automation and sequences](/foundations/automation-and-sequences.md)
* [Deliverability](/foundations/deliverability.md)
* [Consent and preferences](/foundations/consent-and-preferences.md)

## Citations

[1] [Google, email sender guidelines (engagement drives reputation and placement)](https://support.google.com/a/answer/81126)
[2] [Word to the Wise, deliveries and opens and clicks (engagement as the placement signal)](https://www.wordtothewise.com/2024/06/deliveries-and-opens-and-clicks/)
