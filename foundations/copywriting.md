---
type: Playbook
title: Copywriting
description: How to write subject lines, CTAs, and a sound email skeleton, plus writing so the substance survives a summariser, with a pre-send checklist.
tags: [copywriting, subject-lines, cta, email-anatomy, deliverability, summarisation]
timestamp: 2026-06-14T00:00:00Z
---

## Subject lines and the envelope

The recipient decides on your message from the envelope: sender name, subject line, and snippet, with no open required. Subject and sender do disproportionate work because they are the only signals available before the decision. A subject line that lifts opens through misdirection lifts delete without read at the same rate, which trains the provider against you. Optimise the envelope to set an honest expectation a real human would act on, not to win a click you immediately lose.

How to write one:

1. Front-load the useful fact. Put the amount, the date, the name, or the action in the first few words, because the snippet and the summariser both read left to right and the right-hand side is often truncated. "20% off ends Sunday" before "Don't miss our amazing limited-time event".
2. Keep it short by default. Aim for roughly 50 to 60 characters so it is not truncated on mobile. Longer is fine when the front-loaded fact survives the cut, since the truncation point is what matters, not the total length.
3. Write the preheader as the second line, not a repeat of the subject. Preview text commonly runs roughly 40 to 100 characters depending on the client; use it to add the detail the subject left out, not to echo it.
4. Apply the self-check as a rule: strip the subject to its first few words and read it aloud. If those words still tell the recipient something concrete and true, keep it. If they say nothing without the rest of the line, rewrite so the fact moves forward.

Test subject lines honestly. An A/B subject test on a single send is usually too small to call: opens are noisy and the difference between two lines is often within that noise. Before declaring a winner, check the test has the volume to detect a real difference, see [sample size and power](/measurement/sample-size-and-power.md), and do not over-read a one-off result from a few thousand sends.

## Email anatomy

A single-intent email has a predictable skeleton. Each block does one job, and the order keeps the most important message above the fold and machine-readable.

* **Preheader / preview text.** The first text the client surfaces after the subject. Carry one extra concrete fact here, not a repeat of the subject.
* **Header.** Logo and a thin nav at most. Recognisable sender, minimal links.
* **Hero message.** One headline carrying the single core message in real text. This is the line a scanner and a summariser will keep, so state the offer, change, or news plainly.
* **Primary CTA.** One button, placed near the hero, repeated lower down if the email is long. Same wording each time.
* **Supporting content.** Detail, proof, or secondary context below the primary action, never competing with it.
* **Footer.** Physical address, clear unsubscribe, sender identity. Required and load-bearing for deliverability.
* **Plain-text part.** A real plain-text alternative alongside the HTML. Some clients and summarisers read it, and it keeps the message legible when images are blocked.

## CTAs

Keep one clear primary action per email; messages with a single call to action consistently out-click those that ask for several at once. Mixed intent campaigns, a service email with a CTA bolted on or a promo with disclaimers in the middle, risk being characterised by the dominant block rather than your intent. Single intent messages with explicit verbs in their key blocks survive both scanning and summarisation better. Use a monitored from address, never noreply@, because a reply is one of the strongest positive signals an inbox can read. For how the message then renders across clients, see [message design and rendering](/foundations/message-design-and-rendering.md).

How to write the button:

1. Lead with a verb and name the outcome. "Get 20% off" beats "Click here", "Track my order" beats "Submit", because the copy tells the recipient what happens next.
2. Keep one primary action. If a second action is unavoidable, make it visibly secondary, a text link rather than a competing button.
3. Make it tappable. A real button block, not a bare inline link, sized so a thumb can hit it on a phone.
4. Match the CTA to the subject's promise. The button should deliver the fact the envelope front-loaded, or the open was a bait and switch.

## Spam trigger avoidance

Authentication and engagement matter far more than word lists, but avoid the obvious: all caps subjects, excessive punctuation, heavy image to text ratios, and link shorteners. Image only emails lose the structure the classifier reads, so the model parses your headline, promo code, body, and footer as one flat block. Keep real text in the message.

## Writing for the summariser

On-device and inbox summarisers compress a message to its gist, keeping what is machine readable and dropping brand voice. Lead with the concrete fact, the amount, the name, the time, the action, so a summary has something to keep. A useful self check: if the subject still tells the user something useful when stripped to its first few words, it carries a fact a summariser can keep. The platform research behind this is in [email intelligence research](/references/email-intelligence-research.md).

Concrete rules, with phrasings:

* **Quantify.** "Save 20%" not "Save big". A number survives compression; an adjective does not.
* **Name the date or deadline.** "Ends Sunday 22 June" not "Ending soon". An explicit date is something a summary can carry verbatim.
* **Name the amount or item.** "Your £15 credit" not "a special reward". The specific noun is what the recipient acts on.
* **Use explicit verbs in key blocks.** "Confirm your address by Friday" not "Action may be required". The verb tells the summariser, and the reader, what to do.
* **Put the fact before the framing.** "Order shipped, arrives Tuesday" before any thank-you copy, so the gist holds even if everything after the first clause is dropped.

## Metric to watch

Use click to open rate (CTOR), clicks divided by opens, as the content engagement measure independent of open noise. See [metrics are directional](/principles/metrics-are-directional.md).

## Pre-send copy checklist

* Subject front-loads a concrete fact and reads usefully when stripped to its first few words.
* Subject is short enough that the fact survives mobile truncation (roughly 50 to 60 characters as a default).
* Preheader adds a fact rather than repeating the subject.
* One primary CTA, verb plus outcome, tappable, consistent wording throughout.
* Hero message is real text, not baked into an image.
* From-address is monitored, not noreply@.
* Footer has a working unsubscribe, physical address, and clear sender identity.
* A plain-text alternative is present.
* Any A/B subject test has the volume to call a real difference before a winner is declared.

## Related

* [Message design and rendering](/foundations/message-design-and-rendering.md)
* [Email intelligence research](/references/email-intelligence-research.md)
* [Sample size and power](/measurement/sample-size-and-power.md)
* [Metrics are directional](/principles/metrics-are-directional.md)

## Citations

[1] [Litmus, the email envelope is the from name, subject line, and preview text](https://www.litmus.com/blog/the-ultimate-guide-to-preview-text-support)
[2] [Campaign Monitor, a single CTA receives far more clicks than competing CTAs](https://www.campaignmonitor.com/resources/knowledge-base/do-ctas-help-to-improve-email-response-rates/)
[3] [Campaign Monitor, click-to-open rate as a content-engagement measure](https://www.campaignmonitor.com/resources/knowledge-base/what-are-good-email-metrics/)
