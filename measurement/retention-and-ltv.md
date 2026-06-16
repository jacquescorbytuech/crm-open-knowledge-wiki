---
type: Method
title: Retention and LTV
description: How to build a cohort retention curve, compute and segment lifetime value against CAC and payback, run a retention sensitivity check, and prove a retention gain with a holdout.
tags: [retention, ltv, cohort, ltv-cac, churn, unit-economics, payback, sensitivity]
timestamp: 2026-06-14T00:00:00Z
---

## What retention and value measure

Engagement and conversion metrics measure the message. Retention and lifetime value measure the business. A lifecycle programme exists to keep customers and grow their value, so these are the numbers it should be judged on, and the ones most worth moving.

## How to build a cohort retention curve

Group customers by when they were acquired and track what share remain active over time. The construction is mechanical.

1. Define the cohort. The usual key is acquisition month, so the January cohort is everyone who made their first purchase or signed up in January. Acquisition channel or plan tier works as a second key when you want to compare them.
2. Define active in period. Pick the action that means alive for your business (a purchase, a login, a paid renewal) and a fixed window (a calendar month is the common one). A customer is active in month N if they took that action in month N.
3. Build numerator and denominator. The denominator is the cohort size, fixed at acquisition and never changing. The numerator for month N is how many of that original cohort were active in month N. Retention at month N is numerator / denominator.
4. Plot percent active at month 1, 3, 6, 12 for each cohort, with months since acquisition on the x axis and percent retained on the y axis.

```
retention(N) = active_in_month_N / cohort_size_at_acquisition
```

The shape carries the signal. Read it as decline then flatten: an early drop as casual sign ups fall away, settling onto a flatter floor that is your stable core of long term customers. The height of that floor is the number that matters, because it is the fraction worth a programme. A curve that keeps falling steeply without ever flattening has no core, which points to a product or fit problem that no amount of messaging will paper over. Reading retention as a curve rather than a single churn number is what turns it from a report card into a diagnostic. Segment the cohorts by acquisition channel, because customers acquired cheaply through one route often retain quite differently from another.

## Contractual and non-contractual settings

Whether you can see churn at all depends on the setting, and it changes how the curve is built. In a contractual business, a subscription or membership or paid renewal, the customer tells you when they leave. A renewal either happens or it does not, so churn is observed and the curve is read straight off the renewals. In a non-contractual business, retail and ecommerce and most transactional commerce, no one announces their departure. A customer who has not bought in three months may have churned or may simply buy infrequently, and a single gap will not tell you which. Here active in period is a softer judgement, inferred from the pattern of purchase timing rather than read off a contract.

The distinction dictates which tools fit. Contractual retention projects well from a shifted-beta-geometric model fitted to a few periods of renewals [4]. Non-contractual bases are the domain of buy-till-you-die models, the Pareto/NBD and its lighter BG/NBD variant, which infer a hidden dropout time from how often and how recently each customer has bought [2][3]. Reach for the wrong family and the projection will mislead.

## Why retention rises, and why one churn rate misleads

The flattening has a mechanism worth understanding, because it changes the arithmetic. Period by period, the retention rate, meaning the share of last period's survivors who stay this period, usually rises as a cohort ages. It is tempting to read that as customers growing more loyal over time. Mostly they are not. A cohort mixes high-churn and low-churn customers, and the high-churn ones leave first, so what remains is steadily enriched in the loyal. The average retention rate climbs even when no single customer's churn probability has moved. This is a sorting effect in a mixed population, not a change of heart [5].

The consequence is practical. Take one blended churn rate from an early period and apply it flat into the future and you will understate lifetime value, often badly, because you have assumed away the dynamic that makes long-lived customers valuable [5]. The curve has to be read as a curve, rising tail and all, not collapsed to a single number. It is also why segmenting earns its keep: a blended curve mixes populations that churn differently and smears the sorting across them.

## Projecting the curve beyond your data

You usually need value over a longer horizon than your data covers. Two tempting shortcuts both go wrong: extrapolating the curve by eye, and assuming a constant retention rate. The constant rate ignores the rising tail and understates; a freehand fit tends to overstate. The disciplined route is to fit a model with an explicit story for how customers churn and let it project the tail. For contractual retention the shifted-beta-geometric model does this from as few as a handful of periods and runs in a spreadsheet [4]. Whatever you fit, cap the horizon where the projection stops adding meaningful value rather than carrying it to infinity, and re-fit per cohort so a pricing or product change surfaces as a new curve instead of hiding inside an old average.

## Lifetime value

LTV combines what a customer is worth per period with how long they stay, derived from the retention curve rather than guessed. Keeping it honest takes some discipline. Use contribution margin, not revenue, so the number reflects real unit economics. Discount future value, because a relationship that only turns profitable years out is worth less than the undiscounted total suggests, sometimes dramatically less. And prefer cohort based LTV to a single blended figure, which hides the differences that decisions depend on.

The simplest defensible form sums contribution margin per active period, weighted by the share still retained in that period, discounted back to today:

```
LTV = sum over periods t = 1..T of:
        M x retention(t) / (1 + d)^t

  M           = contribution margin per customer per period
  retention(t)= share of the cohort still active in period t (from the curve)
  d           = discount rate per period
  T           = horizon (cap it where retention has flattened or the curve runs out)
```

A clearly hypothetical worked example, illustrative numbers only, not a benchmark. Say contribution margin is 20 per active month, the monthly discount rate is 1%, and a cohort retains 100% in month 0 then 60%, 50%, 45% over the next three months before you cap the horizon:

```
month 0: 20 x 1.00 / 1.01^0 = 20.00
month 1: 20 x 0.60 / 1.01^1 = 11.88
month 2: 20 x 0.50 / 1.01^2 =  9.80
month 3: 20 x 0.45 / 1.01^3 =  8.73
LTV (4 months) = 20.00 + 11.88 + 9.80 + 8.73 = 50.41
```

Undiscounted the same flows total 51.00, so the discount shaves a little here and far more over a multi year horizon.

## LTV to CAC, and payback period

Compare lifetime value to the cost of acquiring the customer. A ratio around three to one is the common health marker. Alongside it sits the payback period, how long until cumulative contribution margin clears CAC, which tells you how long your acquisition spend is underwater.

```
LTV:CAC      = LTV / CAC
CAC payback  = number of periods until cumulative margin >= CAC
```

> [!example] Reading LTV:CAC and payback
> Continuing the hypothetical above, suppose CAC is 30. Then LTV:CAC is 50.41 / 30 = 1.7, below the three to one marker, so this cohort is acquired too expensively or retained too poorly to be comfortable. For payback, accumulate margin period by period until it clears 30: month 0 reaches 20.00, month 1 reaches 31.88, so this cohort pays back in month 1. The ratio judges whether the customer is worth acquiring at all; payback judges how long your cash is tied up getting there.

## How to segment LTV, and why

A blended LTV averages away the decisions. Compute it separately by:

* Acquisition source. Channels differ in both CAC and retention, so a cheap source can still be the worst once you weigh how badly it retains, and an expensive one the best. Only segmented LTV:CAC tells you where the next acquisition pound should go.
* Cohort. Comparing acquisition months shows whether newer customers are retaining better or worse, which is the earliest read on whether a programme or product change is working.
* Tier or plan. Higher tiers usually carry both higher margin and higher retention, so their LTV justifies more acquisition spend and more programme attention.

The point of segmenting is that LTV is an input to a decision, and the decision (where to spend, whom to keep) lives at the segment level, not the average.

## How to run a retention sensitivity check

The most useful thing the model surfaces is sensitivity: which input moves LTV most. Run it as a simple what if. Take the LTV formula, nudge one input at a time by the same proportion, and compare the resulting change in LTV.

* Move retention up by, say, 10% relative across the curve, recompute LTV.
* Separately move contribution margin up by the same 10%, recompute LTV.
* Compare the two lifts.

Small improvements in retention move LTV more than comparable changes in margin or discounting, because retention compounds through every later period of the sum while a margin change scales a fixed set of flows. That is the quantified case for spending on the retention stage of the lifecycle, and it usually beats cutting price. Published estimates of customer equity point the same way: one widely cited study put the firm value impact of a 1% gain in retention at around 5%, against roughly 1% for an equivalent margin gain and a fraction of that for lower acquisition cost [6]. See [lifecycle mapping](/foundations/lifecycle-mapping.md).

## How to move it, and how to prove you did

Retention responds to onboarding that drives early activation, to relevant and well paced lifecycle messaging, and to timely intervention before lapse, not to heavier discounting. Targeting that intervention is the job of a churn propensity model, which scores each customer on how likely they are to lapse next so the retention and winback effort reaches them while there is still something to save. That is a predictive model, distinct from grouping the base: see [churn propensity scoring](/foundations/segmentation-models.md#propensity) for the model and how it differs from the uplift question, and [loyalty and retention programmes](/foundations/loyalty-and-retention-programs.md) for the interventions it feeds. Prove the lift the way the rest of the programme is proven, against a holdout: hold back a randomised slice of the targeted population, run the intervention on the rest, and read the difference in retention between the two. A retention gain claimed without a control group is usually just the customers who were going to stay anyway. See [holdouts and control groups](/measurement/holdouts-and-control-groups.md).

## Related

* [Holdouts and control groups](/measurement/holdouts-and-control-groups.md)
* [Core metrics](/measurement/core-metrics.md)
* [Lifecycle mapping](/foundations/lifecycle-mapping.md)
* [Segmentation models](/foundations/segmentation-models.md)
* [Loyalty and retention programmes](/foundations/loyalty-and-retention-programs.md)
* [Uplift and incrementality](/measurement/uplift-and-incrementality.md)
* [Sample size and power](/measurement/sample-size-and-power.md)

## Citations

[1] [AMA, customer lifetime value guide and calculator](https://www.ama.org/toolkits/ama-lifetime-value-calculator/)

[2] Schmittlein, Morrison and Colombo, [Counting Your Customers: Who Are They and What Will They Do Next?](https://pubsonline.informs.org/doi/10.1287/mnsc.33.1.1), Management Science 33(1), 1987. The Pareto/NBD model, the foundation of customer-base analysis in non-contractual settings.

[3] Fader, Hardie and Lee, [Counting Your Customers the Easy Way: An Alternative to the Pareto/NBD Model](https://www.brucehardie.com/papers/bgnbd_2004-04-20.pdf), Marketing Science 24(2), 2005. The BG/NBD model, a lighter buy-till-you-die alternative that runs in a spreadsheet.

[4] Fader and Hardie, [How to Project Customer Retention](https://www.brucehardie.com/papers/021/sbg_2006-05-30.pdf), Journal of Interactive Marketing 21(1), 2007. The shifted-beta-geometric model for projecting a contractual retention curve from a few periods.

[5] Fader and Hardie, [Customer-Base Valuation in a Contractual Setting: The Perils of Ignoring Heterogeneity](http://brucehardie.com/papers/022/fader_hardie_mksc_10.pdf), Marketing Science 29(1), 2010. Why cohort retention rises through a sorting effect, and why one blended rate understates value.

[6] Gupta, Lehmann and Stuart, [Valuing Customers](https://journals.sagepub.com/doi/10.1509/jmkr.41.1.7.25084), Journal of Marketing Research 41(1), 2004. Estimates the relative impact of retention, margin and acquisition cost on firm value.

[7] McCarthy and Fader, [Customer-Based Corporate Valuation for Publicly Traded Non-Contractual Firms](https://doi.org/10.1177/0022243718802843), Journal of Marketing Research 55(5), 2018. The modern extension of these models to public-company valuation (CBCV); see also McCarthy's [research page](https://danielminhmccarthy.com/research.html).
