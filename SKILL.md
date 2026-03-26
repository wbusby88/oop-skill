---
name: object-oriented-programming
description: Use when an AI agent is deciding whether object-oriented design is appropriate, planning object boundaries, reviewing SOLID-driven designs, or spotting fake OOP such as anemic models, interface cargo culting, weak encapsulation, and classes used for their own sake.
---

# Planning OOP and SOLID

## Overview

Use this skill to make planning-time OOP decisions before implementation starts, then review drafted designs for fake OOP and weak object boundaries. The goal is not "use classes well"; the goal is "use object-oriented design only where it creates better behavior boundaries, policy control, and change isolation than simpler alternatives." Once OOP is justified, default to real objects that own state, invariants, and behavior rather than helper-heavy procedural flows.

## When to Use

- The design might introduce entities, value objects, policies, services, or interfaces.
- A plan is drifting toward many classes but the ownership of behavior is unclear.
- A review needs to distinguish real encapsulation from class-shaped data containers.
- SOLID is being cited, but it is not clear whether it improves the design or just adds ceremony.
- The problem includes rich domain rules, lifecycle transitions, or policy enforcement and may justify object boundaries.
- The user explicitly asks for an OOP design, object model, class design, aggregate, entity, or value object structure.

Do not use this skill for beginner syntax teaching or for forcing an object model onto straightforward data transformation problems.

## Entry Workflow

1. If the user explicitly wants OOP or the domain has lifecycle/invariant pressure, identify the candidate objects first.
2. Identify where behavior, invariants, and policy ownership actually live.
3. Choose the smallest set of value objects, entities, aggregates, and policies that can protect those rules.
4. Define how each important object is created, what state it hides, and which intent methods own transitions.
5. Use SOLID to validate the design, not to invent abstractions.
6. Check the anti-pattern catalog before approving the plan.
7. Compare the object-oriented design against a simpler non-OOP alternative.

## Quick Triage

- Use OOP when:
  - domain rules must be enforced across lifecycle transitions
  - invariants must survive multiple operations over time
  - policies need explicit ownership and substitution boundaries
  - the user explicitly asks for an OOP/object design and the domain is richer than a pure data pipeline
- When OOP is chosen:
  - prefer a domain object with explicit construction over helper modules that mutate shared records
  - default to `new Thing(...)` when there is one normal creation path; use named/static factories only when they express a genuinely different creation meaning or handle explicit rehydration/parsing boundaries
  - keep important state behind methods or policies instead of exporting writable fields
  - let callers request outcomes from the object instead of orchestrating each mutation step themselves
- Avoid OOP when:
  - the work is mostly stateless transformation or aggregation
  - behavior lives naturally in a pipeline, rule table, or pure function layer
  - proposed classes do not own meaningful state transitions or rule enforcement

## Section Map

- OOP decision heuristics
- Behavior and encapsulation heuristics
- Composition and boundary heuristics
- SOLID validation lens
- Review red flags
- Anti-pattern routing
- Reference examples and verification scenarios in `oop-planning-examples.md`

## OOP Decision Heuristics

- Prefer objects when domain behavior must guard invariants over time.
- Prefer simpler data-oriented or functional structures when the design mostly transforms records without owned lifecycle rules.
- Reject classes that only rename nouns from the requirements without gaining control over behavior.
- Reject interfaces created only to satisfy a pattern rather than a real substitution or boundary need.
- If a mutable record would otherwise be passed through multiple helper functions, strongly consider turning that boundary into an object.

Planning questions:
- What can become invalid if callers bypass this boundary?
- Which rules need one owner instead of coordination across many helpers?
- If this object disappeared, would the remaining design become clearer?

## Object Ownership Defaults

- When the prompt asks for an OOP system, assume the primary domain concepts should become behavior-owning objects unless the problem is obviously a pure transformation task.
- Start with value objects for immutable concepts with validation, then introduce entities where identity and lifecycle matter over time.
- Use an aggregate or root object when multiple changes must preserve one transactionally meaningful invariant.
- Put domain rules in the object that can actually prevent invalid state, not in a helper file that merely remembers to run first.
- Keep helper functions subordinate to objects: helpers may calculate, parse, format, or map data, but they should not own the core lifecycle of a domain concept.

Planning questions:
- Which concept should be instantiated as an object because callers must not edit its internals directly?
- Which concept is only data and should remain a record, DTO, or value object instead of growing ad hoc methods?
- Which object is the natural owner of each rule that currently appears in a helper or manager?

## Construction and Encapsulation Defaults

- Prefer explicit construction such as `new Subscription(args)` or a named factory when an object must start life valid.
- Default to a constructor when the object has one normal way to become valid; do not replace ordinary construction with `fromX`, `create`, or `build` methods that merely forward arguments.
- Use a named/static factory when it communicates a distinct creation semantics such as rehydration from persistence, parsing external input, or selecting among meaningfully different valid states.
- Keep nullable or optional input handling outside the core object when possible; `fromOptional`, `maybeCreate`, or `fromNullable` patterns often hide upstream control flow rather than modeling a domain concept.
- Constructors or factories should establish required invariants up front rather than relying on follow-up helper calls.
- Expose intent methods such as `cancel()`, `suspend()`, `approve()`, or `retryPayment()` instead of writable status fields.
- Hide mutable internals behind private state, validated accessors, or value objects when the language supports it.
- If persistence requires rehydration, keep it explicit with a separate factory or repository path rather than weakening normal construction rules.
- If a top-level helper needs several fields the object already owns, consider making it a private method or composed policy on that object instead of passing its own state back out.

Planning questions:
- How is the object guaranteed to be valid immediately after construction?
- Is this named factory expressing real domain meaning, or is it avoiding a constructor without gaining clarity?
- Which fields should never be directly mutable by callers?
- Which transitions deserve explicit methods instead of public data mutation?

## Behavior and Encapsulation Heuristics

- Put rules where they can be enforced, not where they are convenient to call.
- A real object should hide invalid state transitions behind methods or policies.
- If external orchestration scripts know more about valid state than the object itself, encapsulation is weak.
- If methods only proxy getters, setters, or repository calls, the design is likely anemic.

Strong signals:
- the object can reject invalid transitions itself
- related rules cluster around the same lifecycle
- callers ask for outcomes, not permission to mutate internals

Weak signals:
- the class mostly exposes mutable fields
- services outside the object assemble the real business policy
- every rule needs multiple collaborators because no object owns it

## Helpers, Services, and Object Boundaries

- Keep pure helper functions for stateless calculations, formatting, parsing, and record-to-record transformations.
- If a helper function mutates shared domain state, depends on call order, or knows the lifecycle better than the object, it probably wants to become a method or policy object.
- If a helper function consumes the same config or internal fields that an object already encapsulates, it is often an encapsulation leak rather than a useful helper.
- Use a domain service only when the behavior does not naturally belong to one object, value object, or policy seam.
- Use application services to coordinate already-owned behavior, not to become the real home of business rules.
- Reject `XManager` or `XHelpers` modules that are effectively the true domain model while the "objects" stay passive.

## Composition and Boundary Heuristics

- Prefer composition when behaviors vary independently or are policy-driven.
- Prefer inheritance only when subtype semantics preserve the same contract and invariants.
- Use interfaces at boundaries where clients truly depend on a role, capability, or external integration seam.
- Keep external I/O and domain behavior separate so policy objects are testable without infrastructure noise.
- Prefer policy objects, strategies, or composed collaborators over inheritance when variation is real but lifecycle ownership stays the same.

Planning questions:
- Is this variability semantic or just code reuse?
- Does this interface protect a boundary, or only satisfy a convention?
- Would a policy object or pure function be clearer than another service class?

## SOLID Validation Lens

- Single Responsibility: check for one reason to change at the behavior boundary, not one method per class.
- Open/Closed: prefer extension through policy seams and composition, not inheritance trees prepared for hypothetical change.
- Liskov Substitution: reject hierarchies where substituting a subtype weakens invariants or changes contract meaning.
- Interface Segregation: define interfaces around concrete client needs, not around a belief that every class deserves one.
- Dependency Inversion: invert dependencies around policy boundaries or external systems, not around internal trivia.

Use SOLID after the design exists in rough form. If SOLID is the reason a class or interface exists, the design is probably backwards.

## Language-Specific Defaults

- JavaScript/TypeScript:
  - For rich domain behavior, prefer `class` plus explicit construction and methods over exporting a mutable object and a pile of helper functions.
  - Use `#private` when you need real runtime privacy in JavaScript or TypeScript, not just naming convention.
  - Keep top-level functions or plain objects for truly stateless utilities, not for owning domain lifecycle.
- Python:
  - Use a regular class when the object owns lifecycle transitions or invariant-enforcing behavior.
  - Use `@dataclass` or a frozen value object style for record-like concepts with lightweight validation and little or no owned lifecycle.
- Java/C#:
  - Default to private state, constructor initialization, and validated methods or properties.
  - Avoid public mutable fields for domain state; expose intent and validation through methods/accessors instead.

## Review Red Flags

- Classes hold data while workflows elsewhere enforce the real rules.
- "Manager", "Coordinator", or "Processor" objects absorb unrelated behavior.
- Inheritance is used to share code rather than preserve semantic substitutability.
- Interface counts are growing faster than meaningful architectural boundaries.
- The design cannot explain why an object is better than a pure function plus data.
- A helper module or service knows the valid transition order better than the object that supposedly owns the domain.
- A static `fromX` or `create` method is used as a constructor alias even though there is only one ordinary creation path.
- Top-level helper functions take the object's own config or state as parameters because the object never internalized that behavior.
- The answer claims to be OOP but never explains construction, hidden state, or the methods that protect invariants.

Review questions:
- Which object owns the most important invariant?
- Where does invalid state get stopped?
- Which abstraction disappears if we remove ceremony and keep only behavior?
- Which part of the design should remain non-OOP because it is simpler that way?

## Anti-Pattern Routing

- For class-shaped data containers, see `Anemic Models` in `oop-planning-examples.md#anemic-models`.
- For abstraction without boundary value, see `Interface Cargo Culting` in `oop-planning-examples.md#interface-cargo-culting`.
- For inheritance misuse, see `Reuse Through Inheritance` in `oop-planning-examples.md#reuse-through-inheritance`.
- For centralized orchestration, see `God Services and Managers` in `oop-planning-examples.md#god-services-and-managers`.
- For helper-first procedural designs disguised as OOP, see `Helper Modules Owning Domain State` in `oop-planning-examples.md#helper-modules-owning-domain-state`.
- For situations where no object model should be introduced, see `When Not to Use OOP` in `oop-planning-examples.md#when-not-to-use-oop`.

Detailed entries, real-world examples, and verification scenarios live in `oop-planning-examples.md`, with direct sections for:
- `#billing-subscriptions`
- `#fulfillment-logistics`
- `#identity-access-management`
- `#anti-pattern-catalog`
- `#verification-scenarios`

Recurring domains in that file:
- billing and subscriptions
- fulfillment and logistics
- identity and access management

Verification preparation:
- Run the RED/GREEN pressure scenarios in `oop-planning-examples.md` before claiming the skill is complete.
- Treat rationalizations such as interface-per-class or inheritance-for-reuse as explicit failure signals.

## Common Mistakes

- Starting from nouns in the requirements and turning each into a class.
- Applying SOLID before identifying behavior ownership.
- Using repositories, managers, and services to carry all domain behavior while entities remain passive.
- Treating interface-per-class as architecture.
- Using inheritance to share implementation where composition or functions would be clearer.
- Exporting mutable records and relying on helper functions to preserve invariants after the fact.
- Replacing straightforward constructors with `fromX` factories that add no semantic distinction and usually signal misplaced control flow.
- Leaving behavior in file-level helpers even though the helper only needs state the object already owns.
- Saying "object-oriented" while omitting construction rules, hidden state, and intent-revealing methods.
