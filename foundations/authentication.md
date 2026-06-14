---
type: Playbook
title: Email Authentication
description: SPF, DKIM, DMARC, and BIMI setup and troubleshooting, the transactional versus marketing distinction, and the bulk sender requirements.
tags: [authentication, spf, dkim, dmarc, bimi, deliverability]
timestamp: 2026-06-14T00:00:00Z
---

# What this covers

Authentication is the set of DNS records and signatures that let a receiving mailbox verify your mail is really from you. It is the precondition for inbox placement, not an optimisation. Set it up before your first send.

# The records

* SPF authorises which servers may send for your domain.
* DKIM cryptographically signs the message so the receiver can verify it was not altered and came from an authorised source.
* DMARC tells receivers what to do when SPF or DKIM alignment fails, and sends you aggregate reports (the `rua` tag) on who is sending under your domain. Parse these with a DMARC aggregator.
* BIMI sits on top of a fully aligned DMARC and puts your verified logo into supporting clients. Not a measurement instrument, but deliverability table stakes worth claiming.

# Bulk sender requirements

Since February 2024 any sender of roughly 5,000 or more messages a day to Gmail or Yahoo must authenticate with SPF and DKIM, align DMARC, support one click unsubscribe per RFC 8058, and keep the reported spam rate under 0.3% (0.1% is the safe target). Microsoft enforced equivalent rules from May 2025, and Gmail moved from deferral to rejection in November 2025. See [platform interventions](/references/platform-interventions.md).

# Transactional versus marketing

Transactional mail (receipts, confirmations, password resets) is not routed to the Promotions tab the way promotional mail is, and tolerates higher volume. Keep the two streams cleanly separated, ideally on distinct subdomains, so a marketing reputation problem cannot poison transactional delivery.

# Common mistake

Missing SPF or DKIM causes deliverability problems and block bounces. Set up authentication before the first send, and auto suppress hard bounces immediately rather than re-sending to them.

# Related

* [Deliverability](/foundations/deliverability.md)
* [Engagement is the new deliverability](/principles/engagement-is-deliverability.md)
* [Bulk sender requirements](/references/platform-interventions.md)

# Citations

[1] [Google, email sender guidelines (SPF, DKIM, DMARC, bulk sender requirements)](https://support.google.com/a/answer/81126)
[2] [RFC 8058, one-click unsubscribe](https://www.rfc-editor.org/rfc/rfc8058)
