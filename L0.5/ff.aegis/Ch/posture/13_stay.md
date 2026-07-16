# `Agentech.stay(time=1.0)`

<!-- START: Definition -->
## 定义

**L0.5 · Posture · Aegis** — 四足着地时，保持机器人当前已经到达的姿态。

来源：[EAIC HUB Aegis SDK](https://www.agent-tech.ai/agentech-products/eaic-hub/view-sdk)，同步日期 2026-07-16。
<!-- END: Definition -->

<!-- START: Syntax -->
## 调用方式

```python
Agentech.stay(time=1.0)
```
<!-- END: Syntax -->

<!-- START: Constraints -->
## 约束

1. 输入必须严格符合参数表中的类型和范围；越界值应被拒绝，不得静默改写。
<!-- END: Constraints -->

<!-- START: Defaults -->
## 默认设定

当前官网没有发布参数默认值。
<!-- END: Defaults -->

<!-- START: Parameters -->
## 参数

| 参数 | 类型 / 范围 | 默认值 | 状态 | 含义 |
| --- | --- | --- | --- | --- |
| `time` | `float > 0 (no maximum)` | — | 可用 | 保持当前姿态的时间。 |
<!-- END: Parameters -->

<!-- START: Behavior -->
## 行为

四足着地时，保持机器人当前已经到达的姿态。
<!-- END: Behavior -->

<!-- START: Return -->
## 返回

当前官网没有为该 Skill 发布更具体的返回结构。实现应报告成功或拒绝状态，并且不得改变已发布的输入契约。
<!-- END: Return -->

<!-- START: Example -->
## 示例

```python
Agentech.stay(time=1.0)
```
<!-- END: Example -->
