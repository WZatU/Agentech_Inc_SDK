# `Agentech.yaw()`

<!-- START: Definition -->
## 定义

**L0.5 · Posture · Aegis** — 使用正速度和带符号目标位置调整机身偏航；负位置向左、正位置向右。

来源：[EAIC HUB Aegis SDK](https://www.agent-tech.ai/agentech-products/eaic-hub/view-sdk)，同步日期 2026-07-16。
<!-- END: Definition -->

<!-- START: Syntax -->
## 调用方式

```python
Agentech.yaw()
Agentech.yaw(speed_rad_s=0.4, position_rad=0.4426)
Agentech.yaw(speed_deg_s=22.92, position_deg=25.36)
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
| 默认调用 | `Agentech.yaw()` | 可用 |
<!-- END: Defaults -->

<!-- START: Parameters -->
## 参数

| 参数 | 类型 / 范围 | 默认值 | 状态 | 含义 |
| --- | --- | --- | --- | --- |
| `speed_rad_s` | `float [0, 0.6]` | — | 可用 | 正的姿态调整速度，单位为弧度每秒。 |
| `speed_deg_s` | `float [0, 34.38]` | — | 可用 | 正的姿态调整速度，单位为度每秒。 |
| `position_rad` | `float [-0.466, 0.4426]` | — | 可用 | 带符号目标姿态位置，单位为弧度。 |
| `position_deg` | `float [-26.73, 25.36]` | — | 可用 | 带符号目标姿态位置，单位为度。 |
<!-- END: Parameters -->

<!-- START: Behavior -->
## 行为

使用正速度和带符号目标位置调整机身偏航；负位置向左、正位置向右。
<!-- END: Behavior -->

<!-- START: Return -->
## 返回

当前官网没有为该 Skill 发布更具体的返回结构。实现应报告成功或拒绝状态，并且不得改变已发布的输入契约。
<!-- END: Return -->

<!-- START: Example -->
## 示例

```python
Agentech.yaw()
Agentech.yaw(speed_rad_s=0.4, position_rad=0.4426)
Agentech.yaw(speed_deg_s=22.92, position_deg=25.36)
```
<!-- END: Example -->
