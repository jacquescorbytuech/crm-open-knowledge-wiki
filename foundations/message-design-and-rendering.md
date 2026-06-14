---
type: Playbook
title: Message Design and Rendering
description: How a message is built so it renders and reads everywhere it lands, mobile-first layout, dark mode, accessibility, alt text, and preheader text, across an inbox landscape where one client dominates and several render the same message differently.
tags: [design, rendering, responsive, dark-mode, accessibility, alt-text, preheader]
timestamp: 2026-06-14T00:00:00Z
---

# Design for where it actually lands

A message is not rendered once. It is rendered by dozens of clients that disagree about CSS, light and dark, and image handling, and most of them open on a phone. Apple's mail clients alone take the largest single share of opens, with Gmail next and Outlook well behind, so a layout tested only in one desktop client is untested. Design for the spread, not for your own inbox.

# Mobile-first

Most email is opened on a mobile device, and a message that breaks on a small screen is deleted rather than zoomed. Design mobile-first: a single-column layout, type large enough to read without pinching, and tap targets big enough for a thumb. Responsive techniques adapt the same message to the screen it lands on.

# Dark mode

Every major client now offers a dark mode, and several recolour your message when it is on. A design that assumes a white background, a logo on white, an image with a baked-in light background, dark text with no contrast fallback, can invert into something unreadable. Test in dark mode and use transparent assets and explicit background handling so the message survives the recolour.

# Accessibility

A meaningful share of recipients use assistive technology, and an inaccessible message simply fails for them. The basics carry most of the weight: a real semantic structure (genuine headings, logical order) that a screen reader can follow, colour contrast that clears the WCAG minimum of 4.5:1 for normal text, and not relying on colour alone to carry meaning. Accessible design also tends to be cleaner design, so the cost is low.

# Alt text

Alt text is the text a client shows in place of an image that is blocked, slow, or failed, and many clients block images by default until the recipient chooses to load them. Without alt text, an image-led message renders as empty boxes. Write functional alt text that carries the image's message, and never let a critical word, the offer, the code, the call to action, live only inside an image. This is also why image-only emails are a [deliverability](/foundations/deliverability.md) risk: the classifier and the summariser read text, not pixels.

# Preheader text

The preheader (preview text) is the snippet a client shows after the subject line in the inbox, the third part of the envelope alongside sender and subject. Left unset, clients pull the first text in the message, often "view in browser" or an address block, wasting the most valuable real estate you have before the open. Write it deliberately to extend the subject line, not repeat it. See [copywriting](/foundations/copywriting.md) for the envelope as a whole.

# Keep real text in the message

Across all of the above runs one rule: keep the substance in live text, not locked in images. It renders when images are blocked, it reads under a screen reader, it survives dark-mode recolouring, and it is the structure the inbox's classifier and summariser parse. Send a proper multipart message with a plain-text part as well as HTML. See [deliverability](/foundations/deliverability.md) and [copywriting](/foundations/copywriting.md).

# Related

* [Copywriting](/foundations/copywriting.md)
* [Deliverability](/foundations/deliverability.md)
* [Email](/channels/email.md)
* [Email intelligence research](/references/email-intelligence-research.md)

# Citations

[1] [Litmus, email client market share (Apple largest, then Gmail, then Outlook)](https://www.litmus.com/email-client-market-share)
[2] [Litmus, the how-to guide to responsive email design (mobile opens; messages deleted if they render badly on mobile)](https://www.litmus.com/blog/the-how-to-guide-to-responsive-email-design-infographic)
[3] [Litmus, the ultimate guide to dark mode for email](https://www.litmus.com/blog/the-ultimate-guide-to-dark-mode-for-email-marketers)
[4] [Litmus, the ultimate guide to email accessibility](https://www.litmus.com/blog/ultimate-guide-accessible-emails)
[5] [W3C WCAG, understanding contrast minimum (4.5:1)](https://www.w3.org/WAI/WCAG21/Understanding/contrast-minimum.html)
[6] [Campaign Monitor, alt text shows when images are blocked](https://www.campaignmonitor.com/resources/guides/alt-text-in-email/)
[7] [Litmus, the ultimate guide to email preview text](https://www.litmus.com/blog/the-ultimate-guide-to-preview-text-support)
[8] [Mailchimp, what an email preheader is](https://mailchimp.com/resources/email-preheader/)
[9] [RFC 2046, multipart/alternative (put the plainest part first)](https://www.rfc-editor.org/rfc/rfc2046.html)
