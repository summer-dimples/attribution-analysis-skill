# attribution-analysis-skill

A reusable **Claude Skill** for structured root-cause analysis of metric anomalies — and
for acing data / strategy / AI-PM **case interview** questions like *"DAU dropped 30%, how
would you investigate?"*

It pushes the model past "I'd look at the data" into a rigorous method: rule out fake
anomalies → decompose (numerator/denominator) → walk four MECE dimensions → state an
investigation order with decision rules → separate correlation from causation → close with
a decision + A/B validation plan. Includes specialized trees for latency spikes, A/B
conflicts, model drift, offline-vs-online gaps, and business-vs-experience tradeoffs.

## Install

```bash
npx skills add <your-github-username>/attribution-analysis-skill
```

## What's inside

- `SKILL.md` — the framework and when it triggers.
- `references/case-library.md` — 10 worked cases (problem → attribution tree → probe
  points) plus a "full-marks answer" skeleton.

## When it triggers

Metric moved unexpectedly (CTR/DAU/retention/conversion/采纳率 up or down), A/B results
conflict, model/recommendation quality decayed, latency spiked, or you're prepping for an
analytical case interview.

## Note

Methodology is general; the worked cases are adapted from a real recommendation-product
PRD retro. Free to use and adapt.

---
Part of the *AI Interview Copilot* project — open-sourcing the **method**, not the data.
