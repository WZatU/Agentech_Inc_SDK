# `Agentech.twist(parameters)`

<!-- START: Definition -->
## 定义

**L0.5 · Movement** — 让站立状态下的 Aegis 机器狗以有限的机身 yaw 角速度向左或向右扭动，然后停止姿态速度指令。

该函数封装上游 ZSL-1 `attitudeControl(..., yaw_vel, ...)` 轴，用于调整机身姿态；它不是 locomotion turn，也不改变底盘路线朝向。
<!-- END: Definition -->

<!-- START: Syntax -->
## 调用方式

```python
Agentech.twist(direction: str)
Agentech.twist(direction: str, yaw_rate_rad_s: float, duration_s: float)
Agentech.twist(
    direction: str,
    yaw_rate_rad_s: float,
    duration_s: float,
    hold_s: float,
    return_to_neutral: bool,
)
```
<!-- END: Syntax -->

<!-- START: Constraints -->
## 约束

1. `direction` 必填，只能是 `"left"` 或 `"right"`。
2. `0.02 <= yaw_rate_rad_s <= 0.2`。这是 Agentech 对外 soft range；上游 attitude yaw 的硬范围按绝对值为 `0.0–0.5 rad/s`。
3. `0 < duration_s <= 2.0`，`0 <= hold_s <= 3.0`。
4. wrapper 会把 `direction` 转换成上游 `yaw_vel` 的正负号；调用者始终传正的角速度绝对值。
5. 超出范围的参数返回 `rejected(E_RANGE)`，不会自动夹到合法范围。
6. 该 API 不接受 `angle_deg`：ZSL-1 公开的是姿态角速度接口，没有公开绝对机身 yaw 机械极限。
<!-- END: Constraints -->

<!-- START: Defaults -->
## 默认设定

| 调用 | 默认反应 |
| --- | --- |
| `Agentech.twist(direction=...)` | 等价于 `Agentech.twist(direction=..., yaw_rate_rad_s=0.2, duration_s=0.5, hold_s=0, return_to_neutral=True)` |
| `Agentech.twist(direction=..., yaw_rate_rad_s=...)` | `duration_s` 默认 `0.5`，`hold_s` 默认 `0`，`return_to_neutral` 默认 `True` |
| `Agentech.twist(direction=..., duration_s=...)` | `yaw_rate_rad_s` 默认 `0.2`，`hold_s` 默认 `0`，`return_to_neutral` 默认 `True` |
<!-- END: Defaults -->

<!-- START: Parameters -->
## 参数

| 参数 | 默认值 | 范围 / 规则 | 说明 |
| --- | --- | --- | --- |
| `direction` | 必填 | `"left"` 或 `"right"` | 决定上游 attitude `yaw_vel` 指令的正负号。 |
| `yaw_rate_rad_s` | `0.2` | `0.02–0.2 rad/s` | Agentech 公共 API 暴露的机身 yaw 角速度绝对值。 |
| `duration_s` | `0.5` | `0 < duration_s <= 2.0` | 非零 attitude yaw 指令的持续时间。 |
| `hold_s` | `0` | `0 <= hold_s <= 3.0` | 非零角速度停止后的可选等待时间。 |
| `return_to_neutral` | `True` | boolean | 要求 Agentech wrapper 使用姿态反馈让机身 yaw 回到中立位。 |

参数限制的唯一来源是 `profiles/aegis/zsl1.yaml`。ZSL-1 允许 attitude `yaw_vel` 的绝对值最大为 `0.5 rad/s`；Agentech 使用更保守的 `0.2 rad/s` 对外 soft maximum。`move(...)` / `turn(...)` 的 `3.0 rad/s` locomotion yaw 上限不能用于这里。

`return_to_neutral=True` 是 Agentech wrapper 行为，不是 `attitudeControl` 的原生参数。它需要机身姿态反馈；能力不可用时返回 `rejected(E_CAPABILITY_UNAVAILABLE)`，不能只靠时间积分猜测绝对角度。
<!-- END: Parameters -->

<!-- START: Behavior -->
## 行为

SDK 会先确认站立状态，把 `direction` 转换成带符号的 attitude `yaw_vel`，持续执行 `duration_s`，然后发送零姿态 yaw 速度。随后按需等待 `hold_s`，并在能力支持时回到中立位。调用会阻塞到完成、拒绝、抢占、急停或超时。
<!-- END: Behavior -->

<!-- START: Return -->
## 返回

```python
SkillResult(status, trace_id, error_code, message)
```

| 字段 | 含义 |
| --- | --- |
| `status` | 本次调用的最终状态：`"succeeded"`、`"rejected"`、`"preempted"`、`"estopped"` 或 `"timeout"` |
| `trace_id` | 用来关联 SDK 日志和设备日志的命令 ID |
| `error_code` | 成功时为 `None`；失败时返回稳定错误码 |
| `message` | 给开发者看的错误或状态说明，不建议用于程序分支判断 |
<!-- END: Return -->

<!-- START: Example -->
## 示例

```python
result = Agentech.twist(direction="left")
result = Agentech.twist(
    direction="right",
    yaw_rate_rad_s=0.15,
    duration_s=0.5,
)
result = Agentech.twist(
    direction="left",
    yaw_rate_rad_s=0.2,
    duration_s=0.5,
    hold_s=0.5,
    return_to_neutral=True,
)
```
<!-- END: Example -->
