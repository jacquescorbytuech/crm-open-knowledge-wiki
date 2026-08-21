---
type: Reference
title: Platform Interventions
description: The dated, citable platform interventions on email and push that double as natural experiments, and the lone motion toward sender side reporting.
tags: [timeline, platform, mpp, bulk-sender, apple-intelligence, gmail]
generated:
  by: human:jacquescorbytuech
  at: 2026-08-20T00:00:00Z
stale_after: 2027-08-20
sources:
  - id: apple-protect-email-privacy-in-mail-mail
    resource: https://support.apple.com/guide/mail/protect-email-privacy-mlhlp1205/mac
    title: "Apple, protect email privacy in Mail (Mail Privacy Protection hides IP and preloads images)"
  - id: litmus-apple-mail-privacy-protection-for-marketers
    resource: https://www.litmus.com/blog/apple-mail-privacy-protection-for-marketers
    title: "Litmus, Apple Mail Privacy Protection for marketers (inflated Apple Mail open rates near 75%)"
  - id: google-email-sender-guidelines-bulk-sender-requirements
    resource: https://support.google.com/a/answer/81126
    title: "Google, email sender guidelines (bulk sender requirements)"
  - id: google-the-2013-tabbed-inbox-promotions-and
    resource: https://blog.google/products/gmail/a-new-inbox-that-puts-you-back-in/
    title: "Google, the 2013 tabbed inbox (Promotions and other tabs)"
  - id: 9to5mac-ios-18-1-ships-apple-intelligence
    resource: https://9to5mac.com/2024/10/28/apple-intelligence-is-here-iphone-ios-8-1/
    title: "9to5Mac, iOS 18.1 ships Apple Intelligence notification summaries"
  - id: techcrunch-apple-pauses-ai-notification-summaries-for
    resource: https://techcrunch.com/2025/01/16/apple-pauses-ai-notification-summaries-for-news-after-generating-false-alerts
    title: "TechCrunch, Apple pauses AI notification summaries for news after false alerts"
  - id: rfc-8058-one-click-unsubscribe
    resource: https://datatracker.ietf.org/doc/html/rfc8058
    title: "RFC 8058, one-click unsubscribe"
  - id: ietf-draft-brotman-aggregate-performance-reporting
    resource: https://datatracker.ietf.org/doc/draft-brotman-aggregate-performance-reporting/
    title: "IETF, draft-brotman-aggregate-performance-reporting"
  - id: microsoft-strengthening-the-email-ecosystem-outlook-s
    resource: https://techcommunity.microsoft.com/blog/microsoftdefenderforoffice365blog/strengthening-email-ecosystem-outlook%E2%80%99s-new-requirements-for-high%E2%80%90volume-senders/4399730
    title: "Microsoft, strengthening the email ecosystem: Outlook's new requirements for high-volume senders (enforcement from 5 May 2025)"
  - id: proofpoint-stricter-google-email-authentication-enforcement-begins
    resource: https://www.proofpoint.com/us/blog/email-and-cloud-threats/clock-ticking-stricter-email-authentication-enforcements-google-start
    title: "Proofpoint, stricter Google email authentication enforcement begins November 2025 (deferral to rejection)"
---

## Each change is a dated natural experiment

Each intervention is discrete and dated, which makes each one a natural experiment a sender can measure a before-and-after against (see [measuring intermediation](/measurement/measuring-intermediation.md)). Most of these changes add a layer of filtering, ranking, or summarisation between the sender and the recipient; most are framed by the platform as a user-protection feature. The practical upshot for a programme is that the inbox and the lock screen are moving targets on which the surviving levers are authentication, list hygiene, and engagement.

## Email and push interventions

| Date | Intervention | Note |
| --- | --- | --- |
| Sep 2021 | Apple Mail Privacy Protection (iOS 15) | Image proxy inflates opens by tens of percentage points on Apple heavy lists, roughly doubling measured open rates; the Mozilla/5.0 user agent becomes the canonical proxy signature. |
| Sep 2021 | iOS 15 Focus and interruption levels | Four level taxonomy; time sensitive is the only addressable level and is not for marketing. |
| Aug 2022 | Android 13 runtime notification permission | Opt in becomes an explicit grant; opt in rates fall sharply. |
| Feb 2024 | Gmail and Yahoo bulk sender requirements | SPF, DKIM, DMARC alignment, RFC 8058 one click unsubscribe, spam rate under 0.3%. Microsoft followed May 2025; Google escalated to rejection Nov 2025. |
| Oct 2024 | iOS 18.1 Apple Intelligence notification summaries | On iPhone 15 Pro forward; the sparkle icon appears. |
| Jan 2025 | iOS 18.3 disables news and entertainment summaries | After the BBC complaint; the cleanest natural experiment for the summarisation effect. |
| Nov 2025 | Pixel notification summaries and Organizer | Pixel 9 and 10; the December follow up auto categorises and silences low priority alerts. |
| Jan 2026 | Gmail AI Overviews and AI Inbox | Powered by Gemini 3; email summarisation default on mobile in most regions. The most aggressive email intermediation since the Promotions tab. |
| early 2026 | Galaxy S26 One UI 8.5 Notification Highlights | On device summarisation on Samsung's stack. |
| Feb 2026 | Microsoft pulls Copilot Priority View from Outlook mobile | Cost and feedback driven; Prioritize My Inbox itself continues across clients. |

## Sender cooperative signals

The signals senders get back are aggregate and deliverability-focused: Gmail Postmaster Tools (aggregate spam rate and reputation by IP and domain) and Microsoft SNDS. The one proposal toward more is draft-brotman-aggregate-performance-reporting, an IETF draft (March 2026) proposing daily aggregate JSON classification and engagement reports keyed by DKIM domain. It is aggregate rather than per-message, email-only, has no summarisation hook, is voluntary for the provider, and sits at an early IETF state.

## The earlier intermediation layer

The summarisation panic is a thin layer on a much older story: Gmail tabs since 2013, Outlook Focused Inbox since 2016, statistical spam filtering since the early 2000s, Android notification channels since 2017, and Focus modes since 2021. A user who silenced your channel in 2019 has been a non engager for years that nobody measured.

## Related

* [Authentication](/foundations/authentication.md)
* [Deliverability](/foundations/deliverability.md)
* [Email intelligence research](/references/email-intelligence-research.md)
* [Measuring intermediation](/measurement/measuring-intermediation.md)
