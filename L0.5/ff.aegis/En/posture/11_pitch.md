# `Agentech.pitch()`

<!-- START: Definition -->
## Definition

**L0.5 · Posture · Aegis** — Adjust the body's pitch posture using a positive speed and signed target position. Direction note: negative position moves down, and positive position moves up.

Source: [EAIC HUB Aegis SDK](https://www.agent-tech.ai/agentech-products/eaic-hub/view-sdk), synchronized 2026-07-16.
<!-- END: Definition -->

<!-- START: Syntax -->
## Syntax

```python
Agentech.pitch()
Agentech.pitch(speed_rad_s=0.4, position_rad=0.4)
Agentech.pitch(speed_deg_s=22.92, position_deg=22.98)
```
<!-- END: Syntax -->

<!-- START: Constraints -->
## Constraints

1. Inputs must match the exact types and ranges in the parameter table; out-of-range inputs are rejected rather than silently reinterpreted.
2. Negative position moves down; positive position moves up. Completion time cannot be guaranteed because acceleration, stabilization, and controller timing can change how long the movement takes.
<!-- END: Constraints -->

<!-- START: Defaults -->
## Defaults

| Source | Default | Status |
| --- | --- | --- |
| Default: 0.4 rad/s, position 0.4 rad (maximum up) | `Agentech.pitch()` | Available |
<!-- END: Defaults -->

<!-- START: Parameters -->
## Parameters

| Parameter | Type / range | Default | Status | Meaning |
| --- | --- | --- | --- | --- |
| `speed_rad_s` | `float [0, 0.6]` | — | Available | Positive pitch speed magnitude in radians per second. |
| `speed_deg_s` | `float [0, 34.38]` | — | Available | Positive pitch speed magnitude in degrees per second. |
| `position_rad` | `float [-0.368, 0.4]` | — | Available | Signed target position in radians. Negative moves down; positive moves up. |
| `position_deg` | `float [-21.11, 22.98]` | — | Available | Signed target position in degrees. Negative moves down; positive moves up. |
<!-- END: Parameters -->

<!-- START: Behavior -->
## Behavior

Adjust the body's pitch posture using a positive speed and signed target position. Direction note: negative position moves down, and positive position moves up.
<!-- END: Behavior -->

<!-- START: Return -->
## Return

The current website does not publish a more specific return schema for this Skill. Implementations must report success or rejection without changing the published input contract.
<!-- END: Return -->

<!-- START: Example -->
## Example

```python
Agentech.pitch()
Agentech.pitch(speed_rad_s=0.4, position_rad=0.4)
Agentech.pitch(speed_deg_s=22.92, position_deg=22.98)
```
<!-- END: Example -->
