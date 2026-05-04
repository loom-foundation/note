---
id: note:req:yb1xez2
name: Typed, checkable relations
kind: requirement
level: system
type: functional
status: current
---

Note shall ensure that relations between artifacts are typed, each carrying a source-kind and target-kind signature, so that the validity of a relationship can be checked mechanically and a traceability graph can be computed from the files alone.

## Rationale

A link is only useful for traceability if its meaning is constrained enough to validate; an untyped "related to" link cannot surface a type error or support a computable graph.

The relation vocabulary and its signatures are specification.

## Relations

- derivedFrom: [Inspectable traceability](../stakeholder/inspectable-traceability.md){id=note:req:sg0npmv}
