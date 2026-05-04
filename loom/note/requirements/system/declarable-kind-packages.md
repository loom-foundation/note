---
id: note:req:ekfkzzt
name: Declarable kind packages
kind: requirement
level: system
type: functional
status: current
---

Note shall ensure a corpus declares the kind packages it enables, and that each package declares its kinds, their fields, their body sections, and their endpoint-typed relations, so that kind legality, field legality, and link legality are checkable from the files plus the declared packages alone.

## Rationale

This is the generic mechanism that replaces a fixed per-kind enumeration in the method itself.
Rather than the method supplying a closed list of sanctioned kinds, a corpus opts into one or more named packages; the package declares exactly what is valid within it.
A checker needs only the corpus files and the declared packages to determine whether an artifact is well-formed: no out-of-band kind registry, no method-level enumeration of all possible kinds.

The obligation is intentionally solution-free: it does not specify how a package is represented, how a corpus manifest references packages, or what the built-in packages contain.
Those are the method's design choices, settled by the deciding decision.

## Relations

- derivedFrom: [Work in a declared, checkable kind vocabulary](../stakeholder/work-in-a-declared-kind-vocabulary.md){id=note:req:jkkpqbv}
- decidedBy: [Kind-agnostic substrate and kind packages](../../decisions/substrate-and-kind-packages.md){id=note:dec:w4awceq}
- delivers: [Your Words Mapped Once, Not Relearned](../../offerings/adopt-in-your-vocabulary/pr-map-your-words-once.md){id=note:pr:hpg313f}
