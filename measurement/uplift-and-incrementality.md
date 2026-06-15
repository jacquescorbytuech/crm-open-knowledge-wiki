---
type: Concept
title: Uplift and Incrementality
description: The difference between predicting who will act and measuring whether sending changed what they did, and the methods that actually measure and model that difference.
tags: [uplift, incrementality, holdout, decisioning, measurement, causal, qini]
timestamp: 2026-06-14T00:00:00Z
---

## The real question

The real question in lifecycle marketing is not did the user open it. It is did sending it change what they did, against an identical user left alone. That is the uplift question, and it separates three groups: the persuadables, whom a message wins over; the sure things, who convert anyway and whom you waste a send on; and the do not disturbers, who would have converted if you had stayed quiet and whom messaging actively loses.

For most senders the honest answer to that question is a number, not a model. A randomised holdout tells you whether a send, sequence, or programme moved behaviour in aggregate, and that single number is as far as the volume on most lists will carry you. Modelling which individuals are persuadable is a real thing you can do, but it is the high volume tier: a brand with a list in the tens of thousands cannot detect the sub percent moves it would need to train on. So lead with the holdout, treat the per user model as the layer you earn your way up to, and read the methods below knowing which of the two you are actually in a position to run.

## Why prediction is not enough

A static model asks which users are most likely to open or buy and aims at them, which keeps messaging the people who were going to act regardless while quietly annoying the ones a message pushes the wrong way. An adaptive model asks how sending this, now, changes what this user does, which is why the same model has to be willing to send nothing at all. The skill is knowing whom not to message, which is harder to learn than whom to message. Uplift studies show the cumulative incremental effect peaks well before you have reached the whole list, and past that peak more targeting reduces it. Send to the whole list and you are into zero or negative territory.

## The two things people call uplift

The word covers two different jobs, and conflating them is the usual source of confusion.

* **Measuring incrementality** answers how much did this send, sequence, or whole programme change behaviour in aggregate. It is a single number with a confidence interval, read from a randomised holdout. Most teams need only this.
* **Modelling uplift** answers which individual users are persuadable, so you can target them and suppress the rest. It needs a model trained on experimental data and is worth the effort only at volume. This is the decisioning layer.

Do the first before you attempt the second. A team that cannot reliably measure programme incrementality has no clean signal to train an uplift model on.

## How to measure incrementality

The mechanism is a randomised holdout, covered in full in [holdouts and control groups](/measurement/holdouts-and-control-groups.md). The arithmetic, once the experiment has run:

```
Incremental rate (absolute) = conversion_treatment - conversion_control
Relative uplift             = (conversion_treatment - conversion_control) / conversion_control
Incremental conversions     = incremental_rate (absolute) x audience_size
```

Treat the result as a distribution, not a point. The absolute lift is significant only if the difference between the two proportions clears the noise, which is the same two proportion test used to plan the test in the first place. See [sample size and power](/measurement/sample-size-and-power.md) for the calculation and [volume thresholds](/measurement/volume-thresholds.md) for the sends per cell a given effect needs.

> [!example] A worked read
> A winback flow goes to 100,000 eligible users, 5,000 held back. Treated convert at 4.0%, control at 3.4%. Absolute lift is 0.6pp, relative uplift 17.6%, and the flow drove roughly 600 incremental conversions across the treated 95,000, not the ~3,800 a last touch report would have claimed. The gap between those two numbers is the entire point of the exercise.

For brand or offline activity that cannot be split at the person level, randomise geographies instead and read the difference against control regions. See the geo experiment section in [holdouts and control groups](/measurement/holdouts-and-control-groups.md).

## How to model uplift at the individual level

This is the high volume tier; if you cannot yet run a clean programme holdout, it is not where you are. The hard part is that you never observe both outcomes for one person: a user is either sent to or held out, never both, so the per user treatment effect is never directly in the data. Every method below is a way around that missing counterfactual, and all of them require training data from a randomised experiment, not from the observational history of who happened to get messaged.

* **Two model (T-learner).** Fit one outcome model on the treated and a separate one on the control, then score uplift as the difference in their predictions. Simple and uses any classifier, but it models the two responses well and the difference between them badly, so small true effects get swamped by the errors of two large models.
* **Single model with a treatment flag (S-learner).** One model with treatment as a feature; uplift is the prediction with the flag on minus the flag off. Stable but tends to underplay the treatment effect, since a flat learner can ignore a weak treatment feature entirely.
* **Class transformation.** Relabel the target so a single standard classifier learns uplift directly, by exploiting the symmetry of a 50/50 randomised split. Clean when the split is balanced, and a good first real attempt.
* **Direct uplift methods.** Uplift trees and forests split on the difference in response between treated and control rather than on response itself, optimising the effect you care about directly. Meta learners such as the X-learner improve on the two model approach when the treatment and control groups are very different sizes.

In practice you do not implement these from scratch. Open libraries such as scikit-uplift, Uber's CausalML, and Microsoft's EconML provide the learners, the evaluation, and the data handling.

## How to evaluate an uplift model

Standard classifier metrics do not apply, because there is no per user ground truth label to score against. You evaluate on a held back randomised set using ranking based curves instead.

* **Uplift curve / Qini curve.** Sort users by predicted uplift, then plot cumulative incremental conversions as you target from the top down. A useful model bends above the diagonal and peaks before the full audience; the peak is your optimal targeting depth.
* **Qini coefficient.** The area between that curve and the random diagonal, a single number for comparing models, analogous to how AUC summarises a classifier.
* **Uplift by decile.** Bin the scored holdout into deciles of predicted uplift and check that measured incremental rate falls monotonically across them. A model whose top decile does not actually show the highest real lift is not ready, however good its curve looks.

The curve also tells you where to stop sending, which is the decision the model exists to make: target down to the peak and suppress everyone past it.

## Why most brands cannot do it

A platform can read a 0.42% lift across tens of millions of users an arm. A brand with a list in the tens of thousands cannot detect a sub percent move in anything, so it can only ever measure gross proxies like opens, never the small shifts in retention or revenue that decide the business. Measure outcomes, not opens is good advice that most brands cannot act on, which is the real reason the long tail clings to opens. Modelling uplift, which differences two already noisy models, needs more volume still, so for most senders the honest stopping point is a programme level holdout and a handful of per flow controls. See [volume thresholds](/measurement/volume-thresholds.md).

## The exploration layer above it

A related idea in adaptive systems is exploration: deliberately sending something the model is unsure about to learn from the result, which can read as flat or negative on short-term metrics and pay back over months. Even platforms with deep instrumentation built bespoke experiments to value exploration, because standard A/B tests tended to show it as neutral or harmful. It is hard to see at the volumes a typical programme runs. See [decisioning and personalisation](/foundations/decisioning-and-personalisation.md).

## Related

* [Holdouts and control groups](/measurement/holdouts-and-control-groups.md)
* [Sample size and power](/measurement/sample-size-and-power.md)
* [Volume thresholds](/measurement/volume-thresholds.md)
* [Frequentist and Bayesian testing](/measurement/frequentist-vs-bayesian.md)
* [Decisioning and personalisation](/foundations/decisioning-and-personalisation.md)
* [Retention and LTV](/measurement/retention-and-ltv.md)

## Citations

[1] [Gutierrez & Gérardy, Causal Inference and Uplift Modeling: A review of the literature (PMLR)](http://proceedings.mlr.press/v67/gutierrez17a/gutierrez17a.pdf)
[2] [Radcliffe & Surry, Real-World Uplift Modelling with Significance-Based Uplift Trees (Qini)](https://www.stochasticsolutions.com/pdf/sig-based-up-trees.pdf)
[3] [Künzel et al., Metalearners for estimating heterogeneous treatment effects (X-learner, PNAS)](https://www.pnas.org/doi/10.1073/pnas.1804597116)
[4] [scikit-uplift documentation (models and evaluation)](https://www.uplift-modeling.com/en/latest/)
[5] [Uber CausalML (uplift and meta-learners)](https://github.com/uber/causalml)
[6] [Su et al., Long-Term Value of Exploration, WSDM 2024 (arXiv 2305.07764)](https://arxiv.org/abs/2305.07764)
