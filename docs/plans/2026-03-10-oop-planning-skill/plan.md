# OOP Planning Skill Plan

> For execution: use `forge-implement`.

## Objective

Define and author an AI-agent skill that teaches object-oriented planning best practices through planning-first heuristics, realistic recurring domains, and explicit anti-pattern detection.

## Scope

- In scope:
  - Create the core skill structure and content model.
  - Author a compact entry workflow for planning-time use.
  - Define principle sections for OOP fundamentals and SOLID validation.
  - Include realistic good/bad examples drawn from recurring domains.
  - Add a dedicated anti-pattern catalog and “when not to use OOP” guidance.
  - Organize the skill in a `writing-skills`-aligned layout that remains searchable and testable.
- Out of scope:
  - Implementing production code unrelated to the skill itself.
  - Building beginner-oriented OOP tutorials.
  - Creating toy examples like `Cat`/`Animal`.
  - Performing final skill testing in this planning phase.

## Context Snapshot

- Relevant memory highlights (include `CON-*` / `DEC-*` / `PIT-*` / `OPS-*` / `LRN-*` IDs from `memory.index.json`):
  - `CON-002`: repo/tooling/layout are not yet established, so the plan must not assume runtime or package defaults.
  - `DEC-002`: project purpose is an agent skill for object-oriented planning best practices.
  - `PIT-001`: avoid inventing stack or delivery details without evidence.
  - `LRN-002`: purpose is already stable even though implementation format is still open.
  - `OPS-002`: no default build/lint/test commands should be assumed yet.
- Relevant research highlights:
  - The skill should target advanced AI agents, planning-first, with review support.
  - The structure should be hybrid, heuristic-heavy, and split into fundamentals, SOLID validation, and anti-pattern/non-OOP guidance.
  - Recurring examples should come from billing/subscriptions, fulfillment/logistics, and identity/access management.
  - A short entry workflow should appear at the top of the skill.

## Approach

- Architecture summary:
  - Use a compact `SKILL.md` as the discovery and execution entrypoint.
  - Use `oop-planning-examples.md` as the single support file for detailed recurring-domain examples, full anti-pattern catalog entries, and verification scenarios.
  - Structure the skill in three main parts:
    1. Planning workflow and OOP fundamentals
    2. SOLID as a validation lens
    3. Anti-pattern catalog and non-OOP decision guidance
- Data flow:
  - Agent discovers the skill from trigger-oriented metadata.
  - Agent reads the entry workflow for quick triage.
  - Agent jumps to specific principle or anti-pattern sections for deeper guidance.
  - Agent uses examples and review questions to choose or reject object-oriented structures before implementation.
- Failure handling:
  - Prevent toy-example drift by requiring all examples to map to the three recurring domains.
  - Prevent SOLID cargo culting by subordinating SOLID to the planning fundamentals section.
  - Prevent verbosity drift by keeping `SKILL.md` compact and routing detailed examples, anti-pattern entries, and verification scenarios into `oop-planning-examples.md`.

## Phases

### Phase 1: Structure and Retrieval Model

- Goal: Define the final artifact structure, section order, and retrieval strategy for the skill.
- Dependencies: Confirmed planning decisions from `research.md`.
- Deliverables: Final file inventory, section map, and acceptance criteria for content organization.

### Phase 2: Core Skill Authoring

- Goal: Draft the core `SKILL.md` with the workflow, heuristics, and section navigation.
- Dependencies: Phase 1 structure decisions.
- Deliverables: Search-optimized frontmatter, overview, workflow, and core heuristic sections.

### Phase 3: Example and Anti-Pattern Reference Authoring

- Goal: Author strong real-world examples, anti-examples, and anti-pattern catalog content.
- Dependencies: Phase 2 section map and example acceptance criteria.
- Deliverables: `oop-planning-examples.md` with recurring domain examples, anti-examples, and the full anti-pattern catalog.

### Phase 4: Skill Verification Preparation

- Goal: Prepare skill-specific test scenarios aligned with `writing-skills`.
- Dependencies: Draft skill content and file structure.
- Deliverables: RED/GREEN pressure scenarios and expected failures documented in `oop-planning-examples.md`, plus links from `SKILL.md`.

## Task Anchors (Required for todo.v2 refs)

Use explicit HTML anchors so `todo.json.plan_refs` can be stable:

- `<a id="task-t01"></a>`
- `<a id="task-t02"></a>`
- `<a id="acceptance-ac1"></a>`
- `<a id="acceptance-ac2"></a>`

## Task Breakdown (Narrative Source)

<a id="task-t01"></a>
### Task T01: Define Skill Artifact Structure

- Objective: Decide the concrete file layout, section ordering, and retrieval boundaries for the skill.
- Scope in:
  - Select `SKILL.md` responsibilities.
  - Decide the supporting file strategy.
  - Define the section map and anchor structure.
- Scope out:
  - Writing full section prose.
  - Running skill tests.
- Files:
  - Create:
    - `SKILL.md`
    - supporting reference file(s), if chosen
  - Modify:
    - none yet
  - Test:
    - none in this task
- Planned commands:
  - inspect repo tree
  - validate file placement after authoring
- Expected command results:
  - planned files exist in the selected structure
  - no unrelated files are introduced
- Commit intent/message pattern:
  - `plan skill structure and section map`
- Acceptance criteria ids:
  - `AC1`
  - `AC2`
- Research refs expected in todo:
  - `research.md#decision-1`
  - `research.md#decision-5`
  - `research.md#decision-6`

<a id="task-t02"></a>
### Task T02: Author Core Workflow and Heuristic Sections

- Objective: Write the core planning workflow and principle sections for the skill.
- Scope in:
  - Entry workflow
  - OOP planning heuristics
  - SOLID validation lens
  - review questions and red flags
- Scope out:
  - extended anti-pattern catalog details if separated
  - verification execution
- Files:
  - Create:
    - `SKILL.md`
  - Modify:
    - supporting reference file(s), if chosen
  - Test:
    - future skill verification assets only
- Planned commands:
  - inspect authored markdown
  - validate anchors and references if split files are used
- Expected command results:
  - core skill content is present and navigable
  - section ordering matches the planned retrieval flow
- Commit intent/message pattern:
  - `author core oop planning skill guidance`
- Acceptance criteria ids:
  - `AC1`
  - `AC3`
- Research refs expected in todo:
  - `research.md#decision-3`
  - `research.md#decision-4`
  - `research.md#decision-6`

<a id="task-t03"></a>
### Task T03: Author Real-World Examples and Anti-Pattern Catalog

- Objective: Add strong good/bad examples and a dedicated anti-pattern catalog using the recurring domains.
- Scope in:
  - domain-specific showcase examples
  - anti-examples
  - “when not to use OOP” comparisons
  - anti-pattern catalog entries
- Scope out:
  - testing skill behavior with subagents
- Files:
  - Create:
    - `oop-planning-examples.md`
  - Modify:
    - `SKILL.md`
  - Test:
    - none in this task
- Planned commands:
  - inspect markdown structure and size
  - verify example domains are covered
- Expected command results:
  - each chosen domain appears in the examples
  - anti-pattern catalog is directly retrievable
- Commit intent/message pattern:
  - `add oop examples and anti-pattern guidance`
- Acceptance criteria ids:
  - `AC3`
  - `AC4`
  - `AC5`
- Research refs expected in todo:
  - `research.md#decision-2`
  - `research.md#decision-3`
  - `research.md#decision-6`

<a id="task-t04"></a>
### Task T04: Prepare Skill Verification Scenarios

- Objective: Define the pressure scenarios and evaluation expectations needed to verify the skill under `writing-skills`.
- Scope in:
  - baseline failure scenarios
  - success criteria for the skill
  - verification notes or support file if required
- Scope out:
  - actually executing the verification loop in this planning phase
- Files:
  - Create:
    - none
  - Modify:
    - `SKILL.md`
    - `oop-planning-examples.md`
  - Test:
    - verification execution deferred to implementation/review phases
- Planned commands:
  - inspect verification notes
  - ensure scenarios map to identified agent failure modes
- Expected command results:
  - pressure scenarios are documented
  - verification approach is aligned with `writing-skills`
- Commit intent/message pattern:
  - `plan skill verification scenarios`
- Acceptance criteria ids:
  - `AC2`
  - `AC6`
- Research refs expected in todo:
  - `research.md#entry-2`
  - `research.md#decision-4`
  - `research.md#decision-6`

## Acceptance Criteria

<a id="acceptance-ac1"></a>
- AC1: The skill has a compact, searchable entrypoint with clear trigger-oriented metadata and a planning-first workflow.
  - Verification method: Review `SKILL.md` structure and frontmatter against the planned section map.

<a id="acceptance-ac2"></a>
- AC2: The skill organization follows `writing-skills` guidance closely enough to support later pressure-style verification, with RED/GREEN scenario preparation documented in `oop-planning-examples.md`.
  - Verification method: Check for compact core structure, clear section responsibilities, and explicit RED/GREEN verification scenarios in `oop-planning-examples.md`.

<a id="acceptance-ac3"></a>
- AC3: The skill teaches both when OOP/SOLID is appropriate and when non-OOP or simpler designs are preferable.
  - Verification method: Review heuristics, examples, and anti-pattern sections for balanced guidance.

<a id="acceptance-ac4"></a>
- AC4: The skill uses realistic recurring domain examples and avoids toy entity examples.
  - Verification method: Confirm billing/subscriptions, fulfillment/logistics, and identity/access management examples appear in authored content.

<a id="acceptance-ac5"></a>
- AC5: The skill includes a dedicated anti-pattern catalog covering class-heavy misuse and weak encapsulation patterns.
  - Verification method: Review anti-pattern section headings and example mappings.

<a id="acceptance-ac6"></a>
- AC6: The plan defines how the skill will be verified using `writing-skills` before completion claims are made, including baseline failure scenarios and expected compliant behavior documented in `oop-planning-examples.md`.
  - Verification method: Inspect `T04` and the planned RED/GREEN verification scenario notes in `oop-planning-examples.md`.

## Test Strategy

- Unit: Not applicable; this work is documentation/skill authoring rather than runtime code.
- Integration: Validate that `SKILL.md` and any support files reference each other coherently and support the intended retrieval flow.
- End-to-end: During later phases, run `writing-skills`-style pressure scenarios to observe agent behavior without and with the drafted skill.
- Regression: Re-run the verification scenarios after any major refactor to ensure anti-pattern guardrails remain explicit.

## Rollback / Recovery

- Trigger: The drafted skill becomes too verbose, loses retrieval clarity, or drifts into beginner/tutorial framing.
- Rollback method: Reduce `SKILL.md` to the compact workflow and heuristic skeleton, move overflow content into support files, and re-validate against acceptance criteria.

## Open Questions

- Question: What final skill name and description best optimize discovery without over-explaining the workflow?
  - Owner: Implementer during authoring

## Review Plan Decision - 2026-03-10

- decision: reviewed
- alignment summary:
  - `A01` aligned
  - `A02` contradicted -> corrected
  - `A03` partial -> corrected
  - `A04` extra -> corrected
- finding decision ledger:
  - `A02` -> yes
  - `A03` -> yes
  - `A04` -> yes
  - `H01` -> yes
  - `H02` -> yes
  - `H03` -> folded into accepted nearby edits
- selected sets:
  - Lock a strict two-file architecture with `SKILL.md` and `oop-planning-examples.md`
  - Store verification scenarios in `oop-planning-examples.md`
  - Remove `AC4` ownership from `T02`
  - Clarify that `SKILL.md` routes to detailed anti-pattern entries in `oop-planning-examples.md`
- residual risks accepted:
  - The final skill name and frontmatter description still need authoring-time judgment.

## Review Mitigation Deltas

- Locked the initial file structure to two files: `SKILL.md` and `oop-planning-examples.md`.
- Assigned detailed examples, anti-pattern catalog entries, and verification scenarios to `oop-planning-examples.md`.
- Kept `SKILL.md` as the compact discovery/workflow entrypoint with routing to deeper material.
- Tightened AC2 and AC6 to require explicit RED/GREEN verification scenarios in the support file.
- Removed premature `AC4` ownership from `T02`.

## Implementation Review Decision - 2026-03-10

- decision: reviewed
- alignment summary:
  - `A01` aligned
  - `A02` aligned
  - `A03` partial -> improvement accepted
  - `A04` aligned
- finding decision ledger:
  - `A03` -> yes
  - `H01` -> yes
  - `H02` -> no action at implementation-review stage
- selected sets:
  - Add explicit anchors and a compact navigation index to `oop-planning-examples.md`
  - Update `SKILL.md` routing to point to named support-file sections
- `forge-iterate` handoff classification:
  - classification: `standard-ready`
  - hard triggers found: `none`
  - weighted risk score and breakdown:
    - retrieval precision risk: 3
    - verification adequacy risk: 2
    - scope drift risk: 0
    - total: 5
  - rationale: The implementation is aligned and scoped correctly; the accepted follow-up is a focused usability/retrieval improvement, not a major redesign.
- residual risks accepted:
  - Verification scenarios may still need stronger multi-pressure combinations during `forge-verify`, but that does not block the focused iteration.

## Implementation Review Deltas

- Add direct navigation support to `oop-planning-examples.md` so future agents can jump to exact domains, anti-patterns, and verification sections.
- Update `SKILL.md` references from file-level routing to section-level routing.

## Append-Only Sections (Reserved)

Use these headings when later phases add durable deltas:

- `## Review Plan Decision - <YYYY-MM-DD>`
- `## Review Mitigation Deltas`
- `## Implementation Review Decision - <YYYY-MM-DD>`
- `## Implementation Review Deltas`
- `## Iteration Major Deltas`
