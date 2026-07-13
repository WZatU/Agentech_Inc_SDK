# `Agentech.turn(parameters)`

<!-- START: Definition -->
## Definition

**L0.5 · Movement** — Rotate the Aegis robot dog left or right in place for a specified duration or approximate angle, then stop.

Use this function to change the direction the robot is facing without intentionally moving forward, backward, or sideways.

The turn uses open-loop control. Angle-based movement is estimated from the commanded yaw rate and execution time; it does not guarantee an exact final heading.
<!-- END: Definition -->

<!-- START: Syntax -->
## Syntax

```python
Agentech.turn(direction: str)
Agentech.turn(direction: str, duration_s: float)
Agentech.turn(direction: str, duration_s: float, yaw_rate_rad_s: float)
Agentech.turn(direction: str, angle_deg: float)
Agentech.turn(direction: str, angle_deg: float, yaw_rate_rad_s: float)
```
<!-- END: Syntax -->

<!-- START: Constraints -->
## Constraints

1. `direction` is required and must be `"left"` or `"right"`.
2. Use either `duration_s` or `angle_deg`, but not both.
3. `yaw_rate_rad_s` is an auxiliary parameter and may be used with either `duration_s` or `angle_deg`.
4. `yaw_rate_rad_s` represents a positive magnitude. Direction is controlled separately by `direction`.
5. Negative yaw-rate values return `rejected(E_RANGE)` and are not automatically converted into a direction.
6. For an angle-based call, the SDK calculates duration using `radians(angle_deg) / yaw_rate_rad_s`.
7. The calculated duration of an angle-based call must not exceed `10.0` seconds.
8. Values outside the supported ranges return `rejected(E_RANGE)` and are not automatically adjusted.
9. Mixing incompatible parameter profiles returns `rejected(E_PROFILE_MIXED)`.
10. The robot must be standing and ready before the turn begins.
11. Every accepted turn ends with a controlled stop. An emergency stop always takes precedence.
<!-- END: Constraints -->

<!-- START: Defaults -->
## Defaults

| Parameter | Default | Meaning |
| --- | ---: | --- |
| `duration_s` | `1.0 s` | Used when neither `duration_s` nor `angle_deg` is provided |
| `yaw_rate_rad_s` | `1.0 rad/s` | Default commanded turn rate |
| `angle_deg` | None | An angle is estimated only when explicitly requested |

| Call | Default behavior |
| --- | --- |
| `Agentech.turn(direction=...)` | Turns in place at `1.0 rad/s` for `1.0 s`, then stops |
| `Agentech.turn(direction=..., duration_s=...)` | `yaw_rate_rad_s` defaults to `1.0` |
| `Agentech.turn(direction=..., angle_deg=...)` | `yaw_rate_rad_s` defaults to `1.0` |

The default call has a theoretical open-loop rotation of approximately:

```text
1.0 rad/s × 1.0 s × 180 / π ≈ 57.3°
```

This value is an estimate, not a guaranteed final heading.
<!-- END: Defaults -->

<!-- START: Parameters -->
## Parameters

### Parameter Profiles

| Profile | Main parameter | Additional parameter | Supported range |
| --- | --- | --- | --- |
| Direction | `direction` | Required | `"left"` or `"right"` |
| Time and rate | `duration_s` | `yaw_rate_rad_s=1.0` | `0 < duration_s <= 10.0`; `0.02 <= yaw_rate_rad_s <= 3.0` |
| Angle and rate | `angle_deg` | `yaw_rate_rad_s=1.0` | `0 < angle_deg <= 360.0`; calculated duration must not exceed `10.0 s` |

### `direction`

Sets the turn direction relative to the robot’s current heading.

| Value | Turn direction |
| --- | --- |
| `"left"` | Rotate counterclockwise around the robot’s vertical axis |
| `"right"` | Rotate clockwise around the robot’s vertical axis |

Changing the robot’s current heading also changes the world-space direction represented by `"left"` and `"right"`.

### `yaw_rate_rad_s`

Sets the commanded yaw-rate magnitude in radians per second.

```text
0.02 <= yaw_rate_rad_s <= 3.0
```

The range follows the Agibot D1 ZSL-1 `move()` command range for nonzero yaw-rate input.

The developer always provides a positive magnitude. The SDK applies the sign from `direction`:

```text
left  -> positive yaw rate
right -> negative yaw rate
```

Useful conversions include:

| `yaw_rate_rad_s` | Theoretical angular speed |
| ---: | ---: |
| `0.02 rad/s` | Approximately `1.15 deg/s` |
| `0.3 rad/s` | Approximately `17.19 deg/s` |
| `0.5 rad/s` | Approximately `28.65 deg/s` |
| `1.0 rad/s` | Approximately `57.30 deg/s` |
| `2.0 rad/s` | Approximately `114.59 deg/s` |
| `3.0 rad/s` | Approximately `171.89 deg/s` |

These conversions describe the command value. The robot’s achieved physical yaw rate may differ because of gait control, ground contact, internal control behavior, and other physical conditions.

### `duration_s`

Sets how long the yaw-rate command remains active.

```text
0 < duration_s <= 10.0
```

If omitted from a duration-based call, it defaults to `1.0` second.

The theoretical heading change is:

```text
estimated_angle_deg =
    duration_s × yaw_rate_rad_s × 180 / π
```

For example:

```text
duration_s = 2.0
yaw_rate_rad_s = 0.3

estimated_angle_deg =
    2.0 × 0.3 × 180 / π
    ≈ 34.38°
```

A duration-based call may produce more than one complete rotation. The SDK limits execution time but does not convert this profile into a target heading.

### `angle_deg`

Requests an approximate in-place rotation angle in degrees.

```text
0 < angle_deg <= 360.0
```

The SDK estimates the required execution time using:

```text
duration_s =
    radians(angle_deg) / yaw_rate_rad_s
```

Equivalent form:

```text
duration_s =
    angle_deg × π / 180 / yaw_rate_rad_s
```

For example:

```text
angle_deg = 90
yaw_rate_rad_s = 1.0

duration_s =
    90 × π / 180 / 1.0
    ≈ 1.571 s
```

The calculated duration must not exceed `10.0` seconds. Otherwise, the call returns `rejected(E_RANGE)`.

The SDK does not verify the final heading using IMU or odometry feedback. Actual rotation may differ from `angle_deg`, especially for short commands or high yaw rates.

### Reserved Parameters

The following parameters are reserved but are not currently supported:

| Parameter | Status |
| --- | --- |
| `angle_percent` | `TBD` — not provided by the Agibot D1 movement interface |
| `turn_level` | `TBD` — no Agibot turn-level parameter or verified level-to-angle mapping is available |
| `quarter_turns` | `TBD` — no native quarter-turn command or verified open-loop calibration is available |

Passing a reserved parameter returns `rejected(E_TBD_PARAMETER)` before a robot or simulator command is emitted.

These parameters may be added later after the turn-rate response is measured and an Agentech mapping is defined.
<!-- END: Parameters -->

<!-- START: Behavior -->
## Behavior

The SDK first makes sure the robot is standing and ready to move. It then resolves the requested direction, yaw-rate magnitude, and duration.

The underlying movement command uses no forward or sideways velocity:

```text
left  -> move(0, 0, +yaw_rate_rad_s)
right -> move(0, 0, -yaw_rate_rad_s)
```

At the end of the requested or calculated duration, the SDK sends:

```text
move(0, 0, 0)
```

Because both `vx` and `vy` are zero, this action requests an in-place turn. Moving turns that combine forward speed and yaw rate belong to a separate arc-movement action.

The call waits until the action succeeds, is rejected, is interrupted, reaches an emergency stop, or times out.

Robot and simulator backends must use the same signed command value and resolved duration. Simulators must not treat `angle_deg` as closed-loop heading completion when the robot backend uses open-loop timing.
<!-- END: Behavior -->

<!-- START: Return -->
## Return

```python
SkillResult(status, trace_id, error_code, message)
```

| Field | Meaning |
| --- | --- |
| `status` | Final state: `"succeeded"`, `"rejected"`, `"preempted"`, `"estopped"`, or `"timeout"` |
| `trace_id` | Command ID used to find related SDK, simulator, and device logs |
| `error_code` | `None` on success; otherwise a stable error code describing the failure |
| `message` | Developer-readable details; do not use this string for application logic |
<!-- END: Return -->

<!-- START: Example -->
## Example

```python
# Turn left at the default command rate of 1.0 rad/s for 1 second.
result = Agentech.turn(direction="left")

# Turn right at 0.3 rad/s for 2 seconds.
# The theoretical heading change is approximately 34.38 degrees.
result = Agentech.turn(
    direction="right",
    duration_s=2.0,
    yaw_rate_rad_s=0.3,
)

# Turn left at the default rate for 0.5 seconds.
result = Agentech.turn(
    direction="left",
    duration_s=0.5,
)

# Request an approximate 90-degree right turn.
# At 1.0 rad/s, the calculated duration is approximately 1.571 seconds.
result = Agentech.turn(
    direction="right",
    angle_deg=90,
    yaw_rate_rad_s=1.0,
)

# Request an approximate 45-degree left turn using the default yaw rate.
result = Agentech.turn(
    direction="left",
    angle_deg=45,
)
```
<!-- END: Example -->
