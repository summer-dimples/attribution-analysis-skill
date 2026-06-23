# Attribution Analysis Skill / 指标归因分析 Skill

## What it does / 作用

Diagnoses metric changes with sanity checks, numerator/denominator decomposition, segmentation, causal hypotheses, and experiment plans.

处理 DAU/留存/CTR/转化/模型效果等指标波动：先排假异常，再拆子分母、分层定位、提出因果假设和验证方案。

## When to use / 何时使用

- PM case interviews involving metric drops
- AI product evaluation questions
- A/B test interpretation
- Model quality or conversion decline diagnosis

## Inputs / 输入

- Metric name and time window
- Observed change
- Business context
- User segments and funnel if available
- Experiment/release/traffic logs if available

## Core workflow / 核心流程

1. Check whether the anomaly is real
2. Decompose numerator/denominator and funnel
3. Segment by user, channel, device, geography, cohort, model version
4. Generate ranked hypotheses
5. Separate correlation from causality
6. Propose data checks, experiments, and decisions

## Output / 输出

- Metric tree
- Hypothesis table
- Priority order
- Data needed
- Decision plan
- Interview-ready answer

## Website integration / 网站集成

Powers product case drills, review critique, and metric-related mock interview questions.

## Repository structure / 仓库结构

```text
attribution-analysis-skill/
├─ README.md
├─ SKILL.md
├─ examples/
│  ├─ input.zh.md
│  ├─ output.zh.md
│  ├─ input.en.md
│  └─ output.en.md
├─ eval/
│  ├─ rubric.zh-en.md
│  └─ test-cases.zh-en.md
└─ references/
   └─ field-notes.zh-en.md
```

## Why this skill matters / 为什么这个 skill 有价值

This skill turns a repeated interview-preparation task into a reusable capability. It is useful both as a standalone GitHub skill and as a building block inside AI Interview Copilot.

它的价值不在于“写得像 prompt”，而在于把一个高频任务抽象成可复用能力：有输入、有流程、有输出、有评估标准，也能嵌入网站 workflow。
