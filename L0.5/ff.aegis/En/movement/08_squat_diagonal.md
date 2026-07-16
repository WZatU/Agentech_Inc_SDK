# `Agentech.squat_diagonal()`

<!-- START: Definition -->
## Definition

**L0.5 · Movement · Aegis** — Move diagonally in the latched low-gait squat stance using an angle, speed, and duration, then remain squatted.

Source: [EAIC HUB Aegis SDK](https://www.agent-tech.ai/agentech-products/eaic-hub/view-sdk), synchronized 2026-07-16.
<!-- END: Definition -->

<!-- START: Syntax -->
## Syntax

```python
Agentech.squat_diagonal(angle_deg=45, speed_mps=0.5, duration_s=2.0)
```
<!-- END: Syntax -->

<!-- START: Constraints -->
## Constraints

1. Inputs must match the exact types and ranges in the parameter table; out-of-range inputs are rejected rather than silently reinterpreted.
2. Before using this movement, make sure the dog is in squat mode by running Agentech.squat().
3. Distance traveled is not guaranteed. Squat movement is open loop, so acceleration, stabilization, and stopping can change the actual distance. Both resolved components must be nonzero and within their limits, so cardinal angles are rejected. Positive angles point right; negative angles point left.
<!-- END: Constraints -->

<!-- START: Defaults -->
## Defaults

No parameter defaults are published on the current website.
<!-- END: Defaults -->

<!-- START: Parameters -->
## Parameters

| Parameter | Type / range | Default | Status | Meaning |
| --- | --- | --- | --- | --- |
| `angle_deg` | `float [-180, 180], non-cardinal` | — | Available | Required direction measured from forward. Positive points right and negative points left; cardinal angles are invalid because both components must move. |
| `speed_mps` | `float > 0, component-limited` | — | Available | Required positive combined diagonal speed. The resolved forward magnitude must be 0.05-3.0 m/s and the resolved lateral magnitude must be 0.1-1.0 m/s. |
| `duration_s` | `float (0, 10] seconds` | — | Available | Required time for the low-gait diagonal command. |
<!-- END: Parameters -->

<!-- START: Behavior -->
## Behavior

Move diagonally in the latched low-gait squat stance using an angle, speed, and duration, then remain squatted.
<!-- END: Behavior -->

<!-- START: Return -->
## Return

The current website does not publish a more specific return schema for this Skill. Implementations must report success or rejection without changing the published input contract.
<!-- END: Return -->

<!-- START: Example -->
## Example

```python
Agentech.squat_diagonal(angle_deg=45, speed_mps=0.5, duration_s=2.0)
```
<!-- END: Example -->
