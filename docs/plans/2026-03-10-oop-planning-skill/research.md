# Research

## Task Metadata

- Topic: OOP planning best-practices skill for AI agents
- Date: 2026-03-10
- Planner: Codex
- Plans folder: `docs/plans/2026-03-10-oop-planning-skill`

## Interview Log (Structured)

Use explicit HTML anchors so `todo.json.research_refs` can be stable.

<a id="entry-1"></a>
### Entry 1

- Question: What is the project purpose?
- User Response: It is an agent skill for object oriented planning best practices
- Interpretation: The repository should produce a reusable skill artifact focused on OOP planning judgment rather than implementation code or a general tutorial.
- Interim Research: Root repo inspection showed no implementation files or prior plan artifacts. Memory v2 was initialized in new-project mode.
- Open Follow-Up: Determine the best teaching structure for the skill.

<a id="entry-2"></a>
### Entry 2

- Question: Which primary teaching structure should dominate: principle-first, scenario-first, or hybrid?
- User Response: 3 hybrid. Also use $writing-skills to help with skill organisation
- Interpretation: The skill should be organized as a principle-by-principle reference, but grounded in recurring realistic scenarios. `writing-skills` should guide eventual skill organization and verification.
- Interim Research: Reviewed `writing-skills` and captured its impact on discoverability, compact core structure, and testability expectations.
- Open Follow-Up: Choose the example backbone for the hybrid structure.

<a id="entry-3"></a>
### Entry 3

- Question: Which example backbone should the skill use?
- User Response: B ok
- Interpretation: Use three recurring domains rather than a single domain or an isolated anti-pattern sandbox.
- Interim Research: Proposed domains with complementary architectural pressures: billing/subscriptions, fulfillment/logistics, identity/access management.
- Open Follow-Up: Decide whether the skill should teach only good OOP or also when not to use OOP/classes.

<a id="entry-4"></a>
### Entry 4

- Question: Should the skill teach only good OOP/SOLID usage, or also explicitly teach when not to use classes/OOP?
- User Response: 2
- Interpretation: The skill must be balanced and include guidance for when simpler or non-OOP approaches are preferable.
- Interim Research: This increases the importance of anti-pattern detection and decision heuristics rather than principle exposition alone.
- Open Follow-Up: Set the audience level.

<a id="entry-5"></a>
### Entry 5

- Question: Which audience level should the skill target?
- User Response: 3 this is for ai agents
- Interpretation: The skill should target advanced AI agents making planning and review decisions, not beginner human readers.
- Interim Research: This pushes the format toward high-signal heuristics, review questions, and retrieval-friendly sections.
- Open Follow-Up: Decide whether planning or review is the primary operating lens.

<a id="entry-6"></a>
### Entry 6

- Question: Should the skill optimize for planning-time judgment, code-review judgment, or both with planning primary?
- User Response: 3 is good
- Interpretation: The skill should support both planning and review, but should be optimized first for architectural choices before coding begins.
- Interim Research: Planning-first supports an agent workflow that prevents fake OOP before implementation.
- Open Follow-Up: Decide the principle model.

<a id="entry-7"></a>
### Entry 7

- Question: Should the principle set be SOLID-centered, OOP-planning-centered, or split across fundamentals, SOLID, and anti-patterns?
- User Response: 3
- Interpretation: The content model should be split into OOP fundamentals, SOLID validation, and anti-pattern/non-OOP guidance.
- Interim Research: This model best supports both retrieval and a balanced “use OOP / avoid OOP” stance.
- Open Follow-Up: Decide the dominant format style.

<a id="entry-8"></a>
### Entry 8

- Question: Should the skill be reference-heavy, heuristic-heavy, or workflow-heavy?
- User Response: 2
- Interpretation: The skill should emphasize explicit decision rules, red flags, review questions, and high-signal examples.
- Interim Research: Heuristic-heavy format is better aligned with AI-agent usage than long-form explanatory prose.
- Open Follow-Up: Decide how explicit anti-pattern coverage should be.

<a id="entry-9"></a>
### Entry 9

- Question: Should anti-patterns be embedded only, have a dedicated catalog, or dominate the skill?
- User Response: 2
- Interpretation: The skill should keep anti-patterns inside principle sections and also include a separate anti-pattern catalog for direct retrieval.
- Interim Research: Dedicated catalog improves quick diagnosis of fake OOP and class-heavy misuse.
- Open Follow-Up: Confirm the overall understanding before producing a scope brief.

<a id="entry-10"></a>
### Entry 10

- Question: Does the Understanding Lock Summary accurately reflect your intent? Please confirm or correct before I produce the Scope Brief + handoff packet.
- User Response: yes
- Interpretation: The scoped concept is confirmed and can be promoted into planning artifacts.
- Interim Research: Produced a scope brief, option set, decision log, and a recommendation to use `forge-plan`.
- Open Follow-Up: Decide whether the finished skill should include a compact entry workflow.

<a id="entry-11"></a>
### Entry 11

- Question: Should the finished skill include a short entry workflow at the top for agents to follow, or stay purely section-based reference material?
- User Response: what is the recommendation for maximum benefit?
- Interpretation: The user delegated the decision after hearing a recommendation.
- Interim Research: A compact entry workflow improves agent usability by giving a fast path before deeper heuristics.
- Open Follow-Up: Confirm the recommendation.

<a id="entry-12"></a>
### Entry 12

- Question: If that matches your preference, I’ll treat “include compact entry workflow” as decided and continue the plan.
- User Response: yes ok
- Interpretation: The skill should include a short planning-first entry workflow before the deeper heuristic/reference sections.
- Interim Research: This supports a `writing-skills`-aligned structure with a compact, searchable `SKILL.md`.
- Open Follow-Up: Resolve a plans root so planning artifacts can be written.

<a id="entry-13"></a>
### Entry 13

- Question: Recommended location is `docs/plans/` at the repo root. If that works, I’ll create a new dated plan folder there and continue.
- User Response: yes
- Interpretation: Use `docs/plans/2026-03-10-oop-planning-skill/` as the active plan folder.
- Interim Research: Created the plan folder after confirming no existing `docs/plans/` root or prior plan artifacts were present.
- Open Follow-Up: None.

## Understanding Summary

- What is being built: An AI-agent skill for object-oriented planning best practices.
- Why it exists: To improve architectural judgment around when and how to use OOP/SOLID, and to detect fake OOP before or during implementation review.
- Who it is for: Advanced AI agents performing planning-first architectural work and code-review-style design critique.
- Key constraints: Repo is still content-empty; structure must follow skill-writing best practices; examples must be realistic and non-trivial; anti-patterns must be first-class.
- Explicit non-goals: Beginner OOP instruction, toy `Cat`/`Animal` examples, implementation code, and class-heavy guidance that treats OOP as mandatory.

## Non-Functional Requirements

- Performance: Not requested; assume low complexity is preferred for retrieval.
- Scale: Not requested; assume a compact core skill with optional supporting reference material.
- Security/Privacy: No special requirements identified.
- Reliability/Availability: The skill should be robust against common agent failure modes such as over-abstraction and blind SOLID cargo culting.
- Maintenance/Ownership: Keep the core skill compact and searchable; place heavier examples/reference material in supporting files if needed.

## Assumptions

- Assumption: The three proposed domains are acceptable as the recurring example set.
  - Confidence: High
  - Validation plan: Confirm during plan review if needed; adjust only if the domain mix weakens coverage.
- Assumption: A compact entry workflow should be included at the top of `SKILL.md`.
  - Confidence: High
  - Validation plan: Reflect it directly in the plan and review it during skill authoring.
- Assumption: `SKILL.md` plus one supporting reference/examples file is the best initial file structure.
  - Confidence: Medium
  - Validation plan: Evaluate during plan review against content size and retrieval clarity.
- Assumption: The skill should optimize for planning-time use while remaining useful for review-time diagnosis.
  - Confidence: High
  - Validation plan: Ensure the acceptance criteria cover both planning and review workflows.

## Decision Log

<a id="decision-1"></a>
- Decision: Use a hybrid structure with principle-by-principle guidance and recurring domain examples.
  - Alternatives considered: Pure principle-first reference; pure scenario-first workshop.
  - Why chosen: It preserves clarity while keeping examples realistic and connected.
  - Risks: Repeated domains may still feel repetitive if examples are not varied enough.

<a id="decision-2"></a>
- Decision: Use billing/subscriptions, fulfillment/logistics, and identity/access management as recurring domains.
  - Alternatives considered: Single enterprise domain; one domain plus anti-pattern sandbox.
  - Why chosen: The three domains create varied pressures around policy, lifecycle, orchestration, and encapsulation.
  - Risks: Domain breadth could increase writing scope if not curated tightly.

<a id="decision-3"></a>
- Decision: Teach both strong OOP/SOLID usage and when not to use classes or OOP.
  - Alternatives considered: OOP-only guidance; anti-abuse-heavy guidance.
  - Why chosen: Balanced guidance produces better planning judgment and makes anti-pattern detection credible.
  - Risks: The skill could become too broad unless the heuristics stay focused.

<a id="decision-4"></a>
- Decision: Optimize for advanced AI agents with planning as the primary lens and review as a secondary lens.
  - Alternatives considered: Intermediate human-oriented guidance; review-first guidance.
  - Why chosen: The user explicitly wants an agent skill that shapes up-front decisions and catches fake OOP.
  - Risks: Dense content may reduce accessibility for weaker agents if the workflow is not crisp.

<a id="decision-5"></a>
- Decision: Split the content model into OOP planning fundamentals, SOLID validation, and anti-pattern/non-OOP cases.
  - Alternatives considered: SOLID-centered only; broad OOP concepts without explicit SOLID sectioning.
  - Why chosen: This gives better retrieval structure and aligns with the user’s request for both best practices and bad practices.
  - Risks: Section boundaries could blur unless the plan defines them explicitly.

<a id="decision-6"></a>
- Decision: Make the skill heuristic-heavy and include a compact entry workflow plus a dedicated anti-pattern catalog.
  - Alternatives considered: Reference-heavy skill; workflow-heavy skill; embedded anti-patterns only.
  - Why chosen: Agents need fast decision rules and a clear path for diagnosing fake OOP, not long essays.
  - Risks: Over-compression could omit needed nuance in the examples.

<a id="decision-7"></a>
- Decision: Recommend a two-file implementation structure: `SKILL.md` plus one supporting reference/examples file.
  - Alternatives considered: Dense single-file skill; larger multi-file modular skill.
  - Why chosen: A compact `SKILL.md` preserves searchability and retrieval, while a support file can hold heavier examples and anti-pattern matrices without bloating the entrypoint.
  - Risks: Verification guidance may compete for space with examples in the support file if the split is not handled carefully.

## Approach Options

- Option A: Dense single-file skill
  - What it enables: simplest file model and lowest navigation overhead.
  - What it costs: higher risk of an overlong `SKILL.md` with weaker retrieval.
  - Decision drivers: best only if examples remain much shorter than currently expected.
- Option B: `SKILL.md` plus one support file
  - What it enables: compact entrypoint plus deeper scenario/anti-pattern material.
  - What it costs: slightly more structure design work and cross-referencing.
  - Decision drivers: best if the core workflow and heuristics fit cleanly in `SKILL.md` and the heavier examples are likely to expand.
- Option C: Multi-file modular skill
  - What it enables: maximum separation of concerns across heuristics, examples, and verification notes.
  - What it costs: more maintenance burden and a higher chance that agents miss important linked material.
  - Decision drivers: best only if support content becomes too large or conceptually distinct for a two-file structure.

## Recommended Approach

- Recommended option: Option B (`SKILL.md` plus one support file)
- Why:
  - aligns with `writing-skills` guidance to keep the core skill compact and searchable
  - supports the requested real-world examples and anti-pattern depth without turning the main skill into a wall of prose
  - gives a clean place to store domain comparison tables, good/bad examples, and anti-pattern catalog entries

## Risks and Unknowns

- Risk: The final skill may become too long if all examples are embedded in `SKILL.md`.
  - Impact: Reduced discoverability and weaker agent retrieval.
  - Mitigation: Default to `SKILL.md` plus one supporting reference/examples file.
- Risk: The line between “use OOP” and “use simpler structures” may stay too abstract without explicit comparison heuristics.
  - Impact: Agents may still default to classes by habit.
  - Mitigation: Require “choose OOP / avoid OOP” rules in each major section and a dedicated anti-pattern catalog.
- Risk: SOLID could overshadow the broader planning skill and turn into checklist cargo culting.
  - Impact: The skill would reinforce the behavior it aims to prevent.
  - Mitigation: Position SOLID as a validation lens after fundamentals, not as the primary structure.

## Memory Candidates

- Finding to append to `memory.md`: Future work in this repo should bias toward a planning-first, heuristic-heavy skill structure for AI agents.
- Pitfall to append to `memory.md`: Allowing SOLID to dominate the structure risks creating checklist-driven fake OOP rather than planning judgment.

## Review Pass - 2026-03-10

Use this section for `forge-review-plan` findings and mitigation decisions.

- Artifact intake summary:
  - Objective and scope: Author an AI-agent skill for OOP planning best practices with planning-first heuristics, realistic recurring domains, anti-pattern guidance, and later `writing-skills`-style verification.
  - Explicit non-goals: beginner OOP tutorial content, toy examples, unrelated implementation code, and final verification execution during planning.
  - Key decisions/assumptions reviewed: hybrid structure, three recurring domains, balanced OOP/non-OOP guidance, advanced AI-agent audience, planning-first with review support, split content model, heuristic-heavy format, compact entry workflow, and a recommended two-file implementation structure.
  - Acceptance criteria count: 6
  - Task count and dependency shape: 4 tasks in a mostly linear flow (`T01` -> `T02`/`T03` -> `T04`) with `T03` depending on both structure and core guidance.
  - Assumptions most likely to fail: that one support file can carry both examples and anti-pattern depth while verification preparation also stays coherent; that the support-file boundary is fixed enough for implementation without causing task churn.
- Alignment coverage (`Axx`, status, severity, refs, recommended correction):
  - `A01`
    - category: `alignment`
    - intent source: Research understanding summary and decisions 1, 3, 4, 5, 6
    - research refs: `research.md#decision-1`, `research.md#decision-3`, `research.md#decision-4`, `research.md#decision-5`, `research.md#decision-6`
    - plan refs: `plan.md#task-t02`, `plan.md#task-t03`, `plan.md#acceptance-ac1`, `plan.md#acceptance-ac3`, `plan.md#acceptance-ac5`
    - todo refs: `T02`, `T03`
    - status: `aligned`
    - severity: `low`
    - summary: The core plan and task set preserve the planning-first, balanced, heuristic-heavy skill shape requested by the user.
    - recommended correction: None.
  - `A02`
    - category: `alignment`
    - intent source: Research assumption on two-file structure and decision 7
    - research refs: `research.md#decision-7`
    - plan refs: `plan.md#task-t01`, `plan.md#task-t04`
    - todo refs: `T01`, `T04`
    - status: `contradicted`
    - severity: `high`
    - summary: The reviewed plan recommends a compact `SKILL.md` plus one support file, but `todo.json` silently expands the implementation to a third file by creating `skill-verification-notes.md` in `T04`. That changes the approved structure boundary without an explicit review decision.
    - recommended correction: Either keep verification notes inside the single support file and remove the third-file target from `T04`, or explicitly revise the plan to approve a three-file structure before implementation.
  - `A03`
    - category: `alignment`
    - intent source: Acceptance criterion AC4 and the task scopes for T02 and T03
    - research refs: `research.md#decision-2`, `research.md#decision-6`
    - plan refs: `plan.md#task-t02`, `plan.md#task-t03`, `plan.md#acceptance-ac4`
    - todo refs: `T02`, `T03`
    - status: `partial`
    - severity: `medium`
    - summary: `T02` claims AC4 coverage even though its scope explicitly excludes extended example matrices and recurring-domain example authoring is assigned to `T03`. This creates verification ambiguity about when AC4 is actually satisfied.
    - recommended correction: Remove `AC4` from `T02` coverage in `plan.md` and `todo.json`, leaving recurring-domain example acceptance on `T03`.
  - `A04`
    - category: `alignment`
    - intent source: Open question on support-file count and implementation boundary
    - research refs: `research.md#decision-7`
    - plan refs: `plan.md`
    - todo refs: `T01`, `T03`, `T04`
    - status: `extra`
    - severity: `medium`
    - summary: `todo.json` locks concrete filenames (`oop-planning-examples.md`, `skill-verification-notes.md`) before the open file-structure question in `plan.md` is reconciled. The naming choice itself is fine, but the task set currently treats it as decided more strongly than the narrative plan does.
    - recommended correction: Update `plan.md` to resolve the support-file naming/boundary explicitly, or relax `todo.json` to keep the support-file name abstract until implementation finalizes it.
- Hardening findings (`Hxx`, severity, evidence refs):
  - `H01`
    - category: `hardening`
    - critical question answered: Which assumption is weakest and least validated?
    - agent answer: The weakest assumption is that verification preparation can be deferred into a separate file decision late in `T04` without re-opening the approved information architecture. That is the first place two implementers are likely to diverge.
    - evidence refs: `research.md#decision-7`, `plan.md#task-t04`, `todo.json:T04`
    - severity: `high`
    - mitigation options:
      - Option 1: Keep a strict two-file implementation by folding verification scenarios into the support file and cross-linking from `SKILL.md`.
      - Option 2: Explicitly upgrade the plan to a three-file structure now, with named responsibilities for `SKILL.md`, examples/anti-patterns, and verification notes.
    - recommended patch set: Prefer Option 1 unless the user wants verification notes isolated as a first-class artifact.
  - `H02`
    - category: `hardening`
    - critical question answered: Which acceptance criteria or tests are under-specified?
    - agent answer: AC2 and AC6 rely on “verification preparation artifacts,” but the current plan does not explicitly state whether those artifacts belong in the support file or a separate notes file. That leaves room for inconsistent implementations and review disagreements.
    - evidence refs: `plan.md#acceptance-ac2`, `plan.md#acceptance-ac6`, `plan.md#task-t04`, `todo.json:T04`
    - severity: `medium`
    - mitigation options:
      - Option 1: Amend AC2/AC6 and T04 to state that verification scenarios live in the support file unless a later replan approves separation.
      - Option 2: Amend AC2/AC6 and T04 to require a dedicated verification-notes file from the start.
    - recommended patch set: Prefer Option 1 to preserve the approved compact structure.
  - `H03`
    - category: `hardening`
    - critical question answered: Where could two implementers diverge and produce different behavior?
    - agent answer: One implementer could place the anti-pattern catalog mostly in `SKILL.md` while another puts it entirely in the support file, because the plan requires direct retrieval but does not fully assign the content boundary between the two files.
    - evidence refs: `plan.md#task-t02`, `plan.md#task-t03`, `todo.json:T02`, `todo.json:T03`
    - severity: `low`
    - mitigation options:
      - Option 1: State that `SKILL.md` contains compact anti-pattern routing and the support file contains the full catalog entries.
      - Option 2: State that the anti-pattern catalog lives entirely in `SKILL.md` and the support file only holds long-form examples.
    - recommended patch set: Clarify that `SKILL.md` routes and the support file holds the detailed catalog.
- Mitigation options and decisions:
  - `A02` -> yes
    - Selected set: Keep the initial implementation at two files by storing verification scenarios in `oop-planning-examples.md` and removing the third-file expansion from `T04`.
    - Rejected option: Explicitly expand to a three-file structure during review.
    - Rationale: Preserves the approved compact architecture and avoids late structure churn.
  - `A03` -> yes
    - Selected set: Remove `AC4` coverage from `T02` so recurring-domain example acceptance belongs only to `T03`.
    - Rejected option: Keep `AC4` on both tasks.
    - Rationale: Eliminates verification ambiguity and keeps acceptance ownership aligned with actual work.
  - `A04` -> yes
    - Selected set: Lock the support-file name and responsibility boundary explicitly in the narrative plan so it matches `todo.json`.
    - Rejected option: Revert `todo.json` to abstract placeholders.
    - Rationale: Concrete naming is acceptable once reviewed, and it reduces implementation drift.
  - `H01` -> yes
    - Selected set: Define a strict two-file information architecture where `SKILL.md` routes and `oop-planning-examples.md` holds detailed examples, anti-pattern catalog entries, and verification scenarios.
    - Rejected option: Permit a later decision on verification-file placement.
    - Rationale: Removes the highest-risk implementation divergence point before execution begins.
  - `H02` -> yes
    - Selected set: Tighten `AC2`, `AC6`, and `T04` so verification preparation explicitly means RED/GREEN pressure scenarios documented in `oop-planning-examples.md`.
    - Rejected option: Keep verification preparation abstract.
    - Rationale: Makes review and implementation expectations concrete.
  - `H03`
    - Decision: folded into nearby changes without separate approval.
    - Applied clarification: `SKILL.md` will contain compact anti-pattern routing, while `oop-planning-examples.md` will hold the detailed anti-pattern catalog entries.

## Implementation Review Notes - 2026-03-10

- Accepted findings:
  - `A03`: strengthen retrieval evidence by adding explicit anchors and a compact navigation index to `oop-planning-examples.md`, and update `SKILL.md` routing to point to named sections.
  - `H01`: treat the same navigation gap as a usability-risk fix and carry it as a focused iteration task rather than approving the current state for verification.
- Rejected/Deferred findings:
  - `H02` deferred to verification because the current RED/GREEN scenarios are sufficient for implementation review and can be pressure-hardened later if needed.
- Intended iteration scope:
  - support-file anchors
  - support-file navigation index
  - tighter `SKILL.md` section routing
