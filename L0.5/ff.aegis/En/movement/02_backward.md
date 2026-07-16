# `Agentech.backward()`

<!-- START: Definition -->
## Definition

**L0.5 · Movement · Aegis** — Move backward using one positive speed-magnitude profile; direction is applied internally.

Source: [EAIC HUB Aegis SDK](https://www.agent-tech.ai/agentech-products/eaic-hub/view-sdk), synchronized 2026-07-16.
<!-- END: Definition -->

<!-- START: Syntax -->
## Syntax

```python
Agentech.backward()
Agentech.backward(speed_mps=0.4, duration_s=1.0)
Agentech.backward(distance_m=1.0, speed_mps=0.4)
Agentech.backward(speed_percent=40, duration_s=1.0)
Agentech.backward(speed_level=100, duration_s=1.0)
Agentech.backward(pace="normal", duration_s=1.0)
Agentech.backward(step_count=6, step_rate_hz=1.5)
```
<!-- END: Syntax -->

<!-- START: Constraints -->
## Constraints

1. Inputs must match the exact types and ranges in the parameter table; out-of-range inputs are rejected rather than silently reinterpreted.
2. `pace` is an Agentech-confirmed maximum-speed ratio: `slow=20%`, `normal=40%`, and `fast=80%`.
3. `step_count`, `step_rate_hz` are still under development and must not be represented as fully validated.
4. Distance is an estimate, not a guarantee: the robot needs time to accelerate to the requested speed, so the actual distance traveled may differ from the value you calculate.
5. Time is an estimate, not a guarantee: the robot needs time to accelerate to the requested speed, so the actual time used may differ from the value you calculate.
<!-- END: Constraints -->

<!-- START: Defaults -->
## Defaults

| Source | Default | Status |
| --- | --- | --- |
| Default: 1 m/s for 1 second | `Agentech.backward()` | Available |
| `speed_mps` | `1.0` | Available |
| `duration_s` | `1.0` | Available |
| `step_rate_hz` | `1.5` | Development |
<!-- END: Defaults -->

<!-- START: Parameters -->
## Parameters

| Parameter | Type / range | Default | Status | Meaning |
| --- | --- | --- | --- | --- |
| `speed_mps` | `float [0.05, 3.00]` | `1.0` | Available | Enter a positive backward speed magnitude in meters per second; the SDK applies the negative body-X direction internally. Negative public inputs and out-of-range values are rejected. |
| `duration_s` | `float (0, 10]` | `1.0` | Available | How long to hold the movement command. Must be greater than 0 and no more than 10 seconds. |
| `distance_m` | `float [0, 2]` | — | Available | Requested travel distance for the distance-and-speed profile. This is an open-loop estimate; acceleration and stopping can change the actual distance. |
| `speed_percent` | `float [0, 100]` | — | Available | Accepts any percentage from 0% through 100%, including decimal values. Use this as a relative speed request; no meters-per-second conversion is promised. |
| `speed_level` | `int [0, 511]` | — | Available | Select one of 512 integer speed levels. Level 0 is the lowest moving-speed level and level 511 is the highest. |
| `pace` | `enum {slow, normal, fast}` | — | Available | Named maximum-speed ratios: slow=20%, normal=40%, fast=80%. |
| `step_count` | `int [1, 10]` | — | Development | Estimated, not physically counted. |
| `step_rate_hz` | `float [0.5, 3.0]` | `1.5` | Development | Estimated cadence only. |
<!-- END: Parameters -->

<!-- START: Behavior -->
## Behavior

Move backward using one positive speed-magnitude profile; direction is applied internally.
<!-- END: Behavior -->

<!-- START: Return -->
## Return

The current website does not publish a more specific return schema for this Skill. Implementations must report success or rejection without changing the published input contract.
<!-- END: Return -->

<!-- START: Example -->
## Example

```python
Agentech.backward(speed_mps=1.0, duration_s=1.0)
Agentech.backward()
Agentech.backward(speed_mps=0.4, duration_s=1.0)
Agentech.backward(distance_m=1.0, speed_mps=0.4)
Agentech.backward(speed_percent=40, duration_s=1.0)
Agentech.backward(speed_level=100, duration_s=1.0)
Agentech.backward(pace="normal", duration_s=1.0)
Agentech.backward(step_count=6, step_rate_hz=1.5)
```
<!-- END: Example -->
