# `Agentech.lateral(parameters)`

<!-- START: Definition -->
## Definition

**L0.5 · Movement** — Move the Aegis robot dog sideways to the left or right at a specified speed, for a specified duration or approximate distance, then stop.

Use this function for simple sideways movement. Direction is relative to where the robot is currently facing. Speed can be provided directly or expressed as a percentage, level, or named pace such as `"slow"`, `"normal"`, or `"fast"`.

Distance-based movement is estimated from speed and time. It does not guarantee that the robot travels the exact requested distance.
<!-- END: Definition -->

<!-- START: Syntax -->
## Syntax

```python
Agentech.lateral(direction: str)
Agentech.lateral(direction: str, speed_mps: float, duration_s: float)
Agentech.lateral(direction: str, speed_percent: int, duration_s: float)
Agentech.lateral(direction: str, speed_level: int, duration_s: float)
Agentech.lateral(direction: str, pace: str, duration_s: float)
Agentech.lateral(direction: str, distance_m: float, speed_mps: float)
```
<!-- END: Syntax -->

<!-- START: Constraints -->
## Constraints

1. `direction` is required and must be `"left"` or `"right"`.
2. Use at most one speed format in each call: `speed_mps`, `speed_percent`, `speed_level`, or `pace`.
3. `distance_m` may be paired only with `speed_mps`.
4. A distance-based call must not include `duration_s`; the SDK calculates the duration from distance and speed.
5. Mixing incompatible parameter profiles returns `rejected(E_PROFILE_MIXED)`.
6. `speed_mps` represents a positive speed magnitude. Direction is controlled separately by `direction`.
7. Values outside the supported ranges return `rejected(E_RANGE)` and are not automatically adjusted.
8. For distance-based movement, `distance_m / speed_mps` must not exceed `10.0` seconds.
9. The robot must be standing and ready before sideways movement begins.
10. Every accepted movement ends with a controlled stop. An emergency stop always takes precedence.
<!-- END: Constraints -->

<!-- START: Defaults -->
## Defaults

| Parameter | Default | Meaning |
| --- | ---: | --- |
| `speed_mps` | `0.4 m/s` | 40% of the maximum speed; equivalent to `pace="normal"` and `speed_level=8` |
| `duration_s` | `1.0 s` | Used when a speed-based call omits duration |
| Distance-profile `speed_mps` | `0.4 m/s` | Used when `distance_m` is provided without an explicit speed |

| Call | Default behavior |
| --- | --- |
| `Agentech.lateral(direction=...)` | Moves in the requested direction at `0.4 m/s` for `1.0 s` |
| `Agentech.lateral(direction=..., speed_mps=...)` | `duration_s` defaults to `1.0` |
| `Agentech.lateral(direction=..., speed_percent=...)` | `duration_s` defaults to `1.0` |
| `Agentech.lateral(direction=..., speed_level=...)` | `duration_s` defaults to `1.0` |
| `Agentech.lateral(direction=..., pace=...)` | `duration_s` defaults to `1.0` |
| `Agentech.lateral(direction=..., distance_m=...)` | `speed_mps` defaults to `0.4` |
<!-- END: Defaults -->

<!-- START: Parameters -->
## Parameters

### Parameter Profiles

| Profile | Main parameter | Additional parameter | Supported range |
| --- | --- | --- | --- |
| Direction | `direction` | Required | `"left"` or `"right"` |
| Speed and time | `speed_mps` | `duration_s=1.0` | `0.05 <= speed_mps <= 1.0`; `0 < duration_s <= 10.0` |
| Percentage and time | `speed_percent` | `duration_s=1.0` | Integer from `5` to `100` |
| Level and time | `speed_level` | `duration_s=1.0` | Integer from `0` to `20` |
| Pace and time | `pace` | `duration_s=1.0` | `"slow"`, `"normal"`, or `"fast"` |
| Distance and speed | `distance_m` | `speed_mps=0.4` | `0 < distance_m <= 2.0`; calculated duration must not exceed `10.0 s` |

### `direction`

Sets the sideways movement direction relative to where the robot is currently facing.

| Value | Movement |
| --- | --- |
| `"left"` | Move sideways to the robot’s left |
| `"right"` | Move sideways to the robot’s right |

Changing the robot’s heading also changes the world-space direction represented by `"left"` and `"right"`.

### `speed_mps`

Sets the sideways speed directly in meters per second.

Provide this parameter as a positive magnitude. The `direction` parameter determines whether the robot moves left or right.

```text
0.05 <= speed_mps <= 1.0
```

The SDK does not accept negative values or automatically convert them into a direction.

If no speed parameter is provided, `speed_mps` defaults to `0.4 m/s`.

### `speed_percent`

Sets the speed as a percentage of the maximum supported sideways speed of `1.0 m/s`.

```text
speed_mps = speed_percent / 100 × 1.0
```

| `speed_percent` | Sideways speed |
| ---: | ---: |
| `5` | `0.05 m/s` |
| `20` | `0.2 m/s` |
| `40` | `0.4 m/s` |
| `80` | `0.8 m/s` |
| `100` | `1.0 m/s` |

Percentages below `5` are rejected because they resolve below the minimum supported nonzero speed.

### `speed_level`

Sets the speed using an integer level from `0` to `20`.

Each nonzero level represents an increase of `0.05 m/s`:

```text
speed_mps = speed_level × 0.05
```

| `speed_level` | Percentage of maximum | Sideways speed | Meaning |
| ---: | ---: | ---: | --- |
| `0` | `0%` | `0.0 m/s` | Stop |
| `1` | `5%` | `0.05 m/s` | Minimum nonzero speed |
| `4` | `20%` | `0.2 m/s` | Same speed as `"slow"` |
| `8` | `40%` | `0.4 m/s` | Same speed as `"normal"` |
| `16` | `80%` | `0.8 m/s` | Same speed as `"fast"` |
| `20` | `100%` | `1.0 m/s` | Maximum speed |

If `speed_level=0`, the SDK sends a stop command immediately and completes without waiting for `duration_s`.

`speed_level` is an Agentech convenience parameter. The resolved numeric speed, rather than the level itself, is sent to the robot.

### `pace`

Sets the speed using a simple named pace.

| `pace` | Percentage of maximum | Speed level | Sideways speed |
| --- | ---: | ---: | ---: |
| `"slow"` | `20%` | `4` | `0.2 m/s` |
| `"normal"` | `40%` | `8` | `0.4 m/s` |
| `"fast"` | `80%` | `16` | `0.8 m/s` |

The named paces use fixed percentages of the maximum supported sideways speed:

```text
slow   = 20% × 1.0 m/s = 0.2 m/s
normal = 40% × 1.0 m/s = 0.4 m/s
fast   = 80% × 1.0 m/s = 0.8 m/s
```

`"normal"` is the default pace.

Named paces are convenient presets. They do not define the minimum or maximum supported speed.

### `duration_s`

Sets how long the robot moves sideways, in seconds.

```text
0 < duration_s <= 10.0
```

If omitted from a speed-based call, it defaults to `1.0` second.

Do not provide `duration_s` together with `distance_m`; distance-based calls calculate their duration automatically.

### `distance_m`

Requests an approximate sideways distance in meters.

```text
0 < distance_m <= 2.0
```

The SDK calculates the required movement duration using:

```text
duration_s = distance_m / speed_mps
```

If `speed_mps` is omitted, it defaults to `0.4 m/s`.

The calculated duration must not exceed `10.0` seconds. Otherwise, the call returns `rejected(E_RANGE)`.

For example:

```text
distance_m = 0.4
speed_mps = 0.2
duration_s = 0.4 / 0.2 = 2.0
```

Distance-based movement uses an open-loop estimate. The robot does not confirm that it traveled the exact requested distance.

### Reserved Parameters

The following parameters are reserved but are not currently supported:

| Parameter | Status |
| --- | --- |
| `step_count` | `TBD` — step-count movement is not supported by the current movement interface |
| `step_rate_hz` | `TBD` — step-rate control is not supported by the current movement interface |
| `gait` | `TBD` — gait selection is not supported by the current movement interface |

Passing a reserved parameter returns `rejected(E_TBD_PARAMETER)` before a robot or simulator command is emitted.
<!-- END: Parameters -->

<!-- START: Behavior -->
## Behavior

The SDK first makes sure the robot is standing and ready to move. It then resolves the requested direction, speed, and duration.

If no speed parameter is provided, the SDK uses the default speed of `0.4 m/s`, equivalent to:

```python
pace="normal"
speed_percent=40
speed_level=8
```

Direction is applied in the robot’s current body frame:

```text
left  -> positive lateral velocity
right -> negative lateral velocity
```

The robot moves sideways for the requested or calculated duration, then performs a controlled stop.

If `speed_level=0`, the robot does not move and receives only the stop command.

The call waits until the action succeeds, is rejected, is interrupted, reaches an emergency stop, or times out.

Robot and simulator backends use the same resolved direction, numeric speed, and timing.
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
# Move left at the default "normal" speed of 0.4 m/s for 1 second.
result = Agentech.lateral(direction="left")

# Move right at the minimum nonzero speed.
result = Agentech.lateral(
    direction="right",
    speed_mps=0.05,
    duration_s=1.0,
)

# Move left at 20% of maximum speed: 0.2 m/s.
result = Agentech.lateral(
    direction="left",
    speed_percent=20,
    duration_s=1.0,
)

# Move right at level 8: 0.4 m/s.
result = Agentech.lateral(
    direction="right",
    speed_level=8,
    duration_s=1.0,
)

# Move left at the slow pace: 0.2 m/s.
result = Agentech.lateral(
    direction="left",
    pace="slow",
    duration_s=1.0,
)

# Move right at the normal pace: 0.4 m/s.
result = Agentech.lateral(
    direction="right",
    pace="normal",
    duration_s=1.0,
)

# Move left at the fast pace: 0.8 m/s.
result = Agentech.lateral(
    direction="left",
    pace="fast",
    duration_s=1.0,
)

# Move right approximately 0.4 meters in 2 seconds.
result = Agentech.lateral(
    direction="right",
    distance_m=0.4,
    speed_mps=0.2,
)

# Move left approximately 0.8 meters using the default speed.
# The calculated duration is 0.8 / 0.4 = 2 seconds.
result = Agentech.lateral(
    direction="left",
    distance_m=0.8,
)

# Send a stop command without moving sideways.
result = Agentech.lateral(
    direction="left",
    speed_level=0,
)
```
<!-- END: Example -->
