---
id: note:req:r8h4g6t
name: Acyclic core relation graph
kind: requirement
level: system
type: constraint
status: current
---

Note shall ensure that the core relation graph is acyclic: no artifact transitively depends on itself through the authored relations, so every trace terminates and resolution is well-defined.

## Rationale

A trace follows the authored relations from a unit back to the intent that governs it. If those relations could form a cycle, an artifact could transitively depend on itself, a trace could fail to terminate, and there would be no well-defined answer to what governs what, defeating the legibility the chain from intent to verification is meant to provide ([Inspectable traceability](../stakeholder/inspectable-traceability.md){id=note:req:sg0npmv}).

Acyclicity has until now been stated only piecemeal: the substrate fixes that "The hierarchical edges are acyclic" ([The substrate](../../specifications/note/substrate.md){id=note:spec:tkhd63e}), the scope graph is a DAG, and the spine pack separately requires grounding to be acyclic so a cited Source does not derive from the artifact it grounds ([The spine pack](../../specifications/note/spine-pack.md){id=note:spec:6kjja5r}). This requirement consolidates those scattered statements into one findable, machine-checkable obligation on the relation graph as a whole.

Acyclicity is intrinsic to a graph whose edges resolve, not an agreed matter of style, so it is a Requirement and not a Convention. Which edges are in scope, and how a cycle is detected, are specification.

## Relations

- derivedFrom: [Inspectable traceability](../stakeholder/inspectable-traceability.md){id=note:req:sg0npmv}
