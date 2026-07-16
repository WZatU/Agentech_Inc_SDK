# `Agentech.stay(time=1.0)`

<!-- START: Definition -->
## Definition

**L0.5 · Posture · Aegis** — Holds the posture the dog has moved to while all four feet remain planted on the ground.

Source: [EAIC HUB Aegis SDK](https://www.agent-tech.ai/agentech-products/eaic-hub/view-sdk), synchronized 2026-07-16.
<!-- END: Definition -->

<!-- START: Syntax -->
## Syntax

```python
Agentech.stay(time=1.0)
```
<!-- END: Syntax -->

<!-- START: Constraints -->
## Constraints

1. Inputs must match the exact types and ranges in the parameter table; out-of-range inputs are rejected rather than silently reinterpreted.
<!-- END: Constraints -->

<!-- START: Defaults -->
## Defaults

No parameter defaults are published on the current website.
<!-- END: Defaults -->

<!-- START: Parameters -->
## Parameters

| Parameter | Type / range | Default | Status | Meaning |
| --- | --- | --- | --- | --- |
| `time` | `float > 0 (no maximum)` | — | Available | How long to hold the current four-foot planted posture. Time must be greater than 0 and has no maximum. |
<!-- END: Parameters -->

<!-- START: Behavior -->
## Behavior

Holds the posture the dog has moved to while all four feet remain planted on the ground.
<!-- END: Behavior -->

<!-- START: Return -->
## Return

The current website does not publish a more specific return schema for this Skill. Implementations must report success or rejection without changing the published input contract.
<!-- END: Return -->

<!-- START: Example -->
## Example

```python
Agentech.stay(time=1.0)
```
<!-- END: Example -->
