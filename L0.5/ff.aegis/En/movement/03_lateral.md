# `Agentech.lateral_left() / Agentech.lateral_right()`

<!-- START: Definition -->
## Definition

**L0.5 · Movement · Aegis** — Move sideways using the matching left or right function.

Source: [EAIC HUB Aegis SDK](https://www.agent-tech.ai/agentech-products/eaic-hub/view-sdk), synchronized 2026-07-16.
<!-- END: Definition -->

<!-- START: Syntax -->
## Syntax

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
## Constraints

1. Inputs must match the exact types and ranges in the parameter table; out-of-range inputs are rejected rather than silently reinterpreted.
2. Completion time remains an estimate because acceleration, stabilization, and controller timing can change how long the movement takes.
3. Distance traveled is an estimate, not a guarantee. Acceleration and stopping can change the actual distance.
<!-- END: Constraints -->

<!-- START: Defaults -->
## Defaults

| Source | Default | Status |
| --- | --- | --- |
| Default: 0.5 m/s for 2 seconds | `Agentech.lateral_left() / Agentech.lateral_right()` | Available |
| `speed_mps` | `0.5` | Available |
| `duration_s` | `2.0` | Available |
<!-- END: Defaults -->

<!-- START: Parameters -->
## Parameters

| Parameter | Type / range | Default | Status | Meaning |
| --- | --- | --- | --- | --- |
| `speed_mps` | `float [0.10, 1.0] m/s` | `0.5` | Available | Positive lateral speed in meters per second. The supported range is 0.10 m/s through 1.0 m/s, inclusive. |
| `duration_s` | `float (0, 10] seconds` | `2.0` | Available | How long to apply the lateral movement command. |
| `distance_m` | `float [0, 2] meters` | — | Available | Requested open-loop lateral travel distance, including 0 and 2 meters. A value of 0 is accepted and produces no lateral movement. |
<!-- END: Parameters -->

<!-- START: Behavior -->
## Behavior

Move sideways using the matching left or right function.
<!-- END: Behavior -->

<!-- START: Return -->
## Return

The current website does not publish a more specific return schema for this Skill. Implementations must report success or rejection without changing the published input contract.
<!-- END: Return -->

<!-- START: Example -->
## Example

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
