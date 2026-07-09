# English SDK Cards

This directory is the English reading entry for Agentech L0.5 SDK cards.

Use these cards when you need the English API contract for bounded atomic Aegis robot-dog skills: movement, posture, safety, and sensing/posture adjustment.

## What This Language Pack Contains

| Layer | Count | Scope |
| --- | ---: | --- |
| `L0.0` | 1 | English telemetry snapshot card, linked from `../../../L0.0/cards/get_battery_status.en.md` |
| `L0.5` | 12 | English bounded atomic skill cards in this directory |

## L0.0 English Card

| API | Category | Card |
| --- | --- | --- |
| `Agentech.get_battery_status(parameters)` | Telemetry | `../../../L0.0/cards/get_battery_status.en.md` |

## L0.5 English Cards

| # | API | Category | Card |
| ---: | --- | --- | --- |
| 01 | `Agentech.forward(parameters)` | Movement | `01_forward.md` |
| 02 | `Agentech.backward(parameters)` | Movement | `02_backward.md` |
| 03 | `Agentech.lateral(parameters)` | Movement | `03_lateral.md` |
| 04 | `Agentech.turn(parameters)` | Movement | `04_turn.md` |
| 05 | `Agentech.twist(parameters)` | Movement | `05_twist.md` |
| 06 | `Agentech.backflip(parameters)` | Movement | `06_backflip.md` |
| 07 | `Agentech.jump(parameters)` | Movement | `07_jump.md` |
| 08 | `Agentech.stand(parameters)` | Posture | `08_stand.md` |
| 09 | `Agentech.sit(parameters)` | Posture | `09_sit.md` |
| 10 | `Agentech.stop(parameters)` | Safety | `10_stop.md` |
| 11 | `Agentech.emergency_stop(parameters)` | Safety | `11_emergency_stop.md` |
| 12 | `Agentech.look(parameters)` | Sensing/Posture | `12_look.md` |

## How To Read A Card

Read each card in this order:

1. `Definition`: confirm the layer, category, and purpose.
2. `Syntax`: copy the valid callable shape.
3. `Constraints`: check selector rules and rejection behavior.
4. `Defaults`: confirm what omitted parameters do.
5. `Parameters`: check ranges, units, mappings, and engineering notes.
6. `Behavior`: understand runtime execution.
7. `Return`: branch on stable return fields.
8. `Example`: use concrete values from real calls.

## English Style Contract

English cards use concise engineering language. The text should make the public API clear without exposing internal controller details, device-specific implementation names, or undocumented recovery logic.

All Python SDK parameters use `snake_case`, and `Syntax` shows parameter names and types only. Concrete values belong in `Example`.
