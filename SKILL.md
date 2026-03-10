---
name: planning-oop-and-solid
description: Use when an AI agent is deciding whether object-oriented design is appropriate, planning object boundaries, reviewing SOLID-driven designs, or spotting fake OOP such as anemic models, interface cargo culting, weak encapsulation, and classes used for their own sake.
---

# Planning OOP and SOLID

## Overview

Use this skill to make planning-time OOP decisions before implementation starts, then review drafted designs for fake OOP and weak object boundaries. The goal is not "use classes well"; the goal is "use object-oriented design only where it creates better behavior boundaries, policy control, and change isolation than simpler alternatives."

## When to Use

- The design might introduce entities, value objects, policies, services, or interfaces.
- A plan is drifting toward many classes but the ownership of behavior is unclear.
- A review needs to distinguish real encapsulation from class-shaped data containers.
- SOLID is being cited, but it is not clear whether it improves the design or just adds ceremony.
- The problem includes rich domain rules, lifecycle transitions, or policy enforcement and may justify object boundaries.

Do not use this skill for beginner syntax teaching or for forcing an object model onto straightforward data transformation problems.

## Entry Workflow

1. Decide whether this problem needs objects at all.
2. Identify where behavior, invariants, and policy ownership actually live.
3. Model only the boundaries that protect those rules.
4. Use SOLID to validate the design, not to invent abstractions.
5. Check the anti-pattern catalog before approving the plan.
6. Compare the object-oriented design against a simpler non-OOP alternative.

## Quick Triage

- Use OOP when:
  - domain rules must be enforced across lifecycle transitions
  - invariants must survive multiple operations over time
  - policies need explicit ownership and substitution boundaries
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

Planning questions:
- What can become invalid if callers bypass this boundary?
- Which rules need one owner instead of coordination across many helpers?
- If this object disappeared, would the remaining design become clearer?

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

## Composition and Boundary Heuristics

- Prefer composition when behaviors vary independently or are policy-driven.
- Prefer inheritance only when subtype semantics preserve the same contract and invariants.
- Use interfaces at boundaries where clients truly depend on a role, capability, or external integration seam.
- Keep external I/O and domain behavior separate so policy objects are testable without infrastructure noise.

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

## Review Red Flags

- Classes hold data while workflows elsewhere enforce the real rules.
- "Manager", "Coordinator", or "Processor" objects absorb unrelated behavior.
- Inheritance is used to share code rather than preserve semantic substitutability.
- Interface counts are growing faster than meaningful architectural boundaries.
- The design cannot explain why an object is better than a pure function plus data.

Review questions:
- Which object owns the most important invariant?
- Where does invalid state get stopped?
- Which abstraction disappears if we remove ceremony and keep only behavior?
- Which part of the design should remain non-OOP because it is simpler that way?

## Anti-Pattern Routing

- For class-shaped data containers, see `Anemic Models`.
- For abstraction without boundary value, see `Interface Cargo Culting`.
- For inheritance misuse, see `Reuse Through Inheritance`.
- For centralized orchestration, see `God Services and Managers`.
- For situations where no object model should be introduced, see `When Not to Use OOP`.

Detailed entries, real-world examples, and verification scenarios live in `oop-planning-examples.md`.

Recurring domains in that file:
- billing and subscriptions
- fulfillment and logistics
- identity and access management

## Common Mistakes

- Starting from nouns in the requirements and turning each into a class.
- Applying SOLID before identifying behavior ownership.
- Using repositories, managers, and services to carry all domain behavior while entities remain passive.
- Treating interface-per-class as architecture.
- Using inheritance to share implementation where composition or functions would be clearer.
