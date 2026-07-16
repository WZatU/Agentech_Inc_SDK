# `Agentech.diagonal()`

<!-- START: Definition -->
## 定义

**L0.5 · Movement · Aegis** — 使用 X/Y 坐标，或使用角度、速度和时长进行对角线移动；正 X 向右、正 Y 向前、正角度向右。

来源：[EAIC HUB Aegis SDK](https://www.agent-tech.ai/agentech-products/eaic-hub/view-sdk)，同步日期 2026-07-16。
<!-- END: Definition -->

<!-- START: Syntax -->
## 调用方式

```python
Agentech.diagonal()
Agentech.diagonal(x_m=0.5, y_m=1.0, duration_s=2.0)
Agentech.diagonal(angle_deg=45, speed_mps=0.5, duration_s=2.0)
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
| 默认调用 | `Agentech.diagonal()` | 可用 |
| `angle_deg` | `45` | 可用 |
| `speed_mps` | `0.5` | 可用 |
| `duration_s` | `2.0` | 可用 |
<!-- END: Defaults -->

<!-- START: Parameters -->
## 参数

| 参数 | 类型 / 范围 | 默认值 | 状态 | 含义 |
| --- | --- | --- | --- | --- |
| `x_m` | `float (nonzero)` | — | 可用 | 左右方向的开环位移；正值向右、负值向左。 |
| `y_m` | `float (nonzero)` | — | 可用 | 前后方向的开环位移；正值向前、负值向后。 |
| `angle_deg` | `float [-180, 180]` | `45` | 可用 | 以正前方为基准的角度，单位为度。 |
| `speed_mps` | `float [0.05, 3.0] m/s` | `0.5` | 可用 | 速度，单位为米每秒；方向和有效范围以本行类型定义为准。 |
| `duration_s` | `float (0, 10]` | `2.0` | 可用 | 动作持续时间。 |
<!-- END: Parameters -->

<!-- START: Behavior -->
## 行为

使用 X/Y 坐标，或使用角度、速度和时长进行对角线移动；正 X 向右、正 Y 向前、正角度向右。
<!-- END: Behavior -->

<!-- START: Return -->
## 返回

当前官网没有为该 Skill 发布更具体的返回结构。实现应报告成功或拒绝状态，并且不得改变已发布的输入契约。
<!-- END: Return -->

<!-- START: Example -->
## 示例

```python
# Coordinate + duration
Agentech.diagonal(x_m=0.5, y_m=1.0, duration_s=2.0)

# Angle + speed + duration
Agentech.diagonal(angle_deg=45, speed_mps=0.5, duration_s=2.0)
Agentech.diagonal()
```
<!-- END: Example -->
