---
id: note:req:233g9mc
name: Legible lifecycle
kind: requirement
level: system
type: functional
status: current
---

Note shall ensure an artifact's authority and maturity state is legible, and that changes to that state are constrained to a well-formed set of transitions.

Note shall define which transitions are well-formed; it shall not decide who is permitted to make one.

## Rationale

A reader's trust in an artifact depends on knowing whether it is provisional or authoritative, and on which state changes are meaningful at all.

Separating the definition of legal transitions (Note's) from the authority to perform them (the Orchestrating Authority's) keeps the boundary intact ([Representation, not enforcement](representation-not-enforcement.md){id=note:req:agncpcc}).

Lifecycle authority is a discipline adopted progressively ([Progressive, right-sized adoption](../stakeholder/progressive-adoption.md){id=note:req:srzdd07}).

The state set and the transition table are specification.

## Relations

- derivedFrom: [Legible artifact maturity](../stakeholder/legible-maturity.md){id=note:req:b3h47g8}
