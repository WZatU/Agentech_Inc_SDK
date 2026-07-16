# `Agentech.diagonal()`

<!-- START: Definition -->
## Definition

**L0.5 · Movement · Aegis** — Move diagonally with public X/Y coordinates or an angle, speed, and duration. Positive X is right, positive Y is forward, and positive angles point right.

Source: [EAIC HUB Aegis SDK](https://www.agent-tech.ai/agentech-products/eaic-hub/view-sdk), synchronized 2026-07-16.
<!-- END: Definition -->

<!-- START: Syntax -->
## Syntax

```python
Agentech.diagonal()
Agentech.diagonal(x_m=0.5, y_m=1.0, duration_s=2.0)
Agentech.diagonal(angle_deg=45, speed_mps=0.5, duration_s=2.0)
```
<!-- END: Syntax -->

<!-- START: Constraints -->
## Constraints

1. Inputs must match the exact types and ranges in the parameter table; out-of-range inputs are rejected rather than silently reinterpreted.
2. The theoretical path is 1 meter. Diagonal movement is open loop, so acceleration, stopping, and wheel slip can change the actual distance.
3. Positive X moves right and negative X moves left. Positive Y moves forward and negative Y moves backward. Both X and Y must be nonzero.
4. 0 degrees is forward. Positive angles point right and negative angles point left. Use forward, backward, or lateral for cardinal directions.
<!-- END: Constraints -->

<!-- START: Defaults -->
## Defaults

| Source | Default | Status |
| --- | --- | --- |
| Default: forward-right at 45 degrees, 0.5 m/s for 2 seconds | `Agentech.diagonal()` | Available |
| `angle_deg` | `45` | Available |
| `speed_mps` | `0.5` | Available |
| `duration_s` | `2.0` | Available |
<!-- END: Defaults -->

<!-- START: Parameters -->
## Parameters

| Parameter | Type / range | Default | Status | Meaning |
| --- | --- | --- | --- | --- |
| `x_m` | `float (nonzero)` | — | Available | Open-loop right/left displacement. Positive is right; negative is left. |
| `y_m` | `float (nonzero)` | — | Available | Open-loop forward/backward displacement. Positive is forward; negative is backward. |
| `angle_deg` | `float [-180, 180]` | `45` | Available | Direction measured from forward. Positive points right and negative points left. |
| `speed_mps` | `float [0.05, 3.0] m/s` | `0.5` | Available | Combined diagonal speed. Enter a value from 0.05 through 3.0 m/s, inclusive. |
| `duration_s` | `float (0, 10]` | `2.0` | Available | How long to apply the diagonal velocity command. |
<!-- END: Parameters -->

<!-- START: Behavior -->
## Behavior

Move diagonally with public X/Y coordinates or an angle, speed, and duration. Positive X is right, positive Y is forward, and positive angles point right.
<!-- END: Behavior -->

<!-- START: Return -->
## Return

The current website does not publish a more specific return schema for this Skill. Implementations must report success or rejection without changing the published input contract.
<!-- END: Return -->

<!-- START: Example -->
## Example

```python
# Coordinate + duration
Agentech.diagonal(x_m=0.5, y_m=1.0, duration_s=2.0)

# Angle + speed + duration
Agentech.diagonal(angle_deg=45, speed_mps=0.5, duration_s=2.0)
Agentech.diagonal()
```
<!-- END: Example -->
