# `Agentech.squat_backward()`

<!-- START: Definition -->
## Definition

**L0.5 · Movement · Aegis** — Walk backward in the latched low-gait squat stance, then stop and remain squatted.

Source: [EAIC HUB Aegis SDK](https://www.agent-tech.ai/agentech-products/eaic-hub/view-sdk), synchronized 2026-07-16.
<!-- END: Definition -->

<!-- START: Syntax -->
## Syntax

```python
Agentech.squat_backward(speed_mps=0.5, duration_s=2.0)
```
<!-- END: Syntax -->

<!-- START: Constraints -->
## Constraints

1. Inputs must match the exact types and ranges in the parameter table; out-of-range inputs are rejected rather than silently reinterpreted.
2. Before using this movement, make sure the dog is in squat mode by running Agentech.squat().
3. Distance traveled is not guaranteed. Squat movement is open loop, so acceleration, stabilization, and stopping can change the actual distance.
<!-- END: Constraints -->

<!-- START: Defaults -->
## Defaults

No parameter defaults are published on the current website.
<!-- END: Defaults -->

<!-- START: Parameters -->
## Parameters

| Parameter | Type / range | Default | Status | Meaning |
| --- | --- | --- | --- | --- |
| `speed_mps` | `float [0.05, 3.00] m/s` | — | Available | Required positive backward speed magnitude; the method applies the backward direction internally. Negative values and values outside the inclusive range are rejected. |
| `duration_s` | `float (0, 10] seconds` | — | Available | Required time for the low-gait backward command. |
<!-- END: Parameters -->

<!-- START: Behavior -->
## Behavior

Walk backward in the latched low-gait squat stance, then stop and remain squatted.
<!-- END: Behavior -->

<!-- START: Return -->
## Return

The current website does not publish a more specific return schema for this Skill. Implementations must report success or rejection without changing the published input contract.
<!-- END: Return -->

<!-- START: Example -->
## Example

```python
Agentech.squat_backward(speed_mps=0.5, duration_s=2.0)
```
<!-- END: Example -->
