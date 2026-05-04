---
id: note:req:rfdr0e7
name: A provided default package
kind: requirement
level: system
type: functional
status: current
---

Note shall provide a default kind package, so that a corpus that declares no package is nonetheless a well-defined corpus with a known kind set.

## Rationale

The package model requires at least one package to be active for a corpus to have any legal kinds.
If no default package is provided, a corpus that omits a package declaration would have no legal kinds at all, making the floor of adoption a configuration step rather than a zero-config starting point.
Providing a default removes that friction: an adopter can start immediately without declaring a package, and the kind set they encounter is the method's considered recommendation for what most efforts earn.

## Relations

- derivedFrom: [Work in a declared, checkable kind vocabulary](../stakeholder/work-in-a-declared-kind-vocabulary.md){id=note:req:jkkpqbv}
- decidedBy: [The default spine pack](../../decisions/spine-pack.md){id=note:dec:4tzn3av}
