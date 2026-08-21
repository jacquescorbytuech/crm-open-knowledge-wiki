---
type: Principle
title: Email metrics are directional, not precise
description: Open rates especially. Never treat metrics as gospel, and never make major decisions on small differences without statistical rigour.
tags: [principle, metrics, opens, ctor]
generated:
  by: human:jacquescorbytuech
  at: 2026-06-14T00:00:00Z
sources:
  - id: word-to-the-wise-deliveries-and-opens
    resource: https://www.wordtothewise.com/2024/06/deliveries-and-opens-and-clicks/
    title: "Word to the Wise, Deliveries and Opens and Clicks"
---

## Stance

Email metrics are directionally useful, not precisely meaningful. The engagement a mailbox provider acts on, dwell, scrolling, replies, moves out of spam, is a different thing from the opens and clicks you can measure. Optimise the proxy as if it were the real signal and you train the provider against you, damaging placement. Open rates especially. Never treat them as gospel. Never make a major decision on a small metric difference without proper statistical rigour.

The proxy trap is not email's alone. A push delivery receipt confirms the OS accepted the payload, not that anyone saw it; an SMS carrier `DLR` is advisory and routinely lies; an in-app impression counts a render, not attention. Every channel hands you a cheap surface metric that stands in for a behaviour you cannot see. The same discipline applies throughout: treat it as direction and measure the outcome. Email's proxy is the most studied and the most distorted of these.

## An open is an image load

What a sender calls an open is an image load: a one pixel image fetched from a tracking server. That fetch happens for many reasons that have nothing to do with a human reading the mail. Apple Mail Privacy Protection fetches it on delivery whether or not the recipient opens, inflating opens by tens of percentage points on Apple heavy lists. Gmail prefetches and proxies images. Spam and security filters fetch it inside the delivery path, sometimes before the mail is delivered, or even when it was rejected. And a Gmail message over 102KB is truncated, cutting off a tracking pixel at the foot of the mail so that a genuine read can record no open at all. The pixel stopped meaning what it meant for two decades. See [platform interventions](/references/platform-interventions.md).

## Two different things called engagement

The engagement a mailbox provider acts on, dwell time, scrolling, replies, deletes, folder moves, the IMAP seen and answered flags, is far richer than anything a sender can see. It is also the signal that actually drives placement. The opens and clicks a sender measures are a thin, noisy proxy for it. A move in your open rate is a move in image load behaviour, not direct evidence of how the provider rates you. See [engagement is the new deliverability](/principles/engagement-is-deliverability.md).

## What to use instead

* Click to open rate (CTOR) for content engagement, independent of open noise.
* Click through and downstream conversion for outcome.
* Reply rate, one click unsubscribe timing, and complaint rate for relationship health.

Clicks are sturdier than opens, because providers do not pre-cache the page behind a link, but they are not clean either.

> [!warning] Scanner clicks inflate Microsoft click rates
> Security scanners, notably at Microsoft properties, follow links at scale and can inflate click counts to absurd levels, which makes a naive click rate at those providers unreliable. A workable rule is to treat clicks more than a few minutes after delivery as probably human.

And do not confuse a recipient who never loads images, often a real person with strict privacy or security settings, with an abandoned address: purging the former to tidy a rate removes real readers.

Optimising for opens through misdirection lifts delete without read at the same rate, which trains the provider that your recipients open and discard, which damages future placement. Short term wins on cheap metrics compound into deliverability damage.

## Related

* [Test rigorously](/principles/test-rigorously.md)
* [Volume thresholds](/measurement/volume-thresholds.md)
* [Deliverability](/foundations/deliverability.md)
* [Core metrics](/measurement/core-metrics.md)
