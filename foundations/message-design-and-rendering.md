---
type: Playbook
title: Message Design and Rendering
description: How to build a message so it renders and reads everywhere it lands, a single-column mobile-first layout with inline CSS, dark-mode and accessibility steps, functional alt text, preheader text, and a pre-send rendering QA checklist, across an inbox landscape where one client dominates and several render the same message differently.
tags: [design, rendering, responsive, dark-mode, accessibility, alt-text, preheader, mjml, qa]
timestamp: 2026-06-14T00:00:00Z
---

## Design for where it actually lands

A message is not rendered once. It is rendered by dozens of clients that disagree about CSS, light and dark, and image handling, and most of them open on a phone. Apple's mail clients alone take the largest single share of opens, with Gmail next and Outlook well behind, so a layout tested only in one desktop client is untested. Design for the spread, not for your own inbox.

## Mobile-first

Most email is opened on a mobile device, and a message that breaks on a small screen is deleted rather than zoomed. Design mobile-first: a single-column layout, type large enough to read without pinching, and tap targets big enough for a thumb. Responsive techniques adapt the same message to the screen it lands on.

## How to build it

A robust email build is deliberately conservative. The steps that keep it intact across the spread:

1. **Start single-column.** One column reflows on a phone without media-query support and degrades to the same layout in clients that strip your CSS. Reach for multi-column only where you can accept it stacking, and stack it by default on mobile.
2. **Constrain the content width.** Set a maximum content width of around 600px, which renders without clipping in desktop clients and scales down on mobile. Let the body fill the viewport below that.
3. **Inline your CSS.** Many clients strip or ignore a `<style>` block, so the styling you depend on for layout and colour should be inline on the elements. Keep a `<style>` block as well for the things inlining cannot do (media queries, `prefers-color-scheme`), but never rely on it alone.
4. **Lay out with tables, not floats or flexbox.** Email CSS support is years behind the browser. Table-based structure renders predictably where modern layout does not. Check any feature you want to lean on against the support tables before you rely on it.
5. **Keep the substance in live text, not images.** Build headlines, offers, and CTAs as real text with a bulletproof (table-and-link) button, so they render with images off, read under a screen reader, and survive dark-mode recolouring.
6. **Use a coding framework to cut breakage.** Hand-writing bulletproof email HTML is error-prone. A framework such as **MJML** compiles a concise syntax down to the table-based, inline-styled markup clients expect, and a tested starter such as the **Cerberus** responsive patterns gives you blocks proven across clients. Either removes a large class of rendering bugs before you test.

## Type and size defaults

Set defaults that read on a phone held at arm's length, then adjust up, never down.

* **Body text** commonly at 14 to 16px or larger; below that, mobile legibility falls off and some clients bump it up for you, breaking your layout.
* **Headings** clearly larger than body, set as real text in a semantic order rather than as images.
* **Line length and spacing** comfortable: generous line height and a single column keep long-form readable on a narrow screen.
* **Tap targets** large enough for a thumb, with space around each so adjacent links are not mis-tapped.

## Dark mode

Every major client now offers a dark mode, and several recolour your message when it is on. A design that assumes a white background, a logo on white, an image with a baked-in light background, dark text with no contrast fallback, can invert into something unreadable. The handling steps:

1. **Do not rely on pure black or pure white.** Clients that auto-invert push extremes hardest, so a near-black or near-white shifts more predictably than the absolute. Choose colours that survive a partial recolour rather than ones that flip to their opposite.
2. **Use transparent-background logos and icons.** A logo baked onto a white tile becomes a white box on a dark background. Export with a transparent background, and give dark-on-light marks a subtle outline or padded container so they stay visible either way.
3. **Set explicit backgrounds and text colours.** State the colours rather than leaving them to default, so a recolouring client has something to work from and you are not relying on its guess.
4. **Add a `prefers-color-scheme` block where supported.** Apple Mail and a few others honour it, letting you supply intentional dark-mode colours instead of accepting the client's automatic inversion. Treat it as an enhancement, not a guarantee.
5. **Test with dark mode on.** Several clients recolour differently, so render the message in dark mode across the clients in your market share, not just the one you use.

## Accessibility

A meaningful share of recipients use assistive technology, and an inaccessible message simply fails for them. The basics carry most of the weight, and they are concrete steps:

1. **Use genuine semantic headings in reading order.** Mark headings as real headings, not bold text, and order the source so a screen reader reads it the way a sighted reader scans it. Visual order and source order should agree.
2. **Set the language and a meaningful title.** Declare the document language so a screen reader pronounces it correctly.
3. **Write descriptive alt text that carries the key info.** The amount, the code, the CTA, anything load-bearing must be in the alt text, not only in the image. Mark purely decorative images as such so a screen reader skips them.
4. **Clear WCAG AA contrast.** Aim for at least 4.5:1 for normal text against its background, and check the dark-mode rendering separately since recolouring can drop a passing pair below the threshold.
5. **Do not rely on colour alone.** Pair colour with text or shape so meaning survives for a recipient who cannot distinguish it.
6. **Keep the substance as real, live text.** Real text resizes, reflows, and reads under assistive technology in a way an image of text never will.

Accessible design also tends to be cleaner design, so the cost is low.

## Alt text

Alt text is the text a client shows in place of an image that is blocked, slow, or failed, and many clients block images by default until the recipient chooses to load them. Without alt text, an image-led message renders as empty boxes. Write functional alt text that carries the image's message, and never let a critical word, the offer, the code, the call to action, live only inside an image. This is also why image-only emails are a [deliverability](/foundations/deliverability.md) risk: the classifier and the summariser read text, not pixels.

## Preheader text

The preheader (preview text) is the snippet a client shows after the subject line in the inbox, the third part of the envelope alongside sender and subject. Left unset, clients pull the first text in the message, often "view in browser" or an address block, wasting the most valuable real estate you have before the open. Write it deliberately to extend the subject line, not repeat it. See [copywriting](/foundations/copywriting.md) for the envelope as a whole.

## Keep real text in the message

Across all of the above runs one rule: keep the substance in live text, not locked in images. It renders when images are blocked, it reads under a screen reader, it survives dark-mode recolouring, and it is the structure the inbox's classifier and summariser parse. Send a proper multipart message with a plain-text part as well as HTML. See [deliverability](/foundations/deliverability.md) and [copywriting](/foundations/copywriting.md).

## Coding for the inbox

Email HTML is not web HTML. Clients strip, rewrite, and ignore CSS in ways no browser would, so the discipline is writing the most robust, accessible markup that degrades gracefully rather than chasing pixel-perfection everywhere. Two community references carry most of this weight and are worth treating as standing tools. **Good Email Code**, by Mark Robbins, is a library of accessible, semantic email-code patterns that explains the reasoning behind each technique and prioritises making the code work over visual consistency. **Can I email**, by Rémi Parmentier (HTeuMeuLeu) and the team at Tilt Studio, is the support-table reference for HTML and CSS features across email clients, in the mould of caniuse.com, so you can check before you rely on a feature whether the clients in your [market share](https://www.litmus.com/email-client-market-share) actually support it.

## Pre-send rendering QA

Run the same checklist before every send, weighted to the clients in your market share. A rendering tool that captures real client screenshots makes most of this a single pass; the rest is a visual read.

* [ ] **Major clients.** Renders correctly in Apple Mail, Gmail, and Outlook at minimum, the three that take most opens, plus any other client significant in your list.
* [ ] **Mobile.** Single column, no horizontal scroll, body text readable without pinching, tap targets large and well spaced.
* [ ] **Dark mode.** Logos and icons stay visible, text keeps contrast, nothing inverts into an unreadable block, checked across clients that recolour.
* [ ] **Images off.** The message still makes sense with images blocked: alt text carries the offer, the code, and the CTA, and the layout does not collapse to empty boxes.
* [ ] **Real text and links.** Headlines, offer, and CTA are live text with a working bulletproof button, not locked inside an image.
* [ ] **Accessibility.** Semantic headings in reading order, AA contrast in both light and dark, no meaning carried by colour alone.
* [ ] **Preheader.** Set deliberately to extend the subject, not a stray "view in browser" or address block.
* [ ] **Multipart.** A plain-text part is present alongside the HTML, plainest first.
* [ ] **Size.** HTML lean enough to stay under the Gmail clipping threshold so the CTA and tracking are not buried. See [email](/channels/email.md).
* [ ] **Links and tracking.** Every link resolves, UTM and tracking parameters are correct, and the unsubscribe link works.

## Related

* [Copywriting](/foundations/copywriting.md)
* [Deliverability](/foundations/deliverability.md)
* [Email](/channels/email.md)
* [Email intelligence research](/references/email-intelligence-research.md)

## Citations

[1] [Litmus, email client market share (Apple largest, then Gmail, then Outlook)](https://www.litmus.com/email-client-market-share)
[2] [Litmus, the how-to guide to responsive email design (mobile opens; messages deleted if they render badly on mobile)](https://www.litmus.com/blog/the-how-to-guide-to-responsive-email-design-infographic)
[3] [Litmus, the ultimate guide to dark mode for email](https://www.litmus.com/blog/the-ultimate-guide-to-dark-mode-for-email-marketers)
[4] [Litmus, the ultimate guide to email accessibility](https://www.litmus.com/blog/ultimate-guide-accessible-emails)
[5] [W3C WCAG, understanding contrast minimum (4.5:1)](https://www.w3.org/WAI/WCAG21/Understanding/contrast-minimum.html)
[6] [Campaign Monitor, alt text shows when images are blocked](https://www.campaignmonitor.com/resources/guides/alt-text-in-email/)
[7] [Litmus, the ultimate guide to email preview text](https://www.litmus.com/blog/the-ultimate-guide-to-preview-text-support)
[8] [Mailchimp, what an email preheader is](https://mailchimp.com/resources/email-preheader/)
[9] [RFC 2046, multipart/alternative (put the plainest part first)](https://www.rfc-editor.org/rfc/rfc2046.html)
[10] [Good Email Code, by Mark Robbins (accessible, semantic email-code patterns)](https://www.goodemailcode.com/)
[11] [Can I email, by Rémi Parmentier (HTeuMeuLeu) and Tilt Studio (HTML/CSS support tables across email clients)](https://www.caniemail.com/)
