---
type: Framework
title: ESP Selection
description: How to evaluate and choose an email service provider using the five factor framework, a weighted scoring worksheet, a trial agenda, and a migration plan.
tags: [esp, vendor-selection, framework, tooling, migration, pricing]
timestamp: 2026-06-14T00:00:00Z
---

## The five factors, in priority order

1. **Features.** Visual editor, automation (drip builder preferred), dynamic segmentation, list growth tools, personalisation, A/B testing, and exportable reporting. Know your must haves versus nice to haves before comparing.
2. **Cost.** Can you afford it at your current list size, how does it scale (per contact or per send limits), and are must have features at your tier or pushed to a more expensive one?
3. **Support.** Live chat, ticketing, documentation, and an active user community. Matters more for less technical teams.
4. **Integrations.** Does it integrate natively with your CRM, ecommerce, and CMS? Native beats Zapier or Make. Only matters if you have specific requirements; do not over engineer this.
5. **Expandability.** The least important factor. Migrating between ESPs is easier than it used to be, so do not pay for features you do not need yet on the promise you will need them later.

## Beginner guidance

Over 220 email platforms exist, and most beginners overthink the choice. Under about 1,000 subscribers the entry level platforms (Mailchimp, Kit, MailerLite, Brevo) are broadly similar and often free. Pick the one that feels most intuitive and start. Stop researching. The rest of this page is for a team that has outgrown that advice and is making a deliberate, comparable choice, usually a paid switch with real data and automations to move.

## Evaluate what you can actually compare

Score vendors on dimensions you can observe and test, and ignore the ones you cannot. The comparable dimensions are concrete and most of them are the features themselves:

* **Channels.** Which channels the platform sends and orchestrates natively (email, SMS, push, in-app, WhatsApp, web, ad-audience sync), versus channels it only reaches through a bolt-on or a third party.
* **Automation.** The triggers, branching, wait/delay logic, and exit conditions the journey builder actually supports, tested against a real flow your programme needs.
* **Segmentation and the data layer.** What customer data it can store and act on, whether segments update dynamically on behaviour and attributes, and how it resolves identity across channels. See [customer data and identity](/foundations/customer-data-and-identity.md).
* **Native integrations.** Whether a first-party connector to your system of record (CRM, ecommerce, CMS) exists, versus a Zapier or Make bridge.
* **Reporting.** What you can measure in-platform and export cleanly, versus what is locked to a dashboard.
* **Pricing model.** Computable to a unit cost (see below).
* **Developer experience.** The API, webhooks, and docs, judged from a real call you make during the trial.

AI and "predictive" features are not comparable. Every vendor lists the same capabilities (send-time optimisation, predictive scoring, subject-line suggestions), the underlying models are undisclosed, and a trial on your small slice of data cannot show whether they work at your scale. Treat them as a tiebreaker between otherwise-equal candidates, never as a deciding factor. The reasons undisclosed models resist comparison are covered in [decisioning and personalisation](/foundations/decisioning-and-personalisation.md).

## Split must have from nice to have

Before scoring anything, write down what the tool has to do, derived from the five factors and your actual programme, not from feature lists. A must have is something the absence of which is a hard no, regardless of price. A nice to have improves the score but never decides it. Keep the must have list short; the longer it grows the more you are letting a vendor's roadmap define your requirements.

| Factor | Typical must have | Typical nice to have |
|---|---|---|
| Features | Automation triggers your flows need, dynamic segmentation, exportable reporting | Advanced send time optimisation, in built predictive scoring |
| Cost | Affordable at current list size with must haves in tier | Generous overage terms, annual discount |
| Support | Documented APIs, reachable support on your plan | 24/7 live chat, named account manager |
| Integrations | Native connector to your system of record (CRM, ecommerce) | Native connectors to secondary tools |
| Expandability | Clean data export, no lock in on owned data | Headroom for channels you may add later |

Decide each row before you see a demo. Any must have a candidate fails removes it from scoring entirely; do not let a strong score elsewhere buy back a missing must have.

## Weighted scoring worksheet

Score the survivors against your own weighting, not vendor marketing. Set a weight per criterion so the priority order is built into the maths, score each candidate 1 to 5 on evidence you gathered (trial, docs, references), then sum weight times score. Weights should sum to 100 and follow your priorities; the column below is a starting point that mirrors the five factor order, adjust it to your situation.

| Criterion | Weight | Candidate A (1-5) | Candidate B (1-5) | Candidate C (1-5) |
|---|---:|---:|---:|---:|
| Features (automation, segmentation, reporting) | 30 | | | |
| Cost at current and projected list size | 25 | | | |
| Deliverability and sending reputation controls | 15 | | | |
| Support quality and responsiveness | 10 | | | |
| Native integrations with your stack | 10 | | | |
| Developer experience (API, webhooks, docs) | 10 | | | |
| **Weighted total** (sum of weight x score) | 100 | | | |

Rules that keep the worksheet honest:

* Score on evidence, not the sales call. A criterion you could not test gets a low or blank score, not a generous guess.
* A failed must have is a disqualification, not a low score. The worksheet only ranks candidates that already clear the must have list.
* Do not retrofit weights to make a preferred vendor win. Set weights before you score.
* A close result means either candidate is fine; revert to the beginner instinct and pick the one your team finds most intuitive.

## Compare pricing models, not headline prices

The headline price is not comparable across vendors because the unit differs. The two common models are **per contact** (you pay for the size of your stored list regardless of sends) and **per send** (you pay for volume sent, often as a monthly send allowance). Neither is cheaper in the abstract; which wins depends entirely on your list size, send frequency, and how fast the list grows.

To compare, model the unit cost yourself rather than reading the page:

1. State your numbers. Current contact count, average sends per contact per month, and a projected contact count for 12 to 18 months out based on your real growth rate.
2. For each candidate, find the tier that holds your **must have features** at your current list size. Features pushed to a higher tier change the real price; record the tier that actually qualifies, not the cheapest one.
3. Compute monthly cost at current size and at projected size from each vendor's own published rates. Do not invent numbers; use the vendor's stated pricing for the qualifying tier.
4. Divide by the relevant unit (cost per 1,000 contacts for per contact, cost per 1,000 sends for per send) so the two models become one comparable figure.
5. Check the overage and tier step behaviour. A per contact plan can jump sharply at a tier boundary; a per send plan can penalise a high frequency programme. Note where each candidate crosses a step at your projected size.

The output is two cost figures per candidate, today and projected, that feed the cost row of the scoring worksheet. A vendor that is cheapest today but steps up sharply at your projected size is often the more expensive choice.

## Run a trial before committing

Do not choose on a demo. A demo shows the happy path on the vendor's data. A trial shows how the tool behaves on yours. Load a representative slice of your own list and run a fixed agenda against each shortlisted candidate, scoring the same tasks for each so the worksheet rests on like for like evidence.

* **Deliverability.** Send a real campaign to a seed set across the major mailbox providers and check inbox placement, not just delivered counts. Confirm the platform supports your own authenticated sending domain (SPF, DKIM, DMARC); see [authentication](/foundations/authentication.md) and [deliverability](/foundations/deliverability.md).
* **An automation trigger.** Build one real flow end to end, fire the trigger, and confirm timing, branching, and exit conditions behave as configured. This is where automation builders differ most from their marketing.
* **Segmentation.** Build a dynamic segment on your own attributes and behaviour, then confirm it updates as data changes rather than being a one off static list. See [customer data and identity](/foundations/customer-data-and-identity.md).
* **An API or webhook integration.** Push a contact in and pull an event out through the API or a webhook, the way your stack will actually use it. Read the docs while you do it; their quality is a proxy for the developer experience.
* **Support response.** Open a real support ticket during the trial and measure the response time and quality on your actual plan tier, not the sales channel.

Record each result as a 1 to 5 score against the worksheet. A capability you could not get working in a trial is unlikely to work better in production.

## Migration plan outline

Migration is less costly than it used to be, but it is not free, and a botched cutover can dent deliverability for weeks. Plan it as a sequence, not a flip of a switch.

1. **Export.** Pull contacts, consent and subscription status, custom fields, and as much engagement history as the old platform allows. Owned data should export cleanly; if it cannot, that is itself a finding about lock in.
2. **Field mapping.** Map every field, segment definition, and consent flag from the old schema to the new one before import. Mismatched consent or status fields are how people get mailed who should not be.
3. **Automation rebuild.** Rebuild flows in the new platform and test each with the trial agenda above. Automations rarely port directly; treat this as a rebuild, not a copy.
4. **Deliverability re-warm.** A new sending domain or IP has no reputation. Ramp volume gradually, starting with your most engaged segments, so the new sending identity earns reputation before you send to the long tail. See [deliverability](/foundations/deliverability.md).
5. **Parallel run.** For a defined window, run critical flows on both platforms or route a slice of traffic to the new one, and reconcile that sends, triggers, and reporting match before you trust it.
6. **Cutover.** Switch remaining traffic over, keep the old platform readable (not sending) for a fallback window, then decommission once the new platform has proven stable across a full cycle.

## Related

* [Decisioning and personalisation](/foundations/decisioning-and-personalisation.md)
* [Customer data and identity](/foundations/customer-data-and-identity.md)
* [Deliverability](/foundations/deliverability.md)
* [Authentication](/foundations/authentication.md)
* [Automation and sequences](/foundations/automation-and-sequences.md)
* [Glossary](/references/glossary.md)

## Citations

This page is practitioner guidance and introduces no external statistics or benchmarks. Where a claim depends on measurement (deliverability, incrementality), see the linked pages and their citations.
