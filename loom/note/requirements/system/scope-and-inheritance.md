---
id: note:req:96smmcv
name: Scope and inheritance
kind: requirement
level: system
type: functional
status: current
---

Note shall ensure intent can be expressed at the scope where it first becomes load-bearing and inherited by the scopes beneath it, that a scope can inherit from more than one source, and that the set of sources a scope inherits from is acyclic so that resolution terminates.

## Rationale

Cross-cutting concerns, such as a privacy concern owned in one branch applying to products in another (see the illustrative situations of [State a shared obligation once](../../needs/state-obligation-once.md){id=note:need:257yf29}), require more than one source of inheritance, so the inheritance structure is a directed acyclic graph rather than a single linear chain.

Acyclicity is what guarantees resolution ends.

Inheritance runs along the scope axis: an inner scope inherits the intent in force at the outer scopes that contain it.

This axis is distinct from the derivedFrom axis, along which a requirement refines the intent it derives from within the requirements layer.

Keeping the two separate matters because they answer different questions: the scope axis says where an obligation applies, while the derivedFrom axis says what an obligation is grounded in.

A single artifact participates in both at once.

How scope itself is expressed, for instance whether by directory location, is specification.

## Relations

- derivedFrom: [Hierarchically scoped intent](../stakeholder/hierarchically-scoped-intent.md){id=note:req:6n6jdyq}
- delivers: [One Home for Cross-Cutting Concerns](../../offerings/scoped-intent/pr-one-home-for-cross-cutting.md){id=note:pr:w32p8a0}
