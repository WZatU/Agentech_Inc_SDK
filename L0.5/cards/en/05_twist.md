# `Agentech.twist(parameters)`

<!-- START: Definition -->
## Definition

**L0.5 · Movement** — Apply a bounded left/right body-yaw rate while the Aegis robot dog remains standing, then stop the attitude command.

The function wraps the upstream ZSL-1 `attitudeControl(..., yaw_vel, ...)` axis. It adjusts body attitude and is not a locomotion turn or a base-heading command.
<!-- END: Definition -->

<!-- START: Syntax -->
## Syntax

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
## Constraints

1. `direction` is required and must be `"left"` or `"right"`.
2. `0.02 <= yaw_rate_rad_s <= 0.2`. This is the Agentech public soft range; the upstream attitude-yaw hard range is `0.0–0.5 rad/s` by magnitude.
3. `0 < duration_s <= 2.0` and `0 <= hold_s <= 3.0`.
4. The wrapper converts `direction` to the sign of upstream `yaw_vel`; callers always pass a positive magnitude.
5. Out-of-range values return `rejected(E_RANGE)` and are not clamped.
6. This API does not accept `angle_deg`: ZSL-1 documents attitude velocity, not an absolute body-yaw mechanical limit.
<!-- END: Constraints -->

<!-- START: Defaults -->
## Defaults

| Call | Default behavior |
| --- | --- |
| `Agentech.twist(direction=...)` | Equivalent to `Agentech.twist(direction=..., yaw_rate_rad_s=0.2, duration_s=0.5, hold_s=0, return_to_neutral=True)` |
| `Agentech.twist(direction=..., yaw_rate_rad_s=...)` | `duration_s` defaults to `0.5`; `hold_s` defaults to `0`; `return_to_neutral` defaults to `True` |
| `Agentech.twist(direction=..., duration_s=...)` | `yaw_rate_rad_s` defaults to `0.2`; `hold_s` defaults to `0`; `return_to_neutral` defaults to `True` |
<!-- END: Defaults -->

<!-- START: Parameters -->
## Parameters

| Parameter | Default | Range / Rule | Description |
| --- | --- | --- | --- |
| `direction` | required | `"left"` or `"right"` | Selects the sign of the upstream attitude `yaw_vel` command. |
| `yaw_rate_rad_s` | `0.2` | `0.02–0.2 rad/s` | Positive body-yaw rate magnitude exposed by the Agentech public API. |
| `duration_s` | `0.5` | `0 < duration_s <= 2.0` | Time for which the nonzero attitude-yaw command is applied. |
| `hold_s` | `0` | `0 <= hold_s <= 3.0` | Optional wait after the nonzero rate command stops. |
| `return_to_neutral` | `True` | boolean | Requests the Agentech wrapper to return body yaw to neutral using attitude feedback. |

The authoritative limit source is `profiles/aegis/zsl1.yaml`. ZSL-1 permits attitude `yaw_vel` through `0.5 rad/s` by magnitude. Agentech applies a conservative `0.2 rad/s` public soft maximum. The `3.0 rad/s` locomotion yaw limit belongs to `move(...)`/`turn(...)` and must not be used here.

`return_to_neutral=True` is an Agentech wrapper behavior, not a native parameter of `attitudeControl`. It requires body-attitude feedback; if that capability is unavailable, the call returns `rejected(E_CAPABILITY_UNAVAILABLE)` rather than estimating an absolute angle from time alone.
<!-- END: Parameters -->

<!-- START: Behavior -->
## Behavior

The SDK verifies standing state, converts `direction` to signed attitude `yaw_vel`, applies that command for `duration_s`, then sends zero attitude yaw rate. It waits for `hold_s` and returns to neutral when requested and supported. The call blocks until completion, rejection, preemption, emergency stop, or timeout.
<!-- END: Behavior -->

<!-- START: Return -->
## Return

```python
SkillResult(status, trace_id, error_code, message)
```

| Field | Meaning |
| --- | --- |
| `status` | Final call state: `"succeeded"`, `"rejected"`, `"preempted"`, `"estopped"`, or `"timeout"` |
| `trace_id` | Command ID used to correlate SDK logs and device logs |
| `error_code` | `None` on success; stable error code on failure |
| `message` | Developer-facing detail; do not branch program logic on this string |
<!-- END: Return -->

<!-- START: Example -->
## Example

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
