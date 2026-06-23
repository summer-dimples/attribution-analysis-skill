# Attribution Analysis Skill · 指标异常归因分析 Skill

A bilingual Claude-style skill for structured metric anomaly attribution and AI PM / strategy / data case interviews.

中英文版指标归因 Skill，适用于 AI 产品经理、策略、数据分析、增长、推荐/模型效果类面试题。

## What it solves / 解决什么问题

Most candidates answer metric cases with: “I would look at the data.” This skill forces a senior structure:

1. Rule out fake anomalies.
2. Decompose numerator / denominator.
3. Walk data / external / user-mix / product-system dimensions.
4. Give an investigation order with decision rules.
5. Separate correlation from causation.
6. End with decision + A/B validation.

很多候选人回答指标题时只会说“我会看数据”。本 Skill 把回答升级成可执行归因链路：排假异常 → 拆指标 → 四象限排查 → 排查顺序与判断规则 → 因果验证 → 决策与 A/B 验证。

## Install / 安装

```bash
npx skills add <your-github-username>/attribution-analysis-skill
```

## Use cases / 适用场景

- DAU / CTR / CVR / retention / adoption rate dropped or spiked.
- A/B conflict: conversion up, satisfaction down.
- Model or recommendation quality decayed.
- Offline metric improved but online metric did not move.
- Latency / P99 spike.
- Business vs experience tradeoff.
- AI PM / strategy / data case interview.

## Files / 文件

- `SKILL.md` — main bilingual skill instruction.
- `references/case-library.zh-en.md` — bilingual case bank and model answer skeleton.

## Part of / 项目归属

Part of the AI Interview Copilot project — open-sourcing the method, not private user data.
