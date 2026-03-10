# Memory (v2)

> This file must stay small. Every agent should read it fully.

## Working Set (Read This Fully)

**Hard cap:** max `12` entries total across all categories.

**Rule:** If you add a new working-set entry, you must merge or demote another entry to `memory.archive.md`.

### Constraints

<a id="con-001"></a>
- **CON-001**:
  - Constraint: Do not skip Forge lifecycle artifacts when the user invokes a Forge phase skill.
  - How to comply: Keep durable project context in Memory v2 at repo root and hand later phases a stable startup digest.
  - Evidence (verification/incidents/links): `AGENTS.md` skill routing rules and the active `forge-init` workflow.

<a id="con-002"></a>
- **CON-002**:
  - Constraint: The repository currently has no implementation files, package manifest, or runtime configuration.
  - How to comply: Treat current stack, commands, and source roots as unknown until evidence appears or the user specifies them.
  - Evidence (verification/incidents/links): Top-level repo inspection on 2026-03-10 found only `.git`, `.idea`, and `.conductor`.

### Decisions

<a id="dec-001"></a>
- **DEC-001**:
  - Decision: Initialize Memory v2 as a new-project repository bootstrap.
  - Rationale: No prior memory artifacts or meaningful implementation history exist in the workspace.
  - Alternatives: Delay memory creation until implementation begins.
  - Implications: Future Forge phases should update memory as the project purpose, stack, and defaults become concrete.

<a id="dec-002"></a>
- **DEC-002**:
  - Decision: Position this repository as an agent skill focused on object-oriented planning best practices.
  - Rationale: User provided the project purpose directly on 2026-03-10.
  - Alternatives: Keep the purpose unspecified until more implementation detail exists.
  - Implications: Planning and content artifacts should optimize for reusable guidance, structure, and heuristics around OOP-oriented planning.

### Pitfalls

<a id="pit-001"></a>
- **PIT-001**:
  - Symptom: Plans assume a language, framework, or package manager that is not actually present.
  - Root cause: Empty repos invite speculative defaults.
  - Prevention: Mark missing repo facts as unknown or candidate-only until the user or checked-in files confirm them.
  - Evidence: Current repo surface provides no implementation evidence.

### Learnings

<a id="lrn-001"></a>
- **LRN-001**:
  - Learning: In repo bootstrap state, the first durable value is workflow context, not technical implementation detail.
  - When it applies: Before source files, manifests, or architecture docs exist.
  - How to apply: Capture process defaults and known absences in memory, then refine once implementation lands.
  - Evidence: `forge-init` requires startup context even for new projects.

<a id="lrn-002"></a>
- **LRN-002**:
  - Learning: The first stable domain fact is the skill's purpose, even before its delivery format or stack is chosen.
  - When it applies: Early-stage skill repositories where content direction is known but implementation details are not.
  - How to apply: Anchor future planning around object-oriented planning best practices and keep execution/tooling details provisional.
  - Evidence: User input on 2026-03-10.

### Operational Defaults

<a id="ops-001"></a>
- **OPS-001**:
  - Rule/default: Use repo-root Memory v2 files (`memory.md`, `memory.index.json`, `memory.archive.md`) as the canonical project memory store.
  - How it affects plans: Later Forge phases should read `memory.md` fully and consult the index for targeted retrieval before planning.
  - How to comply: Update existing entries in place; archive long-tail details instead of growing the working set.

<a id="ops-002"></a>
- **OPS-002**:
  - Rule/default: Until package tooling exists, do not assume default build, lint, or test commands.
  - How it affects plans: `forge-plan` and `forge-quick` must either derive commands from newly added manifests or ask the user.
  - How to comply: Keep commands unset in memory until evidence is available.

## How To Use Memory (Read This Once)

1. Always read the **Working Set** above.
2. For targeted retrieval, consult `memory.index.json`:
   - filter by `tags` and `applies_to`
   - pull relevant IDs into plan/review packets as a “Memory Digest”
3. Prefer updating existing entries over appending duplicates.
4. If a new insight is durable but not yet fully proven, add it as `status: candidate` in `memory.index.json` and promote it during verification.

## Project Summary

- Name: oop-skill
- Purpose: Agent skill for object-oriented planning best practices.
- Audience: Assumption: agents or developers authoring/using planning workflows. User confirmation still useful.

## Tech Stack

- Languages: Unknown.
- Frameworks: Unknown.
- Tooling: Git repository with no detected package manager or runtime configuration yet. Delivery format for the skill is still unspecified.

## Registry Files

- `memory.index.json` (canonical registry; IDs, tags, applies_to, links)
- `memory.archive.md` (long tail; can be large; prefer index-driven access)
