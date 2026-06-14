---
type: Reference
title: Decisioning and Personalisation
description: The landscape of AI personalisation in CRM and lifecycle platforms, the difference between machine learning that supports a marketer's decision and machine learning that makes it, the common product capabilities, the vendor categories, and the data prerequisite they all share.
tags: [decisioning, personalisation, machine-learning, bandits, send-time, vendors]
timestamp: 2026-06-14T00:00:00Z
---

## Two things the word "AI" hides

Marketing platforms use "AI" for two quite different things, and conflating them overstates what a programme is actually running.

* **Decision support** is machine learning that assists a journey the marketer designed: it scores, ranks, recommends, and optimises at points inside a structure a human built. The marketer still decides what the journey is.
* **Decisioning** is machine learning that makes the decision: a system that chooses, per customer, what to send, when, on which channel, and increasingly whether to send at all, within goals and guardrails the marketer sets. The marketer sets the objective; the system explores and learns.

Most of what ships in a CRM stack is decision support. Decisioning is the smaller, newer, more capable category, and the harder one to adopt because it asks the marketer to hand a learning system the wheel and trust a [holdout](/measurement/holdouts-and-control-groups.md) to vindicate it.

But every capability on this page, decision support and decisioning alike, is downstream of one upstream decision you make before any of it: whether you have built a unified, clean, training-ready first-party data foundation. Build it and the advanced options stay open; skip it and no amount of vendor AI compensates. The vendor and method taxonomy below only starts to matter once that is settled, so read it as the menu you earn access to, not the first choice you make.

## Common decision-support capabilities

These appear across the major customer-engagement platforms and are largely interchangeable on a feature sheet:

* **Send-time optimisation:** predicting each recipient's most engageable time and sending then.
* **Predictive scores:** churn likelihood, conversion propensity, and predicted lifetime value, used to segment. See [segmentation models](/foundations/segmentation-models.md).
* **Content and product recommendations**, and generative subject-line and copy assistance.
* **Frequency and channel optimisation** inside a journey the marketer laid out.

Most of it does something; how much is often hard to verify independently, since the strongest numbers tend to come from vendor case studies.

## What decisioning adds

True decisioning borrows the methods used in large-scale recommendation: **contextual bandits** and reinforcement learning, which choose an action from each customer's context and keep reallocating as feedback arrives, measured against a control rather than an open or click. **Next-best-action / next-best-offer** engines rank the best action per customer in real time. The theoretical edge over test-and-roll-out is real: committing to an A/B winner leaves traffic parked on losing variants, where a system that keeps learning does not. The contrast with a rules-based journey builder is the whole point, predefined paths versus continuous per-customer optimisation.

The mechanism that makes this work is also its hardest cost to swallow. A learning system has to **explore**, deliberately spending some sends on actions it is unsure about so it can find the better ones, rather than only **exploiting** what currently looks best. Exploration is what a fixed A/B test cannot do once it has crowned a winner, and it is what lets a bandit keep improving. But the exploratory sends look like waste on short-horizon metrics, since some of them are by design the worse option, and the payoff arrives later as the system converges. Valuing it correctly takes a longer measurement horizon than most programmes run; the incrementality framing is in [uplift and incrementality](/measurement/uplift-and-incrementality.md).

> [!warning] Do not read exploration as waste
> A learning system spends some sends on actions it is unsure about, which look like the worse option on this week's open rate. Killing it for that dip is the standard way an organisation strangles a decisioning system before it can pay back.

## The vendor landscape

* **Decision-support suites.** Salesforce Einstein, Adobe Sensei / Journey Optimizer, Klaviyo, Iterable, Braze, HubSpot, and the mobile-first names converge on the capability list above.
* **AI-decisioning specialists.** Vendors such as Aampe (per-user agents using bandits and Thompson sampling) and Hightouch (decisioning on top of the data warehouse) make the per-customer decision the product, measuring each decision against a control.
* **Enterprise decisioning.** Adobe Journey Optimizer real-time decisioning, Salesforce on Data Cloud, and Pega Customer Decision Hub (next-best-action for regulated industries) run the offer-ranking and adaptive-journey machinery natively on a unified profile.
* **Acquisition signal.** Braze's acquisition of OfferFit folded a reinforcement-learning decisioning engine into a major engagement platform, a sign the categories are converging.

When evaluating, and assuming the data foundation the opening named is already in place, note that AI feature inventories read almost identically across vendors; differentiate on the audience model, the data layer, and the experiment runner, as in [ESP selection](/foundations/esp-selection.md), not the marketing page.

## Why the claims are hard to verify

The reason these features resist comparison is structural, not just marketing opacity, and it is worth understanding before you weight them in a vendor choice.

* **The models are undisclosed.** Vendors do not expose the model, its features, or its training data, so two "send-time optimisation" features that look identical on a feature sheet can behave nothing alike, and you cannot tell which from the outside.
* **There is no ground truth at the individual level.** You see what the system chose to send and what happened next, never what would have happened had it chosen differently for that same person. Without a counterfactual, a per-customer decision cannot be scored directly; only the aggregate effect against a [holdout](/measurement/holdouts-and-control-groups.md) can.
* **A trial cannot settle it.** These systems need volume and time to learn, so a short proof-of-concept on a slice of your data shows the cold-start, not the converged, behaviour. The strongest numbers in the market are vendor case studies, which select for success and rarely carry a clean control.

The practical consequence is the one [ESP selection](/foundations/esp-selection.md) draws: treat AI feature lists as a tiebreaker between otherwise-equal platforms, never as the deciding factor, and insist that any claimed lift be one you can reproduce against your own holdout.

## What adopting decisioning asks of you

Decisioning is harder to adopt than decision support because it changes who decides, not just what tooling runs. Handing a learning system the per-customer choice means setting an objective and guardrails rather than designing the journey, tolerating the exploration cost above, and trusting a [holdout](/measurement/holdouts-and-control-groups.md) to tell you whether it is working when no single decision can be inspected. The guardrails are the real design surface: the frequency ceilings, suppression rules, and brand or eligibility constraints the system must respect while it optimises inside them. A programme that cannot yet state its objective and guardrails, or cannot run a clean holdout, is not ready to hand over the wheel, whatever the vendor demo shows.

## The data prerequisite

The upstream decision the opening named is worth seeing concretely. Every capability above depends on the same thing: unified, clean, training-ready first-party data. The decisioning specialists need a high-fidelity event feed or a warehouse with your behaviour in it; the enterprise tier needs the unified profile in production. Data quality determines how well any of it works, which is why the [customer data and identity](/foundations/customer-data-and-identity.md) layer comes first. Build the data foundation, and the advanced options stay open; skip it, and no amount of vendor AI compensates.

## Related

* [Customer data and identity](/foundations/customer-data-and-identity.md)
* [Segmentation models](/foundations/segmentation-models.md)
* [ESP selection](/foundations/esp-selection.md)
* [Uplift and incrementality](/measurement/uplift-and-incrementality.md)
* [Holdouts and control groups](/measurement/holdouts-and-control-groups.md)

## Citations

[1] [Hightouch, journeys vs AI decisioning (rules-based journeys vs per-customer AI decisioning)](https://hightouch.com/blog/journeys-vs-ai-decisioning)
[2] [Salesforce, Einstein for Marketing Cloud feature overview](https://help.salesforce.com/s/articleView?id=mktg.mc_ees_einstein_feature_overview.htm&language=en_US&type=5)
[3] [Adobe Journey Optimizer, offer selection in decisions (AI-ranked next-best offer)](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-manage-activities/configure-offer-selection)
[4] [Braze, intelligent timing (per-user send-time optimisation)](https://www.braze.com/docs/user_guide/brazeai/intelligence_suite/intelligent_timing)
[5] [Klaviyo, personalised send time](https://help.klaviyo.com/hc/en-us/articles/45231714007323)
[6] [Pega, next best action (real-time AI decisioning)](https://www.pega.com/technology/next-best-action)
[7] [Li et al., a contextual-bandit approach to personalised recommendation (arXiv 1003.0146)](https://arxiv.org/abs/1003.0146)
[8] [Braze, contextual bandits for real-time personalisation](https://www.braze.com/resources/articles/contextual-bandits)
[9] [Twilio, data quality as the prerequisite for AI personalisation](https://www.twilio.com/en-us/resource-center/data-readiness-ai-driven-personalization)
[10] [Braze completes acquisition of OfferFit](https://www.braze.com/press-releases/braze-completes-acquisition-of-offerfit)
