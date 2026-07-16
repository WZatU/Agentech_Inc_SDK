# `Agentech.squat_backward()`

<!-- START: Definition -->
## 定义

**L0.5 · Movement · Aegis** — 在保持锁定低步态蹲姿的情况下向后行走，停止后继续保持蹲姿。

来源：[EAIC HUB Aegis SDK](https://www.agent-tech.ai/agentech-products/eaic-hub/view-sdk)，同步日期 2026-07-16。
<!-- END: Definition -->

<!-- START: Syntax -->
## 调用方式

```python
Agentech.squat_backward(speed_mps=0.5, duration_s=2.0)
```
<!-- END: Syntax -->

<!-- START: Constraints -->
## 约束

1. 输入必须严格符合参数表中的类型和范围；越界值应被拒绝，不得静默改写。
2. 使用该动作前，必须先通过 `Agentech.squat()` 让机器狗进入蹲姿。
3. 涉及距离或完成时间的描述属于开环估计，不能视为保证值。
<!-- END: Constraints -->

<!-- START: Defaults -->
## 默认设定

当前官网没有发布参数默认值。
<!-- END: Defaults -->

<!-- START: Parameters -->
## 参数

| 参数 | 类型 / 范围 | 默认值 | 状态 | 含义 |
| --- | --- | --- | --- | --- |
| `speed_mps` | `float [0.05, 3.00] m/s` | — | 可用 | 速度，单位为米每秒；方向和有效范围以本行类型定义为准。 |
| `duration_s` | `float (0, 10] seconds` | — | 可用 | 动作持续时间。 |
<!-- END: Parameters -->

<!-- START: Behavior -->
## 行为

在保持锁定低步态蹲姿的情况下向后行走，停止后继续保持蹲姿。
<!-- END: Behavior -->

<!-- START: Return -->
## 返回

当前官网没有为该 Skill 发布更具体的返回结构。实现应报告成功或拒绝状态，并且不得改变已发布的输入契约。
<!-- END: Return -->

<!-- START: Example -->
## 示例

```python
Agentech.squat_backward(speed_mps=0.5, duration_s=2.0)
```
<!-- END: Example -->
