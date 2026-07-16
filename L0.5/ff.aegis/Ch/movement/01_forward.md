# `Agentech.forward()`

<!-- START: Definition -->
## 定义

**L0.5 · Movement · Aegis** — 使用一种正向速度大小模式向前移动，并在结束时受控停止。

来源：[EAIC HUB Aegis SDK](https://www.agent-tech.ai/agentech-products/eaic-hub/view-sdk)，同步日期 2026-07-16。
<!-- END: Definition -->

<!-- START: Syntax -->
## 调用方式

```python
Agentech.forward()
Agentech.forward(speed_mps=0.4, duration_s=1.0)
Agentech.forward(distance_m=1.0, speed_mps=0.4)
Agentech.forward(speed_percent=40, duration_s=1.0)
Agentech.forward(speed_level=100, duration_s=1.0)
Agentech.forward(pace="normal", duration_s=1.0)
Agentech.forward(step_count=6, step_rate_hz=1.5)
```
<!-- END: Syntax -->

<!-- START: Constraints -->
## 约束

1. 输入必须严格符合参数表中的类型和范围；越界值应被拒绝，不得静默改写。
2. `pace` 使用 Agentech 已确认的最大速度比例：`slow=20%`、`normal=40%`、`fast=80%`。
3. `step_count`、`step_rate_hz` 仍处于开发中，不得描述为已完成真机验证。
4. 涉及距离或完成时间的描述属于开环估计，不能视为保证值。
<!-- END: Constraints -->

<!-- START: Defaults -->
## 默认设定

| 来源 | 默认值 | 状态 |
| --- | --- | --- |
| 默认调用 | `Agentech.forward()` | 可用 |
| `speed_mps` | `1.0` | 可用 |
| `duration_s` | `1.0` | 可用 |
| `step_rate_hz` | `1.5` | 开发中 |
<!-- END: Defaults -->

<!-- START: Parameters -->
## 参数

| 参数 | 类型 / 范围 | 默认值 | 状态 | 含义 |
| --- | --- | --- | --- | --- |
| `speed_mps` | `float [0.05, 3.00]` | `1.0` | 可用 | 速度，单位为米每秒；方向和有效范围以本行类型定义为准。 |
| `duration_s` | `float (0, 10]` | `1.0` | 可用 | 动作持续时间。 |
| `distance_m` | `float [0, 2]` | — | 可用 | 开环请求距离；实际距离可能受到加速、稳定和停止过程影响。 |
| `speed_percent` | `float [0, 100]` | — | 可用 | 相对于最大支持速度的百分比请求，允许小数。 |
| `speed_level` | `int [0, 511]` | — | 可用 | 整数速度档位。 |
| `pace` | `enum {slow, normal, fast}` | — | 可用 | 命名速度模式。 |
| `step_count` | `int [1, 20]` | — | 开发中 | 估计步数，不代表精确的足部接触计数。 |
| `step_rate_hz` | `float [0.5, 3.0]` | `1.5` | 开发中 | 估计步频。 |
<!-- END: Parameters -->

<!-- START: Behavior -->
## 行为

使用一种正向速度大小模式向前移动，并在结束时受控停止。
<!-- END: Behavior -->

<!-- START: Return -->
## 返回

当前官网没有为该 Skill 发布更具体的返回结构。实现应报告成功或拒绝状态，并且不得改变已发布的输入契约。
<!-- END: Return -->

<!-- START: Example -->
## 示例

```python
Agentech.forward(speed_mps=1.0, duration_s=1.0)
Agentech.forward()
Agentech.forward(speed_mps=0.4, duration_s=1.0)
Agentech.forward(distance_m=1.0, speed_mps=0.4)
Agentech.forward(speed_percent=40, duration_s=1.0)
Agentech.forward(speed_level=100, duration_s=1.0)
Agentech.forward(pace="normal", duration_s=1.0)
Agentech.forward(step_count=6, step_rate_hz=1.5)
```
<!-- END: Example -->
