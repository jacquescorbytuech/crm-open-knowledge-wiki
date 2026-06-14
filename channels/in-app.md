---
type: Channel
title: In-app
description: How to use an owned in-product surface, choose the message format by interruption tolerance, set trigger conditions and frequency caps, decide in-app versus push versus email, and measure it cleanly against a holdout.
tags: [channel, in-app, owned, in-product, onboarding, formats, triggers, frequency]
timestamp: 2026-06-14T00:00:00Z
---

## What it is

In app messaging is everything you can show inside your own product: passive cards in a feed the user reaches deliberately, a persistent message centre or inbox, modal and slide up messages triggered on session events, and messaging primitives embedded in the product flows themselves. It is the highest fidelity owned surface most brands have.

What sets it apart is what is missing from the path: in-app is the only channel with no platform editor and no permission gate standing between you and the user. Nothing ranks, bundles, or silences the message, and nothing has to grant it reach first. That absence is not just a delivery convenience; it is exactly what makes in-app the one channel where holdout-based incrementality can be measured cleanly and honestly, because both arms of the test see the same unmediated surface. The measurement section at the foot of the page is where that pays off; the permission and filtering sections below are the two halves of why.

## Permission and reach

No per channel opt in, because the user is already inside a product they chose to open. The hard limit is the opposite of push: in app reaches only the active user. Someone who has not opened the app in a fortnight cannot be reached this way at all, which is precisely the gap push and email cover.

## Filtering and editing

None. Nothing passes through APNs, FCM, or a mailbox provider, so nothing summarises, ranks, bundles, or silences it, and you see every render, dismiss, and interaction. It is the most fully owned and observable surface in the channel mix. See [the channel mix](/channels/index.md).

## Technical specifics

In-app spans a range of intrusiveness, from interruptive to ambient, and the format is the main control you have.

* **Modal / full-screen.** A centred dialog or takeover. Highest attention, highest interruption: it stops the session and demands a response before the user continues. The cost is the same: it is the most disruptive thing you can put on the surface the relationship is built on.
* **Slide-up / banner.** A lighter prompt anchored to an edge of the screen that does not block the flow. Lower attention than a modal, far lower disruption; the user can read it or carry on without dismissing anything.
* **Embedded card / content feed.** Ambient content placed in a surface the user reaches deliberately. Lowest attention, lowest disruption, and persistent: it sits in place rather than firing once.
* **Message centre / inbox.** A persistent in-product inbox the user opens on demand. Ambient and durable, and the only format that can hold a message for a user to find later rather than requiring a live moment to fire.

**How it fires.** In-app messages are typically synced to the device at session start, cached locally, and displayed when the user meets a trigger condition evaluated on-device during a live session: viewing a particular screen, completing or abandoning an action, reaching a session count, or crossing an attribute threshold. Because evaluation happens on-device against the cached set, eligibility and content are only as fresh as the last sync, so a user who qualified mid-session may not see the message until the next session, and a campaign edited server-side does not reach a device until it next syncs. Plan triggers and end dates with that lag in mind.

**Format decision rule.** Match the format to the message's importance and to how much interruption the moment can bear. Reserve the modal for the single highest-value moment, a blocking decision the user must make now or a one-time message they genuinely must not miss; one well-placed takeover earns attention, a stream of them trains dismissal. Use a slide-up or banner for the timely-but-not-blocking majority: a nudge, a contextual tip, a soft offer that should be noticed but must not stop the task. Use an embedded card or inbox for anything ambient or self-serve: evergreen education, a "finish setup" prompt that can wait, content the user can return to. When in doubt, drop one rung down the interruption ladder; the cheaper format usually does the job without spending goodwill.

**Frequency and placement discipline.** Treat interruptive formats as a scarce per-session budget, not a per-message decision. Sensible defaults: cap interruptive messages (modal plus slide-up) to one per session or visit, and prefer at most one modal per user per day; let ambient cards and the inbox carry the rest, since they cost nothing to leave unshown. Do not fire an interruption on top of an active task or mid-checkout. Hold a priority order so two eligible campaigns never stack in one session, and enforce these caps centrally rather than per campaign. See [orchestration and frequency](/foundations/orchestration-and-frequency.md).

**Trigger conditions in practice.** Tie the message to a context window so it lands when it is useful and not before. Show a "finish setup" card when the user reaches the screen the unfinished step belongs to and the step is still incomplete, not on every launch. Surface a feature tip the first time a user opens the area it applies to, capped to once. Fire an upsell slide-up after a user repeats the action the paid tier would improve, not on session one. Each of these is an on-device condition (current screen, completion state, action count) checked against the synced rule set, so keep the conditions to attributes that update reliably on the device and remember the sync-freshness lag above when timing anything that must appear immediately after a server-side event.

## Best-fit jobs

Everything that does not need to reach a dormant user: onboarding and activation, feature education and discovery, cross sell and upsell, contextual prompts at the moment of relevant action, and surveys. Because it interrupts a session the user chose, relevance and timing matter more than reach.

## In-app versus push versus email

The channels do different jobs, so split by where the user is. In-app does the in-session work: it acts on a session the user already started, with room, context, and no per-device permission to spend, so it carries onboarding, education, contextual prompts, and upsell while the user is present. It is the destination, not the way back. Push and email bring an absent user back so in-app can do that work; push when the message is worth breaking into the user's day, email when it is rich or can wait. The default heuristic: if the user is in session, let in-app carry it; if the user is gone and you need them to return, that is a [push](/channels/push.md) or an [email](/channels/email.md), not an in-app message. In-app cannot initiate contact, so anything that depends on reaching a user who is not there is the wrong job for it.

## Constraints

It cannot initiate contact; it can only act on a session the user started. Over using modals and interstitials degrades the product experience, which is a steeper cost here than an ignored email, because it sits on the surface the relationship is actually built on. See [respect the subscriber](/principles/respect-the-subscriber.md).

## Measurement

The cleanest measurement of any channel. The SDK records impression, dismiss, and interaction with no platform mediated gap, so render to conversion is fully attributable end to end. Read the obvious response metrics, CTR on the message and downstream conversion on the action it asked for, but do not stop there: an interruptive format can lift its own click rate while quietly costing the session. Watch the guardrails alongside the response, session abandonment, task completion, and dismiss rate, to catch a modal that converts the few who engage while pushing the rest out of the flow. The honest read of both is against a randomised holdout: hold back a slice of the eligible users, show to the rest, and measure the difference in the action you wanted and in the guardrail metrics, so you see the message's true incremental effect and its true cost. This is where the missing editor and the missing permission gate the opening named pay off: with nothing between you and the device, both arms are clean, which is why holdout based incrementality testing is easiest to run honestly here. See [holdouts and control groups](/measurement/holdouts-and-control-groups.md).

## Lifecycle role

The destination the other channels drive toward. Push and email bring the user back; in app does the work once they arrive. Run them as one portfolio, not as rivals.

## Related

* [Push](/channels/push.md)
* [Email](/channels/email.md)
* [The channel mix](/channels/index.md)
* [Orchestration and frequency](/foundations/orchestration-and-frequency.md)
* [Respect the subscriber](/principles/respect-the-subscriber.md)
* [Holdouts and control groups](/measurement/holdouts-and-control-groups.md)

## Citations

[1] [Braze, in-app messages reach only active users](https://www.braze.com/docs/user_guide/channels/in_app_messages/faq)
[2] [Airship, in-app automation cached and displayed on trigger conditions](https://www.airship.com/docs/guides/features/messaging/in-app-automation/)
</content>
</invoke>
