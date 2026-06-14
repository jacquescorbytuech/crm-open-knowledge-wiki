---
type: Principle
title: Email metrics are directional, not precise
description: Open rates especially. Never treat metrics as gospel, and never make major decisions on small differences without statistical rigour.
tags: [principle, metrics, opens, ctor]
timestamp: 2026-06-14T00:00:00Z
---

# Stance

Email metrics are directionally useful, not precisely meaningful. Open rates especially. Never treat them as gospel. Never make a major decision on a small metric difference without proper statistical rigour.

# An open is an image load

What a sender calls an open is an image load: a one pixel image fetched from a tracking server. That fetch happens for many reasons that have nothing to do with a human reading the mail. Apple Mail Privacy Protection fetches it on delivery whether or not the recipient opens, inflating opens by tens of percentage points on Apple heavy lists. Gmail prefetches and proxies images. Spam and security filters fetch it inside the delivery path, sometimes before the mail is delivered, or even when it was rejected. And a Gmail message over 102KB is truncated, cutting off a tracking pixel at the foot of the mail, so a genuine read can record no open at all. The pixel stopped meaning what it meant for two decades. See [platform interventions](/references/platform-interventions.md).

# Two different things called engagement

The engagement a mailbox provider acts on, dwell time, scrolling, replies, deletes, folder moves, the IMAP seen and answered flags, is far richer than anything a sender can see, and it is what actually drives placement. The opens and clicks a sender measures are a thin, noisy proxy for it. Conflating the two is the core error: a move in your open rate is a move in image load behaviour, not direct evidence of how the provider rates you. See [engagement is the new deliverability](/principles/engagement-is-deliverability.md).

# What to use instead

* Click to open rate (CTOR) for content engagement, independent of open noise.
* Click through and downstream conversion for outcome.
* Reply rate, one click unsubscribe timing, and complaint rate for relationship health.

Clicks are sturdier than opens, because providers do not pre-cache the page behind a link, but they are not clean either.

> [!warning] Scanner clicks inflate Microsoft click rates
> Security scanners, notably at Microsoft properties, follow links at scale and can inflate click counts to absurd levels, so a naive click rate at those providers is unreliable. A workable rule is to treat clicks more than a few minutes after delivery as probably human.

And do not confuse a recipient who never loads images, often a real person with strict privacy or security settings, with an abandoned address: purging the former to tidy a rate removes real readers.

Optimising for opens through misdirection lifts delete without read at the same rate, which trains the provider that your recipients open and discard, which damages future placement. Short term wins on cheap metrics compound into deliverability damage.

# Related

* [Test rigorously](/principles/test-rigorously.md)
* [Volume thresholds](/measurement/volume-thresholds.md)
* [Deliverability](/foundations/deliverability.md)
* [Core metrics](/measurement/core-metrics.md)

# Citations

[1] [Word to the Wise, Deliveries and Opens and Clicks](https://www.wordtothewise.com/2024/06/deliveries-and-opens-and-clicks/)
