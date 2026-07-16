# Agentech SDK

This repository organizes Agentech SDK cards by development status, SDK layer,
robot, language, and website category.

## Repository Structure

```text
Agentech_SDK/
├── README.md
├── Unclassify/
│   ├── En/
│   └── Ch/
├── L0.0/
├── L0.5/
├── L1.0/
├── profiles/
└── manifest.json
```

`Unclassify/` is the top-level working inbox. Cards remain there until their
layer, robot, language, and website category are confirmed.

Formal classified cards will use:

```text
<Layer>/<robot>/<language>/<website-category>/<card>.md
```

Example:

```text
L0.5/ff.aegis/En/movement/04_diagonal.md
L0.5/ff.aegis/Ch/movement/04_diagonal.md
```

## SDK Layers

| Layer | Responsibility |
| --- | --- |
| `L0.0` | Raw device, driver, or telemetry read without Agentech interpretation. |
| `L0.5` | Direct bounded SDK action, state read, configuration call, image operation, transform lookup, or adapter call. |
| `L1.0` | Narrow deterministic primitive with typed input/output and bounded side effects. |

Layer classification must be decided before robot and website-category
placement.

## Robot Namespaces

| Namespace | Meaning |
| --- | --- |
| `ff.aegis` | Aegis robot SDK cards |
| `ff.navi` | Navi robot SDK cards |
| `ff.master` | FF Master robot SDK cards; testing has not started |

Do not infer FF Master capabilities from Aegis or Navi.

## Language Rule

English and Chinese cards must remain paired:

```text
En/<same-card>.md
Ch/<same-card>.md
```

Function name, layer, parameters, constraints, defaults, behavior, and return
schema must match across both languages.

## Profiles

`profiles/` stores robot-grounding data used by SDK contracts, including:

- upstream robot methods;
- command ranges and units;
- coordinate signs;
- public wrapper mappings;
- defaults and rejection rules;
- return codes and control modes;
- source provenance and unresolved `TBD` fields.

These profiles are the intended bottom-level data source for SDK definitions,
but their values still require ongoing source and hardware review.
An existing value must not be treated as accurate merely because it appears in
a profile.

## Website Synchronization

The current Aegis card inventory and public parameter contracts are synchronized
from the [EAIC HUB Aegis SDK](https://www.agent-tech.ai/agentech-products/eaic-hub/view-sdk).

- Website Skill names determine which Aegis cards exist.
- Website categories determine the repository category folder.
- Website parameter names, types, ranges, defaults, and availability states are
  preserved in both languages.
- Agentech-confirmed pace ratios override the website's stale development label:
  `slow=20%`, `normal=40%`, and `fast=80%` of maximum supported speed.
- `profiles/` may provide implementation grounding, but it must not overwrite a
  newer published website contract.

## Current Status

- Aegis is synchronized to 21 website Skills and 42 bilingual card files.
- One Aegis sensing Skill is classified under `L0.0`.
- Twenty Aegis movement, posture, and safety Skills are classified under
  `L0.5`.
- `twist` and `look` were removed because they are not present in the current
  Aegis website inventory.
- `Unclassify/En` and `Unclassify/Ch` are currently empty working inboxes.
- The current SDK layer structures are `L0.0`, `L0.5`, and `L1.0`.
- `ff.master` remains empty because testing has not started.
- Only this root README is maintained.

## 记忆总结

Aegis 已按官网同步为 21 个 Skill、42 张中英文卡：电池读取放在
`L0.0/sensing`，其余 20 个直接动作放在 `L0.5` 的 `movement`、
`posture`、`safety` 类别中。官网没有的 `twist` 和 `look` 已删除，
官网新增的 10 个动作已补齐；`Unclassify` 当前为空。参数以官网为准，
但 pace 使用已确认比例：`slow=20%`、`normal=40%`、`fast=80%`。
