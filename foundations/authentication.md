---
type: Playbook
title: Email Authentication
description: How to set up and roll out SPF, DKIM, DMARC, and BIMI, structure sending subdomains, meet bulk sender requirements, and troubleshoot alignment failures before you send.
tags: [authentication, spf, dkim, dmarc, bimi, deliverability, dns, alignment]
timestamp: 2026-06-14T00:00:00Z
---

# What this covers

Authentication is the set of DNS records and signatures that let a receiving mailbox verify your mail is really from you. It is the precondition for inbox placement, not an optimisation. Set it up before your first send, then verify it with the checklist at the end before you turn the tap on.

# The records

* SPF authorises which servers may send for your domain.
* DKIM cryptographically signs the message so the receiver can verify it was not altered and came from an authorised source.
* DMARC tells receivers what to do when SPF or DKIM alignment fails, and sends you aggregate reports (the `rua` tag) on who is sending under your domain. Parse these with a DMARC aggregator.
* BIMI sits on top of a fully aligned DMARC at enforcement and puts your verified logo into supporting clients. Not a measurement instrument, but deliverability table stakes worth claiming.

The three core records do different jobs and you need all three. SPF and DKIM each prove authorisation by a different mechanism, DMARC ties them to the visible From domain and tells receivers what to do on failure. BIMI is optional and depends on the other three being right first.

# How to set up SPF

SPF is a single DNS TXT record published at the root of your sending domain. It lists the mechanisms allowed to send, then ends with an `all` qualifier that decides the verdict for everything else.

```
v=spf1 include:_spf.google.com include:sendgrid.net -all
```

Steps:

1. Identify every service that sends mail as your domain (your ESP, your transactional provider, your own servers).
2. Add each one with the `include:` value the provider documents, or with `ip4:` / `ip6:` for fixed IPs.
3. End with `-all` (hardfail, reject anything not listed) once you are confident the list is complete. Use `~all` (softfail) only as a temporary state while you confirm coverage.
4. Publish exactly one SPF record per domain. Two SPF records is a permanent error and voids SPF entirely.

The pitfall: SPF allows at most 10 DNS lookups when a receiver evaluates the record, counting every `include`, `a`, `mx`, `ptr`, and `redirect`. Chained includes blow this limit quietly and the record then returns permerror, which most receivers treat as a failure. Audit the lookup count, flatten or remove unused includes, and prefer a small fixed set of senders.

# How to set up DKIM

DKIM signs each message with a private key, and receivers fetch the matching public key from a DNS TXT record at a selector you choose.

Steps:

1. Generate a key pair, 2048-bit RSA is the current default, 1024-bit is the floor and should not be used for new setups.
2. Choose a selector, an arbitrary label that lets you run more than one key at once, for example `s1` or `mail2026`.
3. Keep the private key on the signing system (your ESP usually generates and holds it for you).
4. Publish the public key as a TXT record at `<selector>._domainkey.<domain>`.

```
s1._domainkey.example.com  TXT  "v=DKIM1; k=rsa; p=MIIBIjANBgkqhkiG9w0BAQEFAA..."
```

The signature header on outgoing mail names the domain (`d=`) and selector (`s=`) so the receiver knows which record to fetch. Most ESPs do all of this for you, your job is to publish the record they give you and confirm it resolves.

Rotate keys on a schedule. A sensible default is every six to twelve months, and immediately if a key is ever exposed. Rotate by publishing a new selector first, switching signing to it, then removing the old record once no in-flight mail still references it. Running two selectors during the overlap is why selectors exist.

# DMARC rollout

DMARC is a TXT record at `_dmarc.<domain>`. Its policy decides what receivers do when a message fails both SPF and DKIM alignment, and `rua` collects the aggregate reports that tell you who is sending as you.

Alignment is the part people miss. A message passes DMARC only if SPF or DKIM passes and the domain it authenticated is aligned with the visible From domain. SPF alignment compares the From domain to the SPF (envelope/return-path) domain, DKIM alignment compares the From domain to the `d=` in the signature. A message can pass raw SPF or DKIM and still fail DMARC because the authenticated domain does not match From. Relaxed alignment (the default) allows a subdomain to align with its organisational domain, strict alignment requires an exact match.

Roll it out in stages and read the aggregate reports between each stage, never jump straight to reject.

1. Start at `p=none`. This enforces nothing, it only turns on reporting. Publish `rua` and let reports accumulate for two to four weeks as a default observation window.

```
_dmarc.example.com  TXT  "v=DMARC1; p=none; rua=mailto:dmarc@example.com; fo=1"
```

2. Read the reports. Identify every legitimate source and confirm it passes SPF or DKIM with alignment. Fix the gaps (a provider signing with the wrong domain, an unaligned return-path) before you tighten anything.
3. Move to `p=quarantine`, optionally ramping with `pct=` (for example `pct=25` then higher) so only a fraction of failing mail is affected while you watch the reports.

```
_dmarc.example.com  TXT  "v=DMARC1; p=quarantine; pct=25; rua=mailto:dmarc@example.com; fo=1"
```

4. When reports show only spoofed or illegitimate mail failing, move to `p=reject`. This is enforcement, and it is the level the bulk sender rules and BIMI both require.

```
_dmarc.example.com  TXT  "v=DMARC1; p=reject; rua=mailto:dmarc@example.com; fo=1"
```

The whole point of the staged path is that `p=none` lets you discover your own legitimate senders without bouncing real mail, so you reach `p=reject` having already proven nothing legitimate fails.

# Subdomain strategy

Send marketing and [transactional](/foundations/transactional-messaging.md) mail from separate subdomains so a reputation problem in one cannot poison the other. Transactional mail (receipts, confirmations, password resets) is not routed to the Promotions tab the way promotional mail is and tolerates higher volume, so isolating it protects the mail users genuinely need.

A common, readable convention:

* `news.example.com` or `mktg.example.com` for marketing and lifecycle.
* `mail.example.com` or `t.example.com` for transactional.

Each subdomain gets its own SPF and DKIM records. Publish DMARC at the organisational domain so it covers the subdomains by default (relaxed alignment lets a subdomain align up to the parent), and add a subdomain-specific record only if you want a different policy there via the `sp=` tag. Warm each sending subdomain independently, reputation is tracked per sending domain and per IP, not per brand.

# BIMI

BIMI displays your verified logo next to your mail in supporting clients. It is the reward for getting authentication fully right, and it has hard prerequisites:

* DMARC published at enforcement, that is `p=quarantine` or `p=reject` (`p=none` does not qualify).
* A logo in SVG Tiny PS (P/S) format, square, hosted over HTTPS.
* A BIMI TXT record at `default._bimi.<domain>` pointing to that logo.
* For the major mailbox providers, a Verified Mark Certificate (VMC) or Common Mark Certificate (CMC) from an authorised issuer, proving you own the mark. This is the step with real cost and lead time.

Treat BIMI as the last item, only worth starting once DMARC is at enforcement and stable.

# Bulk sender requirements

Since February 2024 any sender of roughly 5,000 or more messages a day to Gmail or Yahoo must authenticate with SPF and DKIM, align DMARC, support one click unsubscribe per RFC 8058, and keep the reported spam rate under 0.3% (0.1% is the safe target). Microsoft enforced equivalent rules from May 2025, and Gmail moved from deferral to rejection in November 2025. See [platform interventions](/references/platform-interventions.md).

To meet them: publish SPF and DKIM as above, get DMARC to at least `p=none` with alignment confirmed (the rules require a DMARC record and that mail authenticates and aligns), include a working `List-Unsubscribe` header with the `List-Unsubscribe-Post` one click form, and watch the spam rate in Google Postmaster Tools so you act before you cross 0.1%.

# Troubleshooting checklist

Before the first send, and whenever placement drops, verify:

- [ ] Exactly one SPF record exists, and it ends in `-all` (or `~all` only as a deliberate temporary state).
- [ ] SPF evaluates within the 10 DNS lookup limit, no permerror.
- [ ] The DKIM public key resolves at `<selector>._domainkey.<domain>` and matches the selector the mail signs with (selector mismatch is a common silent failure).
- [ ] A test message passes DKIM, the `d=` domain aligns with the visible From domain.
- [ ] A DMARC record exists at `_dmarc.<domain>` and `rua` reports are arriving.
- [ ] Aggregate reports show your legitimate sources passing with alignment before you raise the policy.
- [ ] Marketing and transactional are on separate subdomains, each with its own SPF and DKIM.
- [ ] Hard bounces are auto suppressed immediately rather than re-sent to.

Verify with the receiver, not just by reading your own DNS. Send a test to a Gmail and an Outlook account and inspect the Authentication-Results header (it states `spf=`, `dkim=`, and `dmarc=` verdicts plus alignment). Use a public DMARC/SPF/DKIM record checker and a mail-test tool to read the verdicts a real receiver applies. Reading the records in isolation will not surface an alignment failure, only an end-to-end test will.

Missing SPF or DKIM causes deliverability problems and block bounces, so set up authentication before the first send.

# Related

* [Deliverability](/foundations/deliverability.md)
* [Engagement is the new deliverability](/principles/engagement-is-deliverability.md)
* [Bulk sender requirements](/references/platform-interventions.md)

# Citations

[1] [Google, email sender guidelines (SPF, DKIM, DMARC, bulk sender requirements)](https://support.google.com/a/answer/81126)
[2] [RFC 8058, one-click unsubscribe](https://www.rfc-editor.org/rfc/rfc8058)
[3] [RFC 7208, Sender Policy Framework (SPF), including the 10 DNS lookup limit](https://www.rfc-editor.org/rfc/rfc7208)
[4] [RFC 6376, DomainKeys Identified Mail (DKIM) signatures](https://www.rfc-editor.org/rfc/rfc6376)
[5] [RFC 7489, Domain-based Message Authentication, Reporting, and Conformance (DMARC)](https://www.rfc-editor.org/rfc/rfc7489)
[6] [BIMI Group, BIMI implementation and VMC requirements](https://bimigroup.org/)
