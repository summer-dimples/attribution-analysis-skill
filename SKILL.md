---
name: attribution-analysis-skill
version: 2.1.0
language: bilingual zh-CN/en
summary: Metric anomaly attribution and AI PM case-interview reasoning.
description: >
  A bilingual skill for diagnosing metric changes such as DAU, retention, CTR, conversion,
  model quality, latency, and revenue. It is designed for AI PM case interviews and product
  decision-making: validate the signal, decompose the metric, segment the impact, generate
  causal hypotheses, and propose experiments or decisions.
---

# Attribution Analysis Skill / 指标归因分析 Skill

## 1. Purpose / 目的

**EN:** Diagnose why a product or model metric changed, separate real signal from noise, and turn a messy metric issue into a clear investigation plan and decision.

**中文：** 用于分析 DAU、留存、CTR、转化率、模型效果、延迟、收入等指标异常。它帮助候选人在 AI PM/产品 Case 面试中从“看到指标变化”走到“验证信号—拆分指标—定位原因—验证因果—提出行动”。

## 2. When to use / 适用场景

Use this skill when the user asks about:

- Metric drops or spikes: DAU down 20%, CTR down, retention down, conversion changed.
- AI product metrics: model quality, hallucination rate, answer satisfaction, task completion, latency.
- Case interviews: “A metric dropped, how do you analyze it?”
- Product review: deciding whether a change caused the movement.

当出现以下问题时调用：

- “DAU 下降 20%，怎么分析？”
- “推荐 CTR 降了，是算法问题还是流量问题？”
- “大模型回答满意度下降，如何排查？”
- “A/B 实验提升了点击但降低了留存，怎么判断？”

## 3. Required inputs / 必要输入

- Metric name / 指标名
- Direction and magnitude / 变化方向与幅度
- Time window / 时间窗口
- Product context / 产品背景
- Known changes / 已知改动：版本、流量、模型、运营、渠道、埋点
- User or segment context / 用户分层、渠道、端、地区等

If missing, ask for the minimum missing information before doing deep attribution.

## 4. Core workflow / 核心流程

### Step 0 — Clarify the metric / 澄清指标
Define numerator, denominator, unit, time granularity, and business meaning.

明确：分子、分母、统计口径、时间粒度、业务含义。

### Step 1 — Validate the signal / 先排假异常
Check data pipeline, logging changes, sample size, seasonality, release calendar, holiday effects, and dashboard changes.

先排除埋点、口径、样本量、节假日、版本灰度、看板变更造成的假异常。

### Step 2 — Decompose the metric / 拆分指标
Break the metric into formula components and adjacent funnel metrics.

将指标拆成分子分母和漏斗上下游。例如：

- CTR = Clicks / Impressions
- Conversion = Orders / Visitors
- Retention = Returning users / Activated users
- Model satisfaction = Helpful answers / Total answers

### Step 3 — Segment the impact / 四象限排查
Segment by user, device, channel, geography, scenario, model version, traffic source, cohort, and product surface.

按用户、端、渠道、地区、场景、模型版本、流量来源、新老用户、功能入口分层定位影响面。

### Step 4 — Generate hypotheses / 生成假设
Use a structured hypothesis tree:

1. Traffic mix changed / 流量结构变化
2. Product experience changed / 产品体验变化
3. Model/system quality changed / 模型或系统质量变化
4. External environment changed / 外部环境变化
5. Measurement changed / 统计口径变化

### Step 5 — Distinguish correlation from causality / 区分相关与因果
Ask what evidence would prove or disprove each hypothesis. Prefer experiment, matched cohort, pre-post comparison, diff-in-diff, and badcase review.

不要把“同时发生”当成“导致”。需要用实验、同群对照、前后对比、差分、badcase 审核来验证。

### Step 6 — Recommend actions / 输出决策
Prioritize actions by impact, confidence, cost, risk, and reversibility.

根据影响、置信度、成本、风险、可逆性排序行动。

## 5. Output contract / 输出格式

```markdown
## 1. Metric definition / 指标定义
- Metric:
- Numerator:
- Denominator:
- Time window:
- Business meaning:

## 2. First judgment / 初步判断
- Is this likely a real anomaly or possible measurement noise?
- Confidence:

## 3. Decomposition / 指标拆解
- Formula:
- Upstream metrics:
- Downstream metrics:

## 4. Segmentation plan / 分层排查
| Segment | What to check | Why it matters | Expected evidence |
|---|---|---|---|

## 5. Hypothesis tree / 假设树
1. Hypothesis:
   - Evidence supporting:
   - Evidence against:
   - How to verify:

## 6. Causality check / 因果验证
- Experiment or quasi-experiment:
- Badcase review:
- Risk of false attribution:

## 7. Decision / 行动建议
- Immediate action:
- Follow-up experiment:
- Monitoring metrics:
- Rollback condition:
```

## 6. Quality bar / 质量标准

A good answer must:

- Start from metric definition, not random guessing.
- Separate fake anomaly from real anomaly.
- Decompose numerator/denominator and funnel.
- Propose evidence needed for each hypothesis.
- Avoid causal claims without validation.
- End with concrete next actions.

好答案必须：先定义指标，再排假异常，再拆分，再分层，再验证因果，最后给行动。

## 7. Anti-patterns / 反模式

- “可能是用户不喜欢” without segmentation.
- Jumping to one cause without checking logging or sample size.
- Confusing correlation with causation.
- Only listing reasons without verification plan.
- No business decision at the end.

## 8. Website integration / 网站集成

- Inject into **Module A** when JD or interview questions contain metrics, growth, conversion, retention, recommendation, model evaluation, or business diagnosis.
- Inject into **Mock Interview** when the interviewer asks a metric/case question.
- Inject into **Review** to judge whether the candidate’s answer has metric definition, decomposition, causality, and action.

在你的网站中，它应该服务于：岗位诊断、指标 Case 面试、Mock 追问、复盘报告。
