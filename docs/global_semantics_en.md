# Agentech.Global

**L0 · Global Semantics** — Execution semantics, shared mappings, and error codes shared by all skill cards; single source of truth, never redefined in individual cards.

## Execution Semantics

| item | constraint |
|---|---|
| call mode | blocking |
| preemption | a new command during execution returns `rejected(E_BUSY)`; only `stop` / `emergency_stop` may preempt |
| profile selection | at most one selector per call; mixing returns `rejected(E_PROFILE_MIXED)` |
| default call | omitting all selectors executes the canonical profile with its defaults |
| disambiguation | when a selector shares a parameter name with another profile's auxiliary, the selector decides the profile (e.g. `DistanceM + SpeedMps` selects `distance-speed`) |
| frame | robot body frame |
| percent basis | the function's own `SafeMax` (or max angle) |

## Shared Mappings

| input | mapping |
|---|---|
| `*Percent` | `value = pct / 100 × SafeMax (or max angle)` |
| `*Level` `1..5` | `20% / 35% / 50% / 70% / 90% × SafeMax (or max angle)` |
| `Pace` | `slow=25%`, `normal=50%`, `fast=75% × SafeMax` |
| distance request | duration estimate only; no arrival verification |

## Return and Error Codes

**Return:** `SkillResult(status, trace_id, error_code, message)` (except L0 telemetry)

| enum | values |
|---|---|
| `status` | `ok | rejected | timeout | preempted | estopped | failed` |
| `error_code` | `E_PROFILE_MIXED | E_RANGE | E_BUSY | E_TIMEOUT | E_SAFETY_GATE | E_UNSUPPORTED | E_STATE | E_INTERNAL` |

**Constraints:** this global card is the single source of truth; individual cards declare only supported profiles plus their own constants and limits.
