---
type: Playbook
title: Message Design and Rendering
description: How to build a message so it renders and reads everywhere it lands, a single-column mobile-first layout with inline CSS, dark-mode and accessibility steps, functional alt text, preheader text and a pre-send rendering QA checklist for email as the hard case, plus how SMS, RCS, push, in-app and wallet passes each constrain the design differently.
tags: [design, rendering, responsive, dark-mode, accessibility, alt-text, preheader, mjml, qa]
generated:
  by: human:jacquescorbytuech
  at: 2026-08-20T00:00:00Z
sources:
  - id: litmus-email-client-market-share-apple-largest
    resource: https://www.litmus.com/email-client-market-share
    title: "Litmus, email client market share (Apple largest, then Gmail, then Outlook)"
  - id: litmus-the-how-to-guide-to-responsive
    resource: https://www.litmus.com/blog/the-how-to-guide-to-responsive-email-design-infographic
    title: "Litmus, the how-to guide to responsive email design (mobile opens; messages deleted if they render badly on mobile)"
  - id: litmus-the-ultimate-guide-to-dark-mode
    resource: https://www.litmus.com/blog/the-ultimate-guide-to-dark-mode-for-email-marketers
    title: "Litmus, the ultimate guide to dark mode for email"
  - id: litmus-the-ultimate-guide-to-email-accessibility
    resource: https://www.litmus.com/blog/ultimate-guide-accessible-emails
    title: "Litmus, the ultimate guide to email accessibility"
  - id: w3c-wcag-understanding-contrast-minimum-4-5
    resource: https://www.w3.org/WAI/WCAG21/Understanding/contrast-minimum.html
    title: "W3C WCAG, understanding contrast minimum (4.5:1)"
  - id: campaign-monitor-alt-text-shows-when-images
    resource: https://www.campaignmonitor.com/resources/guides/alt-text-in-email/
    title: "Campaign Monitor, alt text shows when images are blocked"
  - id: litmus-the-ultimate-guide-to-email-preview
    resource: https://www.litmus.com/blog/the-ultimate-guide-to-preview-text-support
    title: "Litmus, the ultimate guide to email preview text"
  - id: mailchimp-what-an-email-preheader-is
    resource: https://mailchimp.com/resources/email-preheader/
    title: "Mailchimp, what an email preheader is"
  - id: rfc-2046-multipart-alternative-put-the-plainest
    resource: https://www.rfc-editor.org/rfc/rfc2046.html
    title: "RFC 2046, multipart/alternative (put the plainest part first)"
  - id: good-email-code-by-mark-robbins-accessible
    resource: https://www.goodemailcode.com/
    title: "Good Email Code, by Mark Robbins (accessible, semantic email-code patterns)"
  - id: can-i-email-by-r-mi-parmentier
    resource: https://www.caniemail.com/
    title: "Can I email, by Rémi Parmentier (HTeuMeuLeu) and Tilt Studio (HTML/CSS support tables across email clients)"
  - id: mjml-a-markup-language-that-compiles-to
    resource: https://mjml.io/
    title: "MJML, a markup language that compiles to responsive, table-based email HTML"
  - id: cerberus-by-ted-goas-a-set-of
    resource: https://www.cerberusemail.com/
    title: "Cerberus, by Ted Goas, a set of tested responsive email patterns"
---

## Design for where it actually lands

A message is not rendered once. Email is the unforgiving case: it is rendered by dozens of clients that disagree about light and dark, CSS and image handling, most of them on a phone. Because Apple's mail clients alone take the largest single share of opens, with Gmail next and Outlook well behind, a layout tested only in one desktop client is untested. The other channels constrain the design differently, a fixed OS template for push, plain text for SMS, native components you control in-app, but the rule is the same everywhere: design for the surface as it actually renders, not for the preview in front of you.

## Mobile-first

Most email is opened on a mobile device, where a message that breaks on a small screen is deleted rather than zoomed. Design mobile-first: a single-column layout, type large enough to read without pinching and tap targets big enough for a thumb. Responsive techniques adapt the same message to the screen it lands on.

## How to build it

A resilient email build is deliberately conservative. The steps that keep it intact across the spread:

1. **Start single-column.** One column reflows on a phone without media-query support and degrades to the same layout in clients that strip your CSS. Reach for multi-column only where you can accept it stacking; on mobile, stack it by default.
2. **Constrain the content width.** Set a maximum content width of around 600px, which renders without clipping in desktop clients and scales down on mobile. Let the body fill the viewport below that.
3. **Inline your CSS.** Many clients strip or ignore a `<style>` block, which is why the styling you depend on for layout and colour belongs inline on the elements. Keep a `<style>` block as well for the things inlining cannot do (media queries, `prefers-color-scheme`), but never rely on it alone.
4. **Lay out with tables, not floats or flexbox.** Email CSS support is years behind the browser. Table-based structure renders predictably where modern layout does not. Check any feature you want to lean on against the support tables before you rely on it.
5. **Keep the substance in live text, not images.** Build headlines, offers and CTAs as real text with a bulletproof (table-and-link) button, so they render with images off, read under a screen reader and survive dark-mode recolouring.
6. **Treat frameworks as an aid, not a substitute for skill.** Hand-written HTML is the standard a talented email developer works to, giving the most control over how a message renders across the client spread. Nothing replaces that judgement. Frameworks can speed the work: **MJML** compiles a concise syntax down to the table-based, inline-styled markup clients expect; a tested starter such as the **Cerberus** responsive patterns gives you blocks proven across clients. But they constrain what you can express and still need a developer who understands the underlying markup to extend, debug and verify the output. Reach for them to save time, not to skip the expertise.

## Type and size defaults

Set defaults that read on a phone held at arm's length, then adjust up, never down.

* **Body text** commonly at 14 to 16px or larger; below that, mobile legibility falls off and some clients bump it up for you, breaking your layout.
* **Headings** clearly larger than body, set as real text in a semantic order rather than as images.
* **Line length and spacing** comfortable: generous line height and a single column keep long-form readable on a narrow screen.
* **Tap targets** large enough for a thumb, with space around each so adjacent links are not mis-tapped.

## Dark mode

Every major client now offers a dark mode, several of which recolour your message when it is on. A design that assumes a white background, a logo on white, an image with a baked-in light background, dark text with no contrast fallback, can invert into something unreadable.

1. **Do not rely on pure black or pure white.** Clients that auto-invert push extremes hardest, which makes a near-black or near-white shift more predictably than the absolute. Choose colours that survive a partial recolour rather than ones that flip to their opposite.
2. **Use transparent-background logos and icons.** A logo baked onto a white tile becomes a white box on a dark background. Export with a transparent background, giving dark-on-light marks a subtle outline or padded container so they stay visible either way.
3. **Set explicit backgrounds and text colours.** State the colours rather than leaving them to default, so a recolouring client has something to work from and you are not relying on its guess.
4. **Add a `prefers-color-scheme` block where supported.** Apple Mail and a few others honour it, letting you supply intentional dark-mode colours instead of accepting the client's automatic inversion. Treat it as an enhancement, not a guarantee.
5. **Test with dark mode on.** Since several clients recolour differently, render the message in dark mode across the clients in your market share, not just the one you use.

## Accessibility

A meaningful share of recipients use assistive technology, for whom an inaccessible message simply fails. The basics get you most of the way:

1. **Use genuine semantic headings in reading order.** Mark headings as real headings, not bold text. Order the source so a screen reader reads it the way a sighted reader scans it. Visual order and source order should agree.
2. **Set the language and a meaningful title.** Declare the document language so a screen reader pronounces it correctly.
3. **Write descriptive alt text with the key info.** The amount, the code, the CTA, anything the message depends on must be in the alt text, not only in the image. Mark purely decorative images as such so a screen reader skips them.
4. **Clear WCAG AA contrast.** Aim for at least 4.5:1 for normal text against its background, checking the dark-mode rendering separately since recolouring can drop a passing pair below the threshold.
5. **Do not rely on colour alone.** Pair colour with text or shape so meaning survives for a recipient who cannot distinguish it.
6. **Keep the substance as real, live text.** Real text resizes, reflows and reads under assistive technology in a way an image of text never will.

Accessible design also tends to be cleaner design, which keeps the cost low.

## Alt text

Alt text is the text a client shows in place of an image that is blocked, slow or failed. Many clients block images by default until the recipient chooses to load them. Without alt text, an image-led message renders as empty boxes. Write functional alt text that states the image's message. Never leave a critical word, the offer, the code, the call to action, only inside an image. This is also why image-only emails are a [deliverability](/foundations/deliverability.md) risk: the classifier and the summariser read text, not pixels.

## Preheader text

The preheader (preview text) is the snippet a client shows after the subject line in the inbox, the third part of the envelope alongside sender and subject. Left unset, clients pull the first text in the message, often "view in browser" or an address block, wasting the most valuable real estate you have before the open. Write it deliberately to extend the subject line, not repeat it. See [copywriting](/foundations/copywriting.md) for the envelope as a whole.

## Keep real text in the message

The substance belongs in live text, not locked in images. It renders when images are blocked; it reads under a screen reader; it survives dark-mode recolouring; it is the structure the inbox's classifier and summariser parse. Send a proper multipart message with a plain-text part as well as HTML. See [deliverability](/foundations/deliverability.md) and [copywriting](/foundations/copywriting.md).

## Coding for the inbox

Email HTML is not web HTML. Clients strip, rewrite and ignore CSS in ways no browser would. The discipline is writing the most resilient, accessible markup that degrades gracefully rather than chasing pixel-perfection everywhere. Two community references cover most of this and are worth treating as standing tools. **Good Email Code**, by Mark Robbins, is a library of accessible, semantic email-code patterns that explains the reasoning behind each technique and prioritises making the code work over visual consistency. **Can I email**, by Rémi Parmentier (HTeuMeuLeu) and the team at Tilt Studio, is the support-table reference for HTML and CSS features across email clients, in the mould of caniuse.com. Before relying on a feature, check whether the clients in your [market share](https://www.litmus.com/email-client-market-share) actually support it.

## Pre-send rendering QA

Run the same checklist before every send, weighted to the clients in your market share. A rendering tool that captures real client screenshots makes most of this a single pass; the rest is a visual read.

* [ ] **Major clients.** Renders correctly in Apple Mail, Gmail and Outlook at minimum, the three that take most opens, plus any other client significant in your list.
* [ ] **Mobile.** Single column, no horizontal scroll, body text readable without pinching, tap targets large and well spaced.
* [ ] **Dark mode.** Logos and icons stay visible, text keeps contrast, nothing inverts into an unreadable block, checked across clients that recolour.
* [ ] **Images off.** The message still makes sense with images blocked: alt text covers the offer, the code and the CTA; the layout does not collapse to empty boxes.
* [ ] **Real text and links.** Headlines, offer and CTA are live text with a working bulletproof button, not locked inside an image.
* [ ] **Accessibility.** Semantic headings in reading order, AA contrast in both light and dark, no meaning conveyed by colour alone.
* [ ] **Preheader.** Set deliberately to extend the subject, not a stray "view in browser" or address block.
* [ ] **Multipart.** A plain-text part is present alongside the HTML, plainest first.
* [ ] **Size.** HTML lean enough to stay under the Gmail clipping threshold so the CTA and tracking are not buried. See [email](/channels/email.md).
* [ ] **Links and tracking.** Every link resolves; UTM and tracking parameters are correct; the unsubscribe link works.

## Rendering in the other channels

Email's rendering is the least predictable of the channels. The other channels trade that fragmentation for tighter templates, which removes most of the cross-client risk and replaces it with format limits.

* **SMS** has no rendering to speak of: plain text, no styling, one link. The design constraint is length, the `GSM-7` and `UCS-2` segment boundary that governs cost and splitting. See [SMS and RCS](/channels/sms-and-rcs.md).
* **RCS** adds rich cards, carousels and suggested replies, but only where both endpoints support it: every RCS message needs an SMS fallback designed in.
* **Push** renders in a fixed OS template you cannot restyle: a title, a short body truncated on the lock screen, an optional image or action buttons the platform may or may not show. Design to the truncation and assume the image is absent. See [push](/channels/push.md).
* **In-app** is the surface you fully control, native components rendered by your own SDK, which reduces the variation to device size and OS version rather than client quirks. The same mobile-first, accessibility and contrast discipline applies. See [in-app](/channels/in-app.md).
* **Wallet passes** render into the platform's pass template, leaving the design work as a choice of which fields hold the message within Apple's and Google's fixed layouts. See [wallet passes](/channels/wallet-passes.md).

## Related

* [Copywriting](/foundations/copywriting.md)
* [Deliverability](/foundations/deliverability.md)
* [Email](/channels/email.md)
* [SMS and RCS](/channels/sms-and-rcs.md)
* [Push](/channels/push.md)
* [Personalisation mechanics](/foundations/personalisation-mechanics.md)
* [Email intelligence research](/references/email-intelligence-research.md)
