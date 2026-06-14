---
type: Reference
title: Platform Interventions
description: The dated, citable platform interventions on email and push that double as natural experiments, and the lone motion toward sender side reporting.
tags: [timeline, platform, mpp, bulk-sender, apple-intelligence, gmail]
timestamp: 2026-06-14T00:00:00Z
---

# Why this matters

Each intervention is discrete and dated, which makes each one a natural experiment a sender can measure a before-and-after against (see [measuring intermediation](/measurement/measuring-intermediation.md)). Most of these changes add a layer of filtering, ranking, or summarisation between the sender and the recipient, and most are framed by the platform as a user-protection feature. The practical upshot for a programme is that the inbox and the lock screen are moving targets, and the levers that survive are authentication, list hygiene, and engagement.

# Email and push interventions

| Date | Intervention | Note |
| --- | --- | --- |
| Sep 2021 | Apple Mail Privacy Protection (iOS 15) | Image proxy inflates opens 30 to 50% on Apple heavy lists; the Mozilla/5.0 user agent becomes the canonical proxy signature. |
| Sep 2021 | iOS 15 Focus and interruption levels | Four level taxonomy; time sensitive is the only addressable level and is not for marketing. |
| Aug 2022 | Android 13 runtime notification permission | Opt in becomes an explicit grant; opt in rates fall sharply. |
| Feb 2024 | Gmail and Yahoo bulk sender requirements | SPF, DKIM, DMARC alignment, RFC 8058 one click unsubscribe, spam rate under 0.3%. Microsoft followed May 2025; Google escalated to rejection Nov 2025. |
| Oct 2024 | iOS 18.1 Apple Intelligence notification summaries | On iPhone 15 Pro forward; the sparkle icon appears. |
| Jan 2025 | iOS 18.3 disables news and entertainment summaries | After the BBC complaint; the cleanest natural experiment for the summarisation effect. |
| Nov 2025 | Pixel notification summaries and Organizer | Pixel 9 and 10; the December follow up auto categorises and silences low priority alerts. |
| Jan 2026 | Gmail AI Overviews and AI Inbox | Powered by Gemini 3; email summarisation default on mobile in most regions. The most aggressive email intermediation since the Promotions tab. |
| early 2026 | Galaxy S26 One UI 8.5 Notification Highlights | On device summarisation on Samsung's stack. |
| Feb 2026 | Microsoft pulls Copilot Priority View from Outlook mobile | Cost and feedback driven; Prioritize My Inbox itself continues across clients. |

# Sender cooperative signals

The signals senders get back are aggregate and deliverability-focused: Gmail Postmaster Tools (aggregate spam rate and reputation by IP and domain) and Microsoft SNDS. The one proposal toward more is draft-brotman-aggregate-performance-reporting, an IETF draft (March 2026) proposing daily aggregate JSON classification and engagement reports keyed by DKIM domain. It is aggregate rather than per-message, email-only, has no summarisation hook, is voluntary for the provider, and sits at an early IETF state.

# The earlier intermediation layer

The summarisation panic is a thin layer on a much older story: Gmail tabs since 2013, Outlook Focused Inbox since 2016, machine learning spam filtering since the late 1990s, Android notification channels since 2017, and Focus modes since 2021. A user who silenced your channel in 2019 has been a non engager for years that nobody measured.

# Related

* [Authentication](/foundations/authentication.md)
* [Deliverability](/foundations/deliverability.md)
* [Email intelligence research](/references/email-intelligence-research.md)
* [Measuring intermediation](/measurement/measuring-intermediation.md)

# Citations

[1] [Apple, protect email privacy in Mail (Mail Privacy Protection hides IP and preloads images)](https://support.apple.com/guide/mail/protect-email-privacy-mlhlp1205/mac)
[2] [Google, email sender guidelines (bulk sender requirements)](https://support.google.com/a/answer/81126)
[3] [Google, the 2013 tabbed inbox (Promotions and other tabs)](https://blog.google/products/gmail/a-new-inbox-that-puts-you-back-in/)
[4] [9to5Mac, iOS 18.1 ships Apple Intelligence notification summaries](https://9to5mac.com/2024/10/28/apple-intelligence-is-here-iphone-ios-8-1/)
[5] [TechCrunch, Apple pauses AI notification summaries for news after false alerts](https://techcrunch.com/2025/01/16/apple-pauses-ai-notification-summaries-for-news-after-generating-false-alerts)
[6] [RFC 8058, one-click unsubscribe](https://datatracker.ietf.org/doc/html/rfc8058)
[7] [IETF, draft-brotman-aggregate-performance-reporting](https://datatracker.ietf.org/doc/draft-brotman-aggregate-performance-reporting/)
