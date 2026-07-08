# Agentech Inc SDK

Agentech SDK skill-card specifications for robot-dog control, telemetry, posture, safety, and sensing.

Current version: `0.2.0`

This repository contains 13 SDK cards:

- 1 L0.0 telemetry card
- 12 L0.5 atomic skill cards
- English and Chinese Markdown versions

## Level Naming

All level package folders use `L<integer>.<single decimal>` format.

Current planned level sequence:

- `L0.0`
- `L0.5`
- `L1.0`
- `L1.5`
- `L2.0`
- `L2.5`

Current active packages are `L0.0/` and `L0.5/`.

## Repository Structure

| path | content |
|---|---|
| `L0.0/` | L0.0 telemetry/data-read package |
| `L0.5/` | L0.5 atomic skill-card package |
| `manifest.json` | repository index |
| `version history.md` | version history |

## L0.0 Package

`L0.0/` contains direct telemetry/data-read cards.

Current card:

- `Agentech.get_battery_status`

L0.0 cards read state only. They do not command motion, stream over time, make safety decisions, or schedule tasks.

## L0.5 Package

`L0.5/` contains bounded atomic skill cards.

Current cards:

- `Agentech.forward`
- `Agentech.backward`
- `Agentech.lateral`
- `Agentech.turn`
- `Agentech.twist`
- `Agentech.backflip`
- `Agentech.jump`
- `Agentech.stand`
- `Agentech.sit`
- `Agentech.stop`
- `Agentech.emergency_stop`
- `Agentech.look`

L0.5 cards are direct, bounded SDK skills. They do not perform obstacle avoidance, target selection, arrival verification, recovery, scheduling, or task planning.

## Parameter Profile Constraint

Each function may support multiple parameter profiles, but each call may select at most one profile.

Example:

```matlab
Agentech.forward(SpeedPercent=30, DurationS=1.0)
```

`SpeedPercent` selects the `percent-time` profile. `DurationS` is an auxiliary parameter.

Invalid mixed-profile call:

```matlab
Agentech.forward(SpeedPercent=30, SpeedLevel=3)
```

This returns `rejected(E_PROFILE_MIXED)`.

## Main Entry Points

| file | purpose |
|---|---|
| `L0.0/cards/get_battery_status.en.md` | English L0.0 card |
| `L0.0/cards/get_battery_status.zh.md` | Chinese L0.0 card |
| `L0.5/cards/en/` | English L0.5 cards |
| `L0.5/cards/zh/` | Chinese L0.5 cards |
