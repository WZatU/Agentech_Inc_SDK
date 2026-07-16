# `Agentech.turn()`

<!-- START: Definition -->
## Definition

**L0.5 · Movement · Aegis** — Turn using signed angles or rates. Direction note: all negative values turn left, and all positive values turn right. The default is +45 degrees (right).

Source: [EAIC HUB Aegis SDK](https://www.agent-tech.ai/agentech-products/eaic-hub/view-sdk), synchronized 2026-07-16.
<!-- END: Definition -->

<!-- START: Syntax -->
## Syntax

```python
Agentech.turn()
Agentech.turn(angle_deg=45, turn_rate_deg_s=22.5)
Agentech.turn(angle_rad=0.7854, turn_rate_rad_s=0.3927)
Agentech.turn(rate_percentage=40, duration_s=2.0)
Agentech.turn(turn_level=256, duration_s=2.0)
Agentech.turn(turn_rate_deg_s=45, duration_s=2.0)
Agentech.turn(turn_rate_rad_s=0.7854, duration_s=2.0)
Agentech.turn_right()
Agentech.turn_left()
Agentech.u_turn()
```
<!-- END: Syntax -->

<!-- START: Constraints -->
## Constraints

1. Inputs must match the exact types and ranges in the parameter table; out-of-range inputs are rejected rather than silently reinterpreted.
2. One full circle is 360 degrees, which equals 2pi radians. If you omit the rate, it defaults to 2 rad/s.
<!-- END: Constraints -->

<!-- START: Defaults -->
## Defaults

| Source | Default | Status |
| --- | --- | --- |
| Default: turn right 45 degrees | `Agentech.turn()` | Available |
<!-- END: Defaults -->

<!-- START: Parameters -->
## Parameters

| Parameter | Type / range | Default | Status | Meaning |
| --- | --- | --- | --- | --- |
| `angle_rad` | `float (unbounded)` | — | Available | Signed target angle in radians. Negative turns left; positive turns right. One full circle is 2pi radians (360 degrees). |
| `turn_rate_rad_s` | `float [-3, 3]` | — | Available | Signed turn rate in radians per second. Negative turns left; positive turns right. |
| `angle_deg` | `float (unbounded)` | — | Available | Signed target angle in degrees. Negative turns left; positive turns right. One full circle is 360 degrees. |
| `turn_rate_deg_s` | `float [-120, 120]` | — | Available | Signed turn rate in degrees per second. Negative turns left; positive turns right. |
| `rate_percentage` | `float [-100, 100]` | — | Available | Signed percentage of the maximum turn rate. Negative turns left; positive turns right. |
| `turn_level` | `int [-511, 511]` | — | Available | Signed turn-rate level: -511 is maximum left, 0 is neutral, and 511 is maximum right. |
| `duration_s` | `float > 0 (no maximum)` | — | Available | How long to apply a rate-based turn command. There is no maximum duration. |
| `turn_right()` | `convenience call` | — | Available | Fixed right 90-degree turn with no parameters. |
| `turn_left()` | `convenience call` | — | Available | Fixed left 90-degree turn with no parameters. |
| `u_turn()` | `convenience call` | — | Available | Fixed left 180-degree turn with no parameters. |
<!-- END: Parameters -->

<!-- START: Behavior -->
## Behavior

Turn using signed angles or rates. Direction note: all negative values turn left, and all positive values turn right. The default is +45 degrees (right).
<!-- END: Behavior -->

<!-- START: Return -->
## Return

The current website does not publish a more specific return schema for this Skill. Implementations must report success or rejection without changing the published input contract.
<!-- END: Return -->

<!-- START: Example -->
## Example

```python
Agentech.turn()
Agentech.turn(angle_deg=45, turn_rate_deg_s=22.5)
Agentech.turn(angle_rad=0.7854, turn_rate_rad_s=0.3927)
Agentech.turn(rate_percentage=40, duration_s=2.0)
Agentech.turn(turn_level=256, duration_s=2.0)
Agentech.turn(turn_rate_deg_s=45, duration_s=2.0)
Agentech.turn(turn_rate_rad_s=0.7854, duration_s=2.0)
Agentech.turn_right()
```
<!-- END: Example -->
