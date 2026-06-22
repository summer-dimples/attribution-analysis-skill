---
name: attribution-analysis
description: >
  Structured root-cause analysis for metric anomalies and analytical "case" questions.
  Use this whenever a metric moved unexpectedly — DAU/CTR/retention/conversion/采纳率
  dropped or spiked, an A/B test gives conflicting results, recommendation or model
  quality decayed (NDCG/采纳率下降), latency/P99 spiked, or generation/answer quality
  fell. Also use when the user is preparing for or answering data/strategy/AI-PM
  interview case questions like "X 指标下降了 30%，你怎么排查？". Make sure to reach for
  this skill even when the user just describes a confusing metric change in passing and
  doesn't explicitly say "归因" or "root cause" — structured attribution is exactly what
  turns a vague "我会看数据" into a rigorous, hireable answer.
---

# 指标异常归因分析 (Attribution Analysis)

A reusable framework for answering any "this metric moved, why?" question — in real
incident review **and** in interviews. The goal is to never stop at "I'd look at the
data." A strong analysis **decomposes the metric, fixes an investigation order, ties each
step to a decision rule, separates correlation from causation, and ends with an action.**

## How to apply this skill

1. **First, rule out the "fake anomaly."** Before blaming the product, check the data
   itself: did the statistic's definition / 埋点 / time window / sampling change? Many
   "drops" are pipeline or counting artifacts. This is the cheapest, most common cause.
2. **Decompose the metric (first principles).** Any ratio splits into numerator and
   denominator — ask which one moved.
   - e.g. CTR = clicks / impressions. Did clicks fall, or did impressions abnormally rise
     (trigger logic loosened, double-counting)?
3. **Walk the four universal dimensions (MECE).** For the moved component, check:
   - **数据口径**: definition / 埋点 / window changed? (rule out first)
   - **外部**: competitor release, holiday seasonality, channel-quality shift, traffic mix.
   - **用户结构**: new vs returning mix, channel quality, persona ratios — averages hide
     structure, so **always segment**.
   - **产品/系统自身**: a release today? model/feature update? resource bottleneck?
     experience regression?
4. **State an investigation order and a decision rule per step.** Don't list "things to
   look at" — say *what you'd look at first, why, and what conclusion each result implies*.
   "If exposure PV jumped → trigger logic loosened. If only new-user CTR is low → a
   pull-in campaign brought low-quality traffic."
5. **Separate correlation from causation.** "How do you prove it was *your* change and not
   the overall trend?" — control for confounders, use holdout/AB, compare to baseline.
6. **Close with a decision + validation plan.** Ship or not? How would you A/B-test the
   hypothesis? Split short-term mitigation ("止血") from long-term mechanism.

## Specialized decomposition trees (use the one that fits)

- **Latency / P99 spike**: upstream (input longer / traffic surge) → this service
  (release / resource / hot key) → downstream deps (each node's latency).
- **A/B conflict (metric A ↑, metric B ↓)**: low-barrier trap (new users flood in and
  drag B down) / localized quality issue / expectation gap. *Disambiguate by checking
  whether the metric changed for existing users only.*
- **Effect decay (drift)**: User Drift (audience changed) / Item Drift (content/SKU
  changed) / Distribution Drift (distribution shift + position bias + feedback loop).
- **Offline good but online flat**: eval-set bias (distribution ≠ online / look-ahead
  bias / too small) / position bias / latency-induced degradation / metric-definition
  mismatch.
- **Business vs experience conflict**: compute ROI — short-term revenue gain vs long-term
  LTV loss; prefer "don't sacrifice the core slot" (separate zone / audience targeting /
  quality gate) over directly degrading the core experience.

## Output shape

Lead with the decomposition (numerator/denominator + which dimension), then the ordered
investigation with decision rules, then the most-likely root cause, then the decision +
validation. Keep it tight and structured — this is a reasoning artifact, not an essay.
A worked bank of 10 real cases is in `references/case-library.md`; read it when the user
wants concrete examples, practice questions, or a model answer to compare against.

## Why this matters

Interviewers (and real on-call situations) reward *judgment under structure*, not a list
of dashboards. The candidate who says "first I'd rule out 埋点, then split numerator vs
denominator, then segment new/old users, and here's what each result would tell me" reads
as senior. The one who says "I'd dig into the data" does not.
