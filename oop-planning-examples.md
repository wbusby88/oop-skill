# OOP Planning Examples

## Purpose

This file holds the detailed recurring-domain examples, anti-pattern catalog, and verification scenarios referenced by `SKILL.md`.

## Navigation Index

- [Billing and subscriptions](#billing-subscriptions)
- [Fulfillment and logistics](#fulfillment-logistics)
- [Identity and access management](#identity-access-management)
- [Anti-pattern catalog](#anti-pattern-catalog)
- [When not to use OOP](#when-not-to-use-oop)
- [Verification scenarios](#verification-scenarios)

<a id="billing-subscriptions"></a>
## Billing and Subscriptions

### Good Fit: Subscription Lifecycle With Policy Ownership

Problem:
- A subscription can move through trial, active, grace, suspended, canceled, and expired states.
- Discount eligibility depends on contract terms, payment failures, recovery windows, and regulatory rules.
- Cancellation rules differ for monthly and annual plans and may preserve access through the billing period.

Good design shape:
- `Subscription` owns state transitions such as activate, suspend, recover, cancel, and expire.
- `BillingPolicy` or `RenewalPolicy` captures pricing and retry rules that vary by product or market.
- `InvoiceAttempt` or `PaymentRecoveryPolicy` handles retry windows without leaking those rules into controllers.

Why OOP helps:
- The lifecycle has protected transitions and invalid state combinations.
- Policies change independently from storage and transport layers.
- Callers should request business outcomes rather than mutate status fields.

Bad contrast:
- `SubscriptionRecord` is a passive data class with public fields.
- `SubscriptionManager`, `BillingManager`, and `RetryCoordinator` decide every valid transition externally.
- The real rules live in if/else trees spread across service classes and background jobs.

Why that is fake OOP:
- The "object model" names nouns but does not own behavior.
- Status integrity depends on external orchestration order.
- Adding a new recovery rule means editing multiple managers instead of extending policy seams.

### When Not to Use OOP Here

If the task is only "generate next invoice previews for 20,000 subscriptions," a pipeline of query -> transform -> summarize is usually clearer than introducing preview objects with trivial methods.

<a id="fulfillment-logistics"></a>
## Fulfillment and Logistics

### Good Fit: Shipment Aggregate With Reservation Rules

Problem:
- Orders reserve stock from multiple locations.
- A shipment can be packed, partially shipped, rerouted, held, or returned.
- Dangerous goods, temperature constraints, and carrier cutoffs affect which transitions are valid.

Good design shape:
- `Shipment` owns packing and shipping transitions and rejects impossible combinations.
- `ReservationPolicy` decides whether inventory can be split, backordered, or rerouted.
- `CarrierSelectionPolicy` evaluates constraints without turning carrier choices into inheritance trees.

Why OOP helps:
- Shipment state changes carry invariants that must remain coherent across operations.
- Policies vary by region, warehouse, and item class.
- The model benefits from encapsulating lifecycle rules instead of exposing mutable status maps.

Bad contrast:
- `Shipment`, `Warehouse`, and `Package` classes are mostly getters/setters.
- `FulfillmentOrchestrator` performs all validation and mutates each object step by step.
- `ExpressShipment extends Shipment` and `ColdChainShipment extends Shipment` exist mostly to share branching logic.

Why that is fake OOP:
- Inheritance is doing code reuse instead of semantic modeling.
- The orchestrator knows the full process graph while the objects know almost nothing.
- Every new shipping edge case increases central complexity rather than localizing policy.

### When Not to Use OOP Here

If the work is "optimize pick-path ordering for a warehouse wave," a data-processing or optimization pipeline may be better than an object graph. The result is usually a computed plan, not a long-lived behavioral aggregate.

<a id="identity-access-management"></a>
## Identity and Access Management

### Good Fit: Access Grant Evaluation With Policy Objects

Problem:
- Access depends on role assignments, temporary grants, tenant boundaries, resource sensitivity, and break-glass exceptions.
- Revocation and approval flows must preserve auditability.
- Different resource types may share policy concepts but not identical rules.

Good design shape:
- `AccessGrant` or `Assignment` owns lifecycle transitions such as approve, revoke, expire, and renew.
- `AuthorizationPolicy` evaluates whether a requested action is permitted under current grants and constraints.
- `BreakGlassPolicy` is composed in as an exceptional capability rather than implemented as a subclass hack.

Why OOP helps:
- Access rules combine lifecycle ownership with policy substitution.
- Strong encapsulation protects audit-sensitive transitions.
- Policy objects make variability explicit without scattering authorization logic.

Bad contrast:
- Every resource gets its own `XPermissionService`.
- Interfaces exist for every service even though only one implementation exists and no boundary is being protected.
- `AdminAccess extends AccessGrant` overrides checks in ways that weaken the base contract.

Why that is fake OOP:
- The design uses interfaces and subclasses as ceremony rather than true seams.
- Substitution becomes unsafe because some grants bypass invariants.
- The authorization model is harder to reason about than a focused policy layer plus explicit grant objects.

### When Not to Use OOP Here

If the task is "expand a permission matrix export" or "summarize access audit records," a query + transformation flow is usually preferable to building export-specific classes.

<a id="anti-pattern-catalog"></a>
## Anti-Pattern Catalog

<a id="anemic-models"></a>
### Anemic Models

Signals:
- entities expose fields and trivial setters
- workflows or services enforce the real rules
- invalid transitions can happen unless callers remember the right sequence

Prevention:
- move lifecycle rules into the owning object or policy
- expose intent methods instead of raw mutation
- make invalid state transitions impossible or explicit

<a id="interface-cargo-culting"></a>
### Interface Cargo Culting

Signals:
- nearly every class has a same-named interface
- interfaces have one implementation and no boundary value
- abstractions exist before clients or substitution needs exist

Prevention:
- define interfaces for client-facing roles, external boundaries, or meaningful alternate implementations
- delete local interfaces that only mirror concrete classes

<a id="reuse-through-inheritance"></a>
### Reuse Through Inheritance

Signals:
- subclasses exist to share code, flags, or partial behavior
- subtype rules are weaker or different from the base contract
- branching logic checks subclass type in callers

Prevention:
- replace reuse hierarchies with composition, policies, or explicit strategy objects
- keep inheritance only when semantic substitutability is real

<a id="god-services-and-managers"></a>
### God Services and Managers

Signals:
- `Manager`, `Coordinator`, `Processor`, or `Orchestrator` objects accumulate domain decisions
- entities remain passive
- new rules are added to central flow code rather than behavior owners

Prevention:
- split orchestration from domain policy
- move invariant enforcement closer to the state it protects
- use orchestration only to sequence already-owned behaviors

<a id="class-wrappers-over-data"></a>
### Class Wrappers Over Data

Signals:
- classes mainly rename DTOs or records
- methods just expose or format fields
- there is no owned lifecycle or behavioral boundary

Prevention:
- keep plain data plain when behavior does not need ownership
- upgrade to objects only when invariants or policy control justify it

<a id="when-not-to-use-oop"></a>
## When Not to Use OOP

Prefer simpler designs when:
- the core job is transformation, aggregation, export, or routing
- rule ownership is shallow and stateless
- the proposed object graph adds names without protection
- behavior reads more clearly as policies plus pure functions

Comparison rule:
- if the non-OOP design is clearer and does not sacrifice invariant protection, keep it.

<a id="verification-scenarios"></a>
## Verification Scenarios

### RED: Expected Failure Without This Skill

Scenario 1: Subscription redesign under abstraction pressure
- Prompt shape: "Design the billing domain for subscriptions, retries, discounts, and cancellation. Use SOLID and make it extensible."
- Expected failure without this skill:
  - creates many interfaces before identifying boundaries
  - produces passive entities plus manager/service classes
  - uses SOLID vocabulary to justify structure instead of behavior ownership

Scenario 2: Fulfillment model under reuse pressure
- Prompt shape: "Model shipments, warehouses, temperature-sensitive packages, and expedited flow with classes."
- Expected failure without this skill:
  - introduces inheritance for shipping variants
  - centralizes decisions in an orchestrator
  - does not compare against a simpler policy-plus-data alternative

Scenario 3: Authorization planning under architecture pressure
- Prompt shape: "Design an enterprise authorization system with best-practice interfaces and extensibility."
- Expected failure without this skill:
  - creates interface-per-service without clear client boundaries
  - weakens contracts through subtype-specific bypass logic
  - fails to identify which transitions require strong encapsulation and audit ownership

### GREEN: Expected Behavior With This Skill

For the same scenarios, the agent should:
- decide first whether objects are justified at all
- identify the invariant-owning lifecycle boundary before naming classes
- use policies and composition where variation is real
- reject interfaces or inheritance that do not protect a boundary
- include at least one explicit "when not to use OOP here" comparison
- name the likely anti-pattern if the design starts drifting toward ceremony

### Review Assertions

- The answer explains why an object exists, not just what noun it represents.
- The answer identifies where invalid state or policy violation is prevented.
- SOLID is used to critique the design, not to force additional abstractions.
- Anti-patterns such as anemic models, god services, or interface cargo culting are called out explicitly when relevant.
- The answer retains simple non-OOP structures where they are better.

### Rationalizations To Watch For

- "We might need multiple implementations later" used to justify interfaces now.
- "This class could grow later" used to justify a weak object boundary now.
- "Inheritance keeps things DRY" used without proving substitutability.
- "Everything should be an object in a proper architecture" used as a premise.
