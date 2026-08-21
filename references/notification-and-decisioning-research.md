---
type: Reference
title: Notification and Decisioning Research
description: The published production notification systems and the agentic messaging and uplift literature behind AI decisioning in marketing, with citations to the primary papers.
tags: [research, notifications, reinforcement-learning, bandits, uplift, agentic]
generated:
  by: human:jacquescorbytuech
  at: 2026-06-02T00:00:00Z
stale_after: 2027-08-20
sources:
  - id: li-2010-contextual-bandit
    resource: https://arxiv.org/abs/1003.0146
    title: "Li et al., A Contextual-Bandit Approach to Personalized Recommendation, WWW 2010"
  - id: jeunen-wheeler-2025-agentic-messaging
    resource: https://arxiv.org/abs/2512.17462
    title: "Jeunen and Wheeler, Behavioural Effects of Agentic Messaging, 2025"
  - id: su-2024-long-term-value-of-exploration
    resource: https://arxiv.org/abs/2305.07764
    title: "Su et al., Long-Term Value of Exploration, WSDM 2024"
  - id: agarwal-2016-contextual-decisions
    resource: https://arxiv.org/abs/1606.03966
    title: "Agarwal et al., Making Contextual Decisions with Low Technical Debt, 2016"
---

## Production notification systems

These are peer reviewed papers on production systems, a useful floor on platform capability since the internal systems are at least as good.

| Paper | Contribution |
| --- | --- |
| Pinterest, KDD 2018 | Weekly notification budget per user against long term engagement; value is highest for casual users. |
| Duolingo, KDD 2020 | Sleeping recovering bandit picks the reminder template; lifts daily actives and new user retention. |
| Twitter, 2022 | Model based reinforcement learning to decide whether to send; cutting volume can lift open rate but cut daily actives. |
| LinkedIn, 2022 and 2026 | Offline reinforcement learning for notifications, then BanditLP pairing neural Thompson sampling with a large linear program for email. |
| Zillow, RecSys 2022 | Boosted tree send or do not send, keeping 98% of clicks while shedding surplus sends. |
| Meta, 2023 | Instagram notification slots as an auction across internal teams; fewer sends, higher click through, across 77M users per arm. |
| [Kuaishou PushGen, WSDM 2026](https://arxiv.org/abs/2512.14490) | LLM generates push copy under style controls; a learned reward model then ranks candidates. |
| Pinterest TransAct, KDD 2023 | Transformer over realtime user activity feeding ranking across surfaces. |

## The agentic messaging and uplift literature

* Aampe published randomised controlled trials of agent led messaging on a financial services app, cutting unsubscribes against a rule based baseline by sending more relevantly, with a longitudinal follow up showing autonomous agents sustaining lift for months after a human curated initialisation phase.
* The uplift literature formalises the persuadable, sure thing and do not disturber framing. It also maps the diminishing returns curve beyond the most responsive segment, with work on delayed feedback and the public Hillstrom dataset.
* Google and DeepMind showed that the long-term value of exploration is hard to see in standard A/B tests and needs bespoke experiment designs, which leaves a per-campaign open rate unlikely to surface it.
* The systems literature notes that these algorithms assume clean, correctly logged data, which is a substantial engineering task to produce reliably, the practical side of the data prerequisite.

## On device editor models

The receiving end runs its own published models: Apple Intelligence on a 3 billion parameter on device foundation model with task specific LoRA adapters; Google's Gemini Nano inside AICore. Notification rewriting and prioritisation patents predate the iOS 18 controversy by years.

## Related

* [Decisioning and personalisation](/foundations/decisioning-and-personalisation.md)
* [Uplift and incrementality](/measurement/uplift-and-incrementality.md)
* [Platform interventions](/references/platform-interventions.md)
