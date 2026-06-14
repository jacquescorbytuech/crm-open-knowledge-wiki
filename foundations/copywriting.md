---
type: Playbook
title: Copywriting
description: Subject lines, email anatomy, CTAs, spam trigger avoidance, and writing so the substance survives a summariser.
tags: [copywriting, subject-lines, cta, deliverability, summarisation]
timestamp: 2026-06-14T00:00:00Z
---

# Subject lines and the envelope

The recipient decides on your message from the envelope: sender name, subject line, and snippet, with no open required. Subject and sender do disproportionate work because they are the only signals available before the decision. A subject line that lifts opens through misdirection lifts delete without read at the same rate, which trains the provider against you. Optimise the envelope to set an honest expectation a real human would act on, not to win a click you immediately lose.

# Anatomy and CTAs

Keep one clear primary action per email; messages with a single call to action consistently out-click those that ask for several at once. Mixed intent campaigns, a service email with a CTA bolted on or a promo with disclaimers in the middle, risk being characterised by the dominant block rather than your intent. Single intent messages with explicit verbs in their key blocks survive both scanning and summarisation better. Use a monitored from address, never noreply@, because a reply is one of the strongest positive signals an inbox can read. For how the message then renders across clients, see [message design and rendering](/foundations/message-design-and-rendering.md).

# Spam trigger avoidance

Authentication and engagement matter far more than word lists, but avoid the obvious: all caps subjects, excessive punctuation, heavy image to text ratios, and link shorteners. Image only emails lose the structure the classifier reads, so the model parses your headline, promo code, body, and footer as one flat block. Keep real text in the message.

# Writing for the summariser

On-device and inbox summarisers compress a message to its gist, keeping what is machine readable and dropping brand voice. Lead with the concrete fact, the amount, the name, the time, the action, so a summary has something to keep. A useful self check: if the subject still tells the user something useful when stripped to its first few words, it carries a fact a summariser can keep. The platform research behind this is in [email intelligence research](/references/email-intelligence-research.md).

# Metric to watch

Use click to open rate (CTOR), clicks divided by opens, as the content engagement measure independent of open noise. See [metrics are directional](/principles/metrics-are-directional.md).

# Related

* [Message design and rendering](/foundations/message-design-and-rendering.md)
* [Email intelligence research](/references/email-intelligence-research.md)
* [Metrics are directional](/principles/metrics-are-directional.md)

# Citations

[1] [Litmus, the email envelope is the from name, subject line, and preview text](https://www.litmus.com/blog/the-ultimate-guide-to-preview-text-support)
[2] [Campaign Monitor, a single CTA receives far more clicks than competing CTAs](https://www.campaignmonitor.com/resources/knowledge-base/do-ctas-help-to-improve-email-response-rates/)
[3] [Campaign Monitor, click-to-open rate as a content-engagement measure](https://www.campaignmonitor.com/resources/knowledge-base/what-are-good-email-metrics/)
