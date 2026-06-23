# Attribution Case Library · 指标归因 Case 题库

Use these cases for AI PM / strategy / data interview practice. Each case includes an attribution tree and probe points.

这些题可以作为 AI PM / 策略 / 数据面试训练题。每道题都包含归因树和追问点。

---

## C1. Recommendation CTR drops / 推荐 CTR 下降

**Case:** CTR drops from 12.3% to 7.8%, while traffic volume is stable.

**题目：** 推荐 CTR 从 12.3% 降到 7.8%，流量规模基本稳定，如何排查？

Attribution tree / 归因树：

- Fake anomaly: tracking definition, click logging, exposure logging.
- Numerator down: fewer clicks due to lower relevance, UI regression, bad ranking.
- Denominator issue: exposure definition changed, duplicated impressions.
- User mix: new-user traffic ratio increased.
- Product/system: ranking model update, recall change, latency causing skipped ranking.

Probe points / 追问点：

- Do you check numerator or denominator first?
- How do you rule out tracking issues?
- Did the drop happen for new users, old users, or all users?
- How do you prove it was the model update?

---

## C2. P99 latency spike / P99 延迟飙升

**Case:** P99 grows from 800ms to 4200ms, downgrade rate rises from 0.5% to 15%.

**题目：** P99 从 800ms 飙到 4200ms，降级率从 0.5% 到 15%，如何排查？

Attribution tree / 归因树：

- Upstream: longer input, traffic surge, larger payload.
- Current service: release, hot key, resource saturation, cache miss.
- Downstream: LLM, vector DB, ranking service, network.
- Data: latency measurement changed.

Probe points / 追问点：

- Do you mitigate first or investigate first?
- Which node’s latency do you break down first?
- What is the rollback condition?
- How do you prevent recurrence?

---

## C3. A/B conflict / A/B 指标冲突

**Case:** Completion rate improves by 18pp, but satisfaction drops by 0.3. Should we ship?

**题目：** A/B 实验完成率 +18pp，但满意度 -0.3，是否上线？

Attribution tree / 归因树：

- Low-barrier trap: more low-intent users finish but feel lower value.
- Local quality issue: certain templates/segments are bad.
- Expectation mismatch: faster completion but less control.
- Metric hierarchy conflict: completion is not the north-star metric.

Probe points / 追问点：

- Which metric is north-star and which is guardrail?
- Did satisfaction drop for old users or only new users?
- Can we ship to a segment only?
- What A/B extension would you run?

---

## Full-score answer skeleton / 满分回答骨架

```text
First, I would rule out fake anomalies: metric definition, tracking, time window, and data pipeline.
Then I would decompose the metric into numerator and denominator.
Next, I would check four dimensions: data definition, external context, user mix, and product/system changes.
I would set an investigation order with decision rules: if A happens, it supports hypothesis A; if B happens, it supports hypothesis B.
Finally, I would separate correlation from causation using control groups or A/B tests, then decide short-term mitigation and long-term mechanism.
```

中文：

```text
我会先排除假异常：指标定义、埋点、统计窗口、数据链路。
然后拆分子和分母，判断到底是哪一侧在动。
接着从四个维度排查：数据口径、外部环境、用户结构、产品/系统自身。
每一步要有判断规则：如果看到 A，支持假设 A；如果看到 B，支持假设 B。
最后用对照组或 A/B 实验区分相关和因果，再给短期止血与长期机制。
```
