---
id: note:req:n8w4k6m
name: Stated-once, typed, checkable term-relations
kind: requirement
level: system
type: functional
status: current
---

Note shall ensure that each load-bearing term has one canonical definition, that a relationship between two terms is typed from a declared, closed set and stated once, that a term used in its defined sense within another artifact is identifiable and its definition resolvable, and that the whole is computable and checkable from the files alone.

## Rationale

Shared, related term meaning needs more than prose definitions: the relationships between terms must be typed and checkable like the relationships between artifacts, a term reference inside a need or a requirement must resolve to its definition, and none of it may depend on a second copy.

Stating each relationship once, with the inverse and any diagram derived rather than authored, is what keeps the term graph free of the drift a hand-maintained diagram-plus-prose invites.

The relation vocabulary, the storage, the reference grammar, and the derivation are specification.

## Relations

- derivedFrom: [Unambiguous, related term meaning](../stakeholder/unambiguous-related-term-meaning.md){id=note:req:c5k9w2h}
- derivedFrom: [Checkable well-formedness and identity](checkable-well-formedness.md){id=note:req:sp8g0my}
