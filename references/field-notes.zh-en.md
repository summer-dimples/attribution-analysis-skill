# Field Notes / 参考说明

## Design logic / 设计逻辑

This skill is designed as a reusable capability rather than a one-off prompt. It has:

- a clear user job-to-be-done;
- a stable input/output contract;
- a workflow that can be inspected;
- an evaluation rubric;
- website integration points.

这个 skill 的设计目标不是“让模型说得更漂亮”，而是让某个高频任务变成可复用能力：可调用、可评估、可迭代。

## Common failure modes / 常见失败模式

1. Generic coaching with no evidence.
2. Overclaiming user achievements.
3. Asking multiple questions at once.
4. Treating persona as voice imitation rather than evaluation lens.
5. Ignoring business or metric logic.

## Integration pattern / 集成方式

```text
User input
↓
Website module decides which skill to inject
↓
Skill prompt + knowledge context + persona context
↓
LLM output
↓
Review/eval criteria applied
```
