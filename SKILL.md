---
name: attribution-analysis
description: >
  EN: Structured root-cause analysis for metric anomalies and analytical case interview questions. Use this skill when a metric changes unexpectedly, an A/B test conflicts, recommendation/model quality decays, latency spikes, conversion or retention drops, or the user needs to answer an AI PM / strategy / data case question.
  中文：用于指标异常归因与分析型 Case 面试。只要出现 DAU、CTR、留存、转化率、采纳率、满意度、NDCG、延迟、P99、A/B 实验结果、模型效果等异常波动，或用户需要回答“某指标下降/上升，如何排查”的面试题，就调用本 Skill。
version: 2.0.0
language: bilingual-zh-en
project: AI Interview Copilot
tags:
  - attribution
  - root-cause-analysis
  - metrics
  - ai-pm
  - case-interview
  - ab-test
  - model-drift
---

# Attribution Analysis Skill · 指标异常归因分析

## 1. Skill purpose / 能力定位

**EN:** This skill turns vague answers like “I would look at the data” into a rigorous root-cause investigation: validate the data, decompose the metric, segment the movement, build hypotheses, test causality, and close with a decision plus validation plan.

**中文：** 本 Skill 的目标是把“我会看数据”这种空泛回答，升级成可执行、可面试、可复盘的归因链路：先排除假异常，再拆指标，再分层定位，再建立假设，再验证因果，最后给出决策与验证方案。

---

## 2. When to use / 何时调用

Use this skill when the user asks about:

- A metric moved unexpectedly: DAU, WAU, CTR, CVR, retention, GMV, revenue, satisfaction, adoption rate, NDCG, latency, P99.
- A/B results conflict: one metric improves while another worsens.
- Recommendation/model quality decays: offline score improves but online effect is flat, model drift, retrieval/ranking degradation.
- Business vs user-experience tradeoff: monetization improves but engagement or satisfaction drops.
- AI PM / strategy / data case interview questions: “某指标下降 30%，你怎么排查？”

当用户出现以下问题时调用：

- 指标突然上涨或下跌：DAU、CTR、转化率、留存、GMV、收入、满意度、采纳率、NDCG、延迟、P99。
- A/B 实验结果矛盾：完成率提升但满意度下降，收入提升但留存下降。
- 推荐/模型效果衰减：离线指标提升但线上不动，模型漂移，召回/排序退化。
- 商业化与体验冲突：收入提升但体验受损。
- AI PM / 策略 / 数据分析 Case 面试题。

---

## 3. Required inputs / 输入信息

Ask for missing context only if necessary. Otherwise proceed with explicit assumptions.

- Metric name / 指标名称
- Direction and magnitude / 变化方向与幅度
- Time window / 发生时间
- Product or business context / 产品或业务背景
- Recent changes / 最近是否发版、改策略、换流量、改埋点
- Available segmentation / 可拆分维度：新老用户、渠道、地区、设备、版本、实验组、模型版本

If the user only provides a short case prompt, infer reasonable assumptions and clearly label them.

如果用户只给了面试题，不要反复追问；可以合理假设，但要明确写出“假设”。

---

## 4. Core workflow / 核心归因流程

### Step 1 — Rule out fake anomaly / 先排除假异常

Check whether the metric movement is caused by measurement rather than reality.

先确认是不是数据本身出了问题，而不是产品真的变差。

Look at:

- Metric definition changed? / 指标定义是否变化
- Tracking or logging changed? / 埋点是否变化
- Time window changed? / 统计窗口是否变化
- Sampling changed? / 抽样口径是否变化
- Data pipeline delay or backfill? / 数据延迟或回补
- Duplicate counting or missing events? / 重复计数或漏计

Decision rule:

- If all segments move exactly at the tracking release time, suspect instrumentation first.
- 如果所有分层都在埋点/数据管道变更时同步异常，优先怀疑口径或埋点。

---

### Step 2 — Decompose the metric / 拆指标

Never analyze a ratio directly. Split it into numerator and denominator.

不要直接分析比率，先拆分子和分母。

Examples:

- CTR = clicks / impressions
- CVR = conversions / visits
- Retention = retained users / activated users
- Adoption rate = accepted AI suggestions / exposed suggestions
- Satisfaction = score distribution, not only average score

Decision rule:

- If the denominator suddenly increases, the metric may drop even when the numerator is stable.
- 如果分母异常扩大，即使分子没变，指标也可能下降。

---

### Step 3 — Walk four MECE dimensions / 四象限排查

Use four universal dimensions:

1. **Data definition / 数据口径** — tracking, metric definition, data pipeline.
2. **External context / 外部环境** — seasonality, competitor, holiday, policy, channel quality.
3. **User mix / 用户结构** — new vs returning, channel, device, region, cohort, persona.
4. **Product/system / 产品与系统自身** — release, UX change, model update, recommendation strategy, latency, availability.

核心原则：平均值会掩盖结构，必须分层。

---

### Step 4 — Set investigation order and decision rules / 给排查顺序和判断规则

A strong answer is not a list of dashboards. It says what to check first, why, and what each result means.

强答案不是罗列“我要看哪些数据”，而是说明：先看什么、为什么先看、看到什么分别意味着什么。

Use this structure:

```text
I would first check <dimension> because <reason>.
If I see <pattern A>, I infer <hypothesis A>.
If I see <pattern B>, I infer <hypothesis B>.
Then I would validate by <method>.
```

中文表达：

```text
我会先看 <维度>，因为 <原因>。
如果看到 <现象 A>，说明可能是 <假设 A>。
如果看到 <现象 B>，说明可能是 <假设 B>。
接下来用 <方法> 验证。
```

---

### Step 5 — Separate correlation from causation / 区分相关与因果

The interviewer will ask: “How do you know it was your change?”

面试官一定会追问：“你怎么证明是你的动作导致的？”

Use:

- A/B test / A/B 实验
- Holdout group / 保留组
- Before-after with control / 带对照的前后对比
- Difference-in-differences / 双重差分
- Cohort analysis / 分 cohort
- Regression or causal inference if appropriate / 必要时用回归或因果推断

Decision rule:

- If treatment and control move together, suspect external trend.
- If only treatment changes after release, suspect product/model change.

---

### Step 6 — Close with decision and validation / 给决策与验证方案

End with action. Do not stop at diagnosis.

最后必须回到决策，不能只停留在归因。

Output:

- Most likely root cause / 最可能根因
- Confidence level / 置信度
- Short-term mitigation / 短期止血
- Long-term mechanism / 长期机制
- A/B or monitoring plan / 验证与监控方案

---

## 5. Specialized trees / 专项归因树

### 5.1 Latency / P99 spike · 延迟异常

Check:

- Upstream input length or traffic surge / 上游输入变长或流量突增
- Current service release, resource, hot key / 本服务发版、资源、热点 key
- Downstream dependencies / 下游依赖：LLM、vector DB、ranking service、network

---

### 5.2 A/B conflict · A/B 指标冲突

Common causes:

- Low-barrier trap: more low-intent users enter / 低门槛带来低质量用户
- Local quality issue / 局部质量问题
- Expectation mismatch / 用户预期偏差
- Metric hierarchy conflict / 指标层级冲突

Decision:

- Define the north-star metric and guardrail metrics before deciding ship/no-ship.
- 先定义北极星指标和护栏指标，再决定是否上线。

---

### 5.3 Model or recommendation drift · 模型/推荐漂移

Check:

- User drift / 用户变化
- Item/content drift / 内容或商品变化
- Distribution shift / 分布偏移
- Feedback loop / 反馈回路
- Position bias / 位置偏差
- Offline-online mismatch / 离线线上不一致

---

### 5.4 Business vs experience conflict · 商业化与体验冲突

Analyze:

- Short-term revenue gain / 短期收入增量
- Long-term LTV loss / 长期 LTV 损失
- User trust damage / 信任损耗
- Alternative placements / 独立区域、分人群、质量门槛

Principle:

- Do not damage the core experience slot unless the ROI is extremely clear and reversible.
- 不轻易牺牲核心体验位，除非 ROI 明确且可逆。

---

## 6. Output contract / 输出格式

When answering, use this structure:

```markdown
## 1. Clarify the metric / 明确指标
- Metric:
- Change:
- Time window:
- Business context:
- Assumptions:

## 2. First check: fake anomaly / 先排假异常
- What to check:
- Decision rule:

## 3. Metric decomposition / 指标拆解
- Numerator:
- Denominator:
- Which side likely moved:

## 4. Four-dimension attribution tree / 四象限归因树
| Dimension | Hypothesis | Evidence to check | Decision rule |
|---|---|---|---|

## 5. Investigation order / 排查顺序
1. First check ... because ...
2. If ... then ...
3. Then validate ...

## 6. Most likely root cause / 最可能根因
- Hypothesis:
- Confidence:
- Why:

## 7. Decision and validation / 决策与验证
- Short-term action:
- Long-term mechanism:
- A/B or monitoring plan:
```

For interview practice, keep it tighter and more oral. For real incident review, be more detailed.

面试场景要更口语、更短；真实复盘可以更细。

---

## 7. Quality bar / 质量标准

A good answer must:

- Start by ruling out fake anomalies.
- Decompose the metric, especially ratios.
- Segment users instead of trusting averages.
- Give an ordered investigation path, not a random checklist.
- State decision rules.
- Distinguish correlation from causation.
- End with action and validation.

一个高分答案必须做到：

- 先排除假异常。
- 拆指标，尤其是比率指标。
- 分层看用户，不能只看平均值。
- 给排查顺序，不是散列表。
- 每一步有判断规则。
- 区分相关与因果。
- 最后给动作与验证。

---

## 8. Anti-patterns / 反模式

Avoid:

- “I would look at the data.” / “我会看数据。”
- Listing dashboards without sequence.
- Ignoring data instrumentation.
- Treating correlation as causation.
- Jumping to product conclusions before checking traffic mix.
- Forgetting business decision and validation.

---

## 9. Example trigger phrases / 触发示例

- “DAU dropped 30%, how would you investigate?”
- “CTR suddenly fell after launch.”
- “A/B test shows conversion up but satisfaction down.”
- “Model offline metrics improved, but online adoption did not move.”
- “推荐效果下降，怎么排查？”
- “采纳率下降，但曝光量上涨，怎么判断？”

---

## 10. Website integration note / 网站集成说明

In AI Interview Copilot, inject this skill when:

- The user is answering a case question.
- The mock interviewer asks about metrics, data, A/B test, model quality, latency, or business tradeoff.
- The review module detects weak attribution or vague data reasoning.

在网站中，以下情况注入本 Skill：

- 用户进入 Case / 指标分析题。
- Mock 面试追问涉及指标、归因、A/B、模型效果、延迟或商业化权衡。
- 复盘模块发现用户回答存在“数据归因不清”的问题。
