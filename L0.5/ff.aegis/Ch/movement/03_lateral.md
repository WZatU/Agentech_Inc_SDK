# `Agentech.lateral_left() / Agentech.lateral_right()`

<!-- START: Definition -->
## 定义

**L0.5 · Movement · Aegis** — 使用对应的左移或右移函数进行横向移动。

来源：[EAIC HUB Aegis SDK](https://www.agent-tech.ai/agentech-products/eaic-hub/view-sdk)，同步日期 2026-07-16。
<!-- END: Definition -->

<!-- START: Syntax -->
## 调用方式

```python
Agentech.lateral_left()
Agentech.lateral_right()
Agentech.lateral_left(distance_m=x, speed_mps=x)
Agentech.lateral_right(distance_m=x, speed_mps=x)
Agentech.lateral_left(speed_mps=x, duration_s=x)
Agentech.lateral_right(speed_mps=x, duration_s=x)
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
| 默认调用 | `Agentech.lateral_left() / Agentech.lateral_right()` | 可用 |
| `speed_mps` | `0.5` | 可用 |
| `duration_s` | `2.0` | 可用 |
<!-- END: Defaults -->

<!-- START: Parameters -->
## 参数

| 参数 | 类型 / 范围 | 默认值 | 状态 | 含义 |
| --- | --- | --- | --- | --- |
| `speed_mps` | `float [0.10, 1.0] m/s` | `0.5` | 可用 | 速度，单位为米每秒；方向和有效范围以本行类型定义为准。 |
| `duration_s` | `float (0, 10] seconds` | `2.0` | 可用 | 动作持续时间。 |
| `distance_m` | `float [0, 2] meters` | — | 可用 | 开环请求距离；实际距离可能受到加速、稳定和停止过程影响。 |
<!-- END: Parameters -->

<!-- START: Behavior -->
## 行为

使用对应的左移或右移函数进行横向移动。
<!-- END: Behavior -->

<!-- START: Return -->
## 返回

当前官网没有为该 Skill 发布更具体的返回结构。实现应报告成功或拒绝状态，并且不得改变已发布的输入契约。
<!-- END: Return -->

<!-- START: Example -->
## 示例

```python
# Distance + speed
Agentech.lateral_left(distance_m=1.0, speed_mps=0.5)
Agentech.lateral_right(distance_m=1.0, speed_mps=0.5)

# Speed + time
Agentech.lateral_left(speed_mps=0.5, duration_s=2.0)
Agentech.lateral_right(speed_mps=0.5, duration_s=2.0)
Agentech.lateral_left()
```
<!-- END: Example -->
