# `Agentech.yaw()`

<!-- START: Definition -->
## Definition

**L0.5 · Posture · Aegis** — Adjust the body's yaw posture using a positive speed and signed target position. Direction note: negative position moves left, and positive position moves right.

Source: [EAIC HUB Aegis SDK](https://www.agent-tech.ai/agentech-products/eaic-hub/view-sdk), synchronized 2026-07-16.
<!-- END: Definition -->

<!-- START: Syntax -->
## Syntax

```python
Agentech.yaw()
Agentech.yaw(speed_rad_s=0.4, position_rad=0.4426)
Agentech.yaw(speed_deg_s=22.92, position_deg=25.36)
```
<!-- END: Syntax -->

<!-- START: Constraints -->
## Constraints

1. Inputs must match the exact types and ranges in the parameter table; out-of-range inputs are rejected rather than silently reinterpreted.
2. Negative position moves left; positive position moves right. Completion time cannot be guaranteed because acceleration, stabilization, and controller timing can change how long the movement takes.
<!-- END: Constraints -->

<!-- START: Defaults -->
## Defaults

| Source | Default | Status |
| --- | --- | --- |
| Default: 0.4 rad/s, position +0.4426 rad (maximum right) | `Agentech.yaw()` | Available |
<!-- END: Defaults -->

<!-- START: Parameters -->
## Parameters

| Parameter | Type / range | Default | Status | Meaning |
| --- | --- | --- | --- | --- |
| `speed_rad_s` | `float [0, 0.6]` | — | Available | Positive yaw speed magnitude in radians per second. |
| `speed_deg_s` | `float [0, 34.38]` | — | Available | Positive yaw speed magnitude in degrees per second. |
| `position_rad` | `float [-0.466, 0.4426]` | — | Available | Signed target position in radians. Negative moves left; positive moves right. |
| `position_deg` | `float [-26.73, 25.36]` | — | Available | Signed target position in degrees. Negative moves left; positive moves right. |
<!-- END: Parameters -->

<!-- START: Behavior -->
## Behavior

Adjust the body's yaw posture using a positive speed and signed target position. Direction note: negative position moves left, and positive position moves right.
<!-- END: Behavior -->

<!-- START: Return -->
## Return

The current website does not publish a more specific return schema for this Skill. Implementations must report success or rejection without changing the published input contract.
<!-- END: Return -->

<!-- START: Example -->
## Example

```python
Agentech.yaw()
Agentech.yaw(speed_rad_s=0.4, position_rad=0.4426)
Agentech.yaw(speed_deg_s=22.92, position_deg=25.36)
```
<!-- END: Example -->
