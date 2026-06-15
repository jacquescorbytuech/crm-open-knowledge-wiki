---
type: Playbook
title: Localisation
description: Sending to a multi-region, multi-language audience: send-time by the recipient's timezone across channels, locale-keyed templates and the translation that fills them, multi-currency and locale-correct formatting of offers, and the encoding and layout traps that come with non-Latin scripts.
tags: [localisation, internationalisation, timezone, multi-language, multi-currency, send-time, i18n]
timestamp: 2026-06-15T00:00:00Z
---

## When defaults become decisions

A programme sending to one country in one language can ignore everything here. The moment the list spans timezones, languages, or currencies, defaults that were invisible become decisions: when a send lands, what language it lands in, and what a price and date mean to the person reading them. These are cross-channel concerns: the per-channel mechanics they touch live in [copywriting](/foundations/copywriting.md), [message design and rendering](/foundations/message-design-and-rendering.md), and the [channel](/channels/) pages, and localisation is the layer that varies those by who the recipient is and where they are.

## Send time by the recipient's timezone

A single send clock is a single timezone's clock. Fire a broadcast at 9am headquarters time and half a global list gets it at 3am. Send-time localisation splits the send so each recipient receives it at the intended local hour, keyed to the timezone on their profile rather than the server's. On the interruptive channels a mistimed send does real harm: an [SMS](/channels/sms-and-rcs.md) or [push](/channels/push.md) that arrives in the middle of the night is worse than ignored, and for SMS the [quiet-hours law](/channels/sms-and-rcs.md) is defined in the recipient's local time, so timezone-correct sending is a compliance control, not just a courtesy. [Email](/channels/email.md) is more forgiving because it waits in the inbox, but local-morning delivery still reads better than overnight.

The data prerequisite is a reliable timezone per contact, inferred from country, postal address, or observed open times, and a sensible fallback when it is missing (the account's primary market, not the server default). Per-recipient send-time optimisation, where the platform learns each contact's responsive hour, is the more sophisticated version of the same idea and carries the same prerequisite.

## Locale-keyed templates and translation

Hard-coded copy is monolingual by construction. The localised pattern is to key content by locale (language plus region, such as `en-GB`, `en-US`, `fr-CA`) and resolve the right variant at send through the [personalisation mechanics](/foundations/personalisation-mechanics.md) the programme already uses for any other profile-driven value. The disciplines that keep it honest:

* **Translate, do not just substitute.** Machine translation gives a draft; a fluent reviewer catches the tone, idiom, and legal phrasing it misses, and the subject line and CTA, the highest-leverage words, are exactly where a stilted translation costs most. Length changes too: German and Finnish run long, which breaks layouts and truncates subject lines tuned for English.
* **Define a fallback locale.** When a contact's locale has no translated variant, fall back to a declared default rather than failing or sending an empty merge field. Make the fallback explicit so a missing translation degrades to a known language, not to a broken message.

## Currency, dates, and formatting

A price, a date, and a number all carry locale. `$1,000` and `1.000 $` are the same amount formatted by opposite conventions, and `03/04` is two different days on the two sides of the Atlantic. Localise the format, and where the offer is transactional, localise the value: show prices in the recipient's currency, set against local price points rather than a raw exchange-rate conversion, so an [offer](/foundations/offers-and-incentives.md) reads as deliberate rather than as a foreign price run through a calculator. The standard locale data for these conventions, currency symbols, date and number formats, and the rest, is maintained centrally in the Unicode CLDR rather than reinvented per programme.

> [!warning] Localise the whole message, not just the body
> A translated body under an English subject line, a local price next to a US date format, or a localised email linking to an English-only landing page all break the spell. The recipient notices the seam, and the seam reads as carelessness. The unit of localisation is the whole journey, message, links, and the page it lands on.

## Scripts and encoding

Non-Latin scripts reach into the channel mechanics. On [SMS](/channels/sms-and-rcs.md) any character outside the GSM-7 set forces the whole message into UCS-2, which cuts the per-segment limit from 160 characters to 70, so a localised SMS can cost several times its English equivalent for the same words. Right-to-left scripts such as Arabic and Hebrew need the layout direction set, not just the text swapped, and [accessibility](/foundations/message-design-and-rendering.md) depends on declaring the message language so a screen reader pronounces it correctly. These are not edge cases in a global programme; they are the difference between a message that renders and one that arrives garbled.

## Related

* [Copywriting](/foundations/copywriting.md)
* [Message design and rendering](/foundations/message-design-and-rendering.md)
* [Personalisation mechanics](/foundations/personalisation-mechanics.md)
* [Offers and incentives](/foundations/offers-and-incentives.md)
* [SMS and RCS](/channels/sms-and-rcs.md)
* [Orchestration and frequency](/foundations/orchestration-and-frequency.md)

## Citations

[1] [Unicode CLDR, locale data for dates, numbers, and currencies](https://cldr.unicode.org/)
[2] [W3C Internationalisation, text direction and language declaration](https://www.w3.org/International/)
