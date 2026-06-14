---
type: Reference
title: Notification and Decisioning Research
description: The published production notification systems and the agentic messaging and uplift literature behind AI decisioning in marketing, with citations to the primary papers.
tags: [research, notifications, reinforcement-learning, bandits, uplift, agentic]
timestamp: 2026-06-02T00:00:00Z
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
| Kuaishou PushGen, WSDM 2026 | LLM generates push copy under style controls, a learned reward model ranks candidates. |
| Pinterest TransAct, KDD 2023 | Transformer over realtime user activity feeding ranking across surfaces. |

## The agentic messaging and uplift literature

* Aampe published randomised controlled trials of agent led messaging on a financial services app, cutting unsubscribes against a rule based baseline by sending more relevantly, with a longitudinal follow up showing autonomous agents sustaining lift for months after a human curated initialisation phase.
* The uplift literature formalises the persuadable, sure thing, and do not disturber framing and the diminishing returns curve beyond the most responsive segment, including work on delayed feedback and the public Hillstrom dataset.
* Google and DeepMind showed that the long-term value of exploration is hard to see in standard A/B tests and needs bespoke experiment designs, so a per-campaign open rate is unlikely to surface it.
* The systems literature notes that these algorithms assume clean, correctly logged data, and producing that reliably is a substantial engineering task, the practical side of the data prerequisite.

## On device editor models

The receiving end runs its own published models: Apple Intelligence on a 3 billion parameter on device foundation model with task specific LoRA adapters, and Google's Gemini Nano inside AICore, with notification rewriting and prioritisation patents predating the iOS 18 controversy by years.

## Related

* [Decisioning and personalisation](/foundations/decisioning-and-personalisation.md)
* [Uplift and incrementality](/measurement/uplift-and-incrementality.md)
* [Platform interventions](/references/platform-interventions.md)

## Citations

[1] [Li et al., A Contextual-Bandit Approach to Personalized Recommendation, WWW 2010 (arXiv 1003.0146)](https://arxiv.org/abs/1003.0146)
[2] Jeunen and Wheeler, Behavioural Effects of Agentic Messaging, 2025 (arXiv 2512.17462)
[3] Su et al., Long-Term Value of Exploration, WSDM 2024 (arXiv 2305.07764)
[4] Agarwal et al., Making Contextual Decisions with Low Technical Debt, 2016 (arXiv 1606.03966)
