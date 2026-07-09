# Agentech Inc SDK

Agentech SDK cards define the public API contract for Aegis robot-dog telemetry and bounded atomic skills.

The purpose of this repository is to make every SDK capability readable by two audiences at the same time:

- developers who need clear function contracts before writing code;
- code-generation agents that need stable, machine-readable sections before calling an SDK function.

Current version: `0.2.0`

## Current Scope

| Layer | Count | Responsibility | Entry |
| --- | ---: | --- | --- |
| `L0.0` | 1 | Direct telemetry snapshot reads | `L0.0/` |
| `L0.5` | 12 | Bounded atomic movement, posture, safety, and sensing/posture skills | `L0.5/` |

Language entry points:

| Language | Entry | Includes |
| --- | --- | --- |
| English | `L0.5/cards/en/README.md` | English L0.5 cards plus the English L0.0 telemetry card |
| Chinese | `L0.5/cards/zh/README.md` | Chinese L0.5 cards plus the Chinese L0.0 telemetry card |

## SDK Philosophy

Each SDK card is a contract, not a tutorial page. A card should tell a developer exactly what can be called, which parameters are legal, what defaults apply, how the robot behaves, and what the caller receives back.

The design goal is small, stable, composable capability descriptions:

| Principle | Meaning |
| --- | --- |
| Explicit layer | Every API declares the responsibility level it belongs to. |
| Small action surface | Each card describes one bounded capability. |
| Typed call shapes | `Syntax` shows callable shapes with parameter names and types. |
| No hidden defaults | `Defaults` states exactly what happens when optional parameters are omitted. |
| Stable failure model | `Constraints` and `Return` describe rejection, timeout, preemption, and emergency-stop behavior. |
| Machine extraction | HTML comments mark every card section so tools can extract modules reliably. |

## Layer Model

Agentech SDK uses level folders to keep responsibility boundaries explicit.

| Layer | Responsibility | Typical Return | Current Status |
| --- | --- | --- | --- |
| `L0.0` | Read one direct device telemetry snapshot. | Typed telemetry snapshot | Active |
| `L0.5` | Execute one bounded SDK skill or safety/posture command. | `SkillResult` | Active |
| `L1.0` | Build a narrow primitive from lower-level actions. | Typed primitive result | Planned |
| `L1.5` | Combine primitives into reusable measurement, verification, or observation. | Evidence-backed skill result | Planned |
| `L2.0` | Answer one domain-level scene question. | Domain decision | Planned |
| `L2.5` | Prepare a workflow package, route package, or checklist. | Execution-ready package | Planned |

## Repository Structure

| Path | Content |
| --- | --- |
| `L0.0/README.md` | L0.0 package index |
| `L0.0/cards/` | English and Chinese L0.0 telemetry cards |
| `L0.5/README.md` | L0.5 package index |
| `L0.5/cards/en/README.md` | English reading entry |
| `L0.5/cards/en/` | English L0.5 cards |
| `L0.5/cards/zh/README.md` | Chinese reading entry |
| `L0.5/cards/zh/` | Chinese L0.5 cards |
| `manifest.json` | Repository-level card index |
| `version history.md` | Version history |

## Card Anatomy

Every card follows the same module order:

| Module | Purpose |
| --- | --- |
| `Definition` | Layer, category, and function purpose |
| `Syntax` | Callable shapes with parameter names and types |
| `Constraints` | Legal combinations, selector rules, and rejection behavior |
| `Defaults` | Exact behavior when optional parameters are omitted |
| `Parameters` | Ranges, units, mappings, and engineering notes |
| `Behavior` | Runtime execution semantics |
| `Return` | Return type and stable fields |
| `Example` | Concrete calls with values |

Module markers are part of the contract:

```md
<!-- START: Parameters -->
## Parameters

...
<!-- END: Parameters -->
```

## Extracting Card Modules

Developers can extract a single module by marker name:

```python
from pathlib import Path
import re

MODULE_RE = re.compile(
    r"<!-- START: ([A-Za-z0-9_-]+) -->(.*?)<!-- END: \1 -->",
    re.DOTALL,
)

def extract_modules(path: str) -> dict[str, str]:
    text = Path(path).read_text(encoding="utf-8")
    return {name: body.strip() for name, body in MODULE_RE.findall(text)}

modules = extract_modules("L0.5/cards/en/01_forward.md")
print(modules["Syntax"])
```

## API Naming

Python SDK parameters use `snake_case`.

| Parameter | Meaning |
| --- | --- |
| `speed_mps` | Speed in meters per second |
| `duration_s` | Duration in seconds |
| `speed_percent` | Product-calibrated speed percentage |
| `step_rate_hz` | Step rate in hertz |

## Parameter Profiles

A parameter profile is one supported way to express the same SDK action. A selector parameter chooses the profile, and auxiliary parameters configure that selected profile.

```python
Agentech.forward(speed_percent=40, duration_s=1.0)
```

In this call, `speed_percent` selects the `percent-time` profile and `duration_s` configures that profile.

Mixed selectors are rejected:

```python
Agentech.forward(speed_percent=40, speed_level=3)
```

This returns `rejected(E_PROFILE_MIXED)`.
