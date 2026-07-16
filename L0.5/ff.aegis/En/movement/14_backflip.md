# `Agentech.backflip()`

<!-- START: Definition -->
## Definition

**L0.5 · Movement · Aegis** — Run the official standard backflip preset without automatic retry.

Source: [EAIC HUB Aegis SDK](https://www.agent-tech.ai/agentech-products/eaic-hub/view-sdk), synchronized 2026-07-16.
<!-- END: Definition -->

<!-- START: Syntax -->
## Syntax

```python
Agentech.backflip()
```
<!-- END: Syntax -->

<!-- START: Constraints -->
## Constraints

1. Inputs must match the exact types and ranges in the parameter table; out-of-range inputs are rejected rather than silently reinterpreted.
2. `SafetyGate` is still under development and must not be represented as fully validated.
<!-- END: Constraints -->

<!-- START: Defaults -->
## Defaults

| Source | Default | Status |
| --- | --- | --- |
| `variant` | `standard` | Available |
| `stabilize_s` | `5.0` | Available |
<!-- END: Defaults -->

<!-- START: Parameters -->
## Parameters

| Parameter | Type / range | Default | Status | Meaning |
| --- | --- | --- | --- | --- |
| `variant` | `standard` | `standard` | Available | Only the official standard preset is available. |
| `stabilize_s` | `float 0..10` | `5.0` | Available | Post-action stabilization window. |
| `SafetyGate` | `system behavior` | — | Development | Formal battery, posture, and readiness thresholds are being implemented. |
<!-- END: Parameters -->

<!-- START: Behavior -->
## Behavior

Run the official standard backflip preset without automatic retry.
<!-- END: Behavior -->

<!-- START: Return -->
## Return

The current website does not publish a more specific return schema for this Skill. Implementations must report success or rejection without changing the published input contract.
<!-- END: Return -->

<!-- START: Example -->
## Example

```python
Agentech.backflip(variant="standard", stabilize_s=5.0)
Agentech.backflip()
```
<!-- END: Example -->
