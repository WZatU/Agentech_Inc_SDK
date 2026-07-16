# `Agentech.turn()`

<!-- START: Definition -->
## 定义

**L0.5 · Movement · Aegis** — 使用带符号的角度或转速进行转向；负值向左、正值向右，默认值为向右 45 度。

来源：[EAIC HUB Aegis SDK](https://www.agent-tech.ai/agentech-products/eaic-hub/view-sdk)，同步日期 2026-07-16。
<!-- END: Definition -->

<!-- START: Syntax -->
## 调用方式

```python
Agentech.turn()
Agentech.turn(angle_deg=45, turn_rate_deg_s=22.5)
Agentech.turn(angle_rad=0.7854, turn_rate_rad_s=0.3927)
Agentech.turn(rate_percentage=40, duration_s=2.0)
Agentech.turn(turn_level=256, duration_s=2.0)
Agentech.turn(turn_rate_deg_s=45, duration_s=2.0)
Agentech.turn(turn_rate_rad_s=0.7854, duration_s=2.0)
Agentech.turn_right()
Agentech.turn_left()
Agentech.u_turn()
```
<!-- END: Syntax -->

<!-- START: Constraints -->
## 约束

1. 输入必须严格符合参数表中的类型和范围；越界值应被拒绝，不得静默改写。
2. 涉及距离或完成时间的描述属于开环估计，不能视为保证值。
<!-- END: Constraints -->

<!-- START: Defaults -->
## 默认设定

| 来源 | 默认值 | 状态 |
| --- | --- | --- |
| 默认调用 | `Agentech.turn()` | 可用 |
<!-- END: Defaults -->

<!-- START: Parameters -->
## 参数

| 参数 | 类型 / 范围 | 默认值 | 状态 | 含义 |
| --- | --- | --- | --- | --- |
| `angle_rad` | `float (unbounded)` | — | 可用 | 带符号目标角度，单位为弧度。 |
| `turn_rate_rad_s` | `float [-3, 3]` | — | 可用 | 带符号转速，单位为弧度每秒。 |
| `angle_deg` | `float (unbounded)` | — | 可用 | 以正前方为基准的角度，单位为度。 |
| `turn_rate_deg_s` | `float [-120, 120]` | — | 可用 | 带符号转速，单位为度每秒。 |
| `rate_percentage` | `float [-100, 100]` | — | 可用 | 相对于最大转速的带符号百分比。 |
| `turn_level` | `int [-511, 511]` | — | 可用 | 带符号转速档位。 |
| `duration_s` | `float > 0 (no maximum)` | — | 可用 | 动作持续时间。 |
| `turn_right()` | `convenience call` | — | 可用 | 无参数固定向右转 90 度。 |
| `turn_left()` | `convenience call` | — | 可用 | 无参数固定向左转 90 度。 |
| `u_turn()` | `convenience call` | — | 可用 | 无参数固定向左掉头 180 度。 |
<!-- END: Parameters -->

<!-- START: Behavior -->
## 行为

使用带符号的角度或转速进行转向；负值向左、正值向右，默认值为向右 45 度。
<!-- END: Behavior -->

<!-- START: Return -->
## 返回

当前官网没有为该 Skill 发布更具体的返回结构。实现应报告成功或拒绝状态，并且不得改变已发布的输入契约。
<!-- END: Return -->

<!-- START: Example -->
## 示例

```python
Agentech.turn()
Agentech.turn(angle_deg=45, turn_rate_deg_s=22.5)
Agentech.turn(angle_rad=0.7854, turn_rate_rad_s=0.3927)
Agentech.turn(rate_percentage=40, duration_s=2.0)
Agentech.turn(turn_level=256, duration_s=2.0)
Agentech.turn(turn_rate_deg_s=45, duration_s=2.0)
Agentech.turn(turn_rate_rad_s=0.7854, duration_s=2.0)
Agentech.turn_right()
```
<!-- END: Example -->
