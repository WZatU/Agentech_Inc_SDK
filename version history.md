# Version History

## 0.3.0 - 2026-07-13

Bottom-level contract correction based on the Agibot ZSL-1 high-level SDK definitions.

- Added `profiles/aegis/zsl1.yaml` as the single source for upstream motion and attitude ranges, coordinate signs, action methods, telemetry fields, return codes, control modes, and Agentech wrapper mappings.
- Defined exact `speed_percent`, `speed_level`, and `pace` resolutions and required robot and simulator backends to share the same resolved command trace.
- Kept previously designed step-count, gait, height, action-style, deceleration-mode, camera-target, and absolute posture-angle fields as explicit non-callable `TBD` entries instead of assigning unsupported values.
- Mapped the existing `sit` wrapper only to normal `lieDown()` and kept it separate from the `passive()` emergency path; limited the executable `look` form to body pitch-rate control while preserving unresolved camera and angle forms as `TBD`.
- Documented open-loop distance and angle formulas without presenting them as measured motion results.
- Added automated consistency checks for bilingual card structure, manifests, parameter ranges, mappings, signs, and stale unsupported fields.

## 0.2.0 - 2026-07-08

Structural cleanup for the SDK documentation repository.

- Renamed the telemetry level package from `L0/` to `L0.0/` to match the integer-plus-one-decimal level naming rule.
- Removed generated aggregate surfaces: root `L0.5.md`, `docs/`, and all `collections/` directories.
- Removed bilingual duplicate card files and kept only `en` and `zh` card sources.
- Updated README and manifests so package indexes point only to canonical card locations.
- Documented planned level sequence: `L0.0`, `L0.5`, `L1.0`, `L1.5`, `L2.0`, `L2.5`.

## 0.1.0 - Initial release

Initial SDK skill-card documentation layout with L0 telemetry, L0.5 atomic skill cards, bilingual aggregate files, collections, and docs outputs.
