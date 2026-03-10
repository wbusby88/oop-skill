# Memory Archive

> This file can grow large. Prefer using `memory.index.json` to find relevant IDs, then jump to anchors here.

## Constraints

<a id="con-001"></a>
### CON-001

- Full details: Forge lifecycle work in this repository should keep durable project context in Memory v2 artifacts at repo root instead of relying on transient chat state.

<a id="con-002"></a>
### CON-002

- Full details: As of 2026-03-10, the repository has no implementation files, manifests, or runtime/tooling configuration, so technical defaults are unproven.

## Decisions

<a id="dec-001"></a>
### DEC-001

- Full details: Memory v2 was initialized in new-project mode because the workspace contained no prior memory files and no meaningful implementation history.

<a id="dec-002"></a>
### DEC-002

- Full details: On 2026-03-10, the user defined the project purpose as an agent skill for object-oriented planning best practices.

## Pitfalls

<a id="pit-001"></a>
### PIT-001

- Full details: The main early-stage risk is inventing technical facts that are not supported by repository evidence or direct user input.

<a id="pit-002"></a>
### PIT-002

- Full details: For this repository, letting SOLID dominate the skill structure would likely create checklist-driven, fake-OOP guidance instead of planning judgment. The planned mitigation is to lead with OOP planning fundamentals and treat SOLID as a validation lens.

## Learnings

<a id="lrn-001"></a>
### LRN-001

- Full details: For empty repositories, capture workflow defaults and known unknowns first; treat implementation details as future updates.

<a id="lrn-002"></a>
### LRN-002

- Full details: A confirmed project purpose is durable enough to shape future plans even when packaging, runtime, and repo layout are still unknown.

## Operational Defaults

<a id="ops-001"></a>
### OPS-001

- Full details: `memory.md`, `memory.index.json`, and `memory.archive.md` at repo root are the canonical project memory set.

<a id="ops-002"></a>
### OPS-002

- Full details: No build, lint, or test commands are currently established for this repository.

<a id="ops-003"></a>
### OPS-003

- Full details: Startup context digest on 2026-03-10:
  - Project purpose: agent skill for object-oriented planning best practices
  - Primary language/framework/runtime: unknown
  - Package manager: unknown
  - Build/lint/test commands: unknown
  - Primary source/test roots: unknown
  - Plans root preference: unknown
  - Workflow constraints from `AGENTS.md`: follow named skill routing, keep Memory v2 at root, do not skip required lifecycle artifacts.

<a id="ops-004"></a>
### OPS-004

- Full details: Planning on 2026-03-10 established a default authoring structure of a compact `SKILL.md` plus one supporting reference/examples file, unless implementation proves that the support content must be split further.
