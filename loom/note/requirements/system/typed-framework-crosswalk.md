---
id: note:req:p2ry9tv
name: Typed framework crosswalk
kind: requirement
level: system
type: functional
status: current
---

Note shall provide, in an opt-in package, typed relations by which a requirement or convention records its correspondence to an external control, distinguishing equivalence, a subset relationship, and a partial overlap, each authored once on the obligation and resolvable to the control it names, so the correspondence is checkable from the files and stated only on the obligation that bears it.

## Rationale

A crosswalk is a relationship between an obligation and an external control, so it is carried by the same authored-once, typed-relation machinery every other relationship uses, not by a free-text note that cannot be checked.

The three relationship kinds (equivalence, subset, overlap) are the established distinctions of cross-framework mapping, reused rather than coined.

Holding the relations in an opt-in package keeps a corpus that answers to no external framework from carrying machinery it does not use.

The external control the relation names is a read-only artifact addressable by durable id, referenced where it lives or captured locally by the existing cross-repository and capture machinery, so this requirement adds the relations, not a second way to reference an artifact, and the relation is authored on the obligation and never on the control.
A subset relationship runs from the obligation's coverage to the control, so a corpus can record that an obligation covers part of what a control demands; the precise orientation and the resolvable form of each relation are specification.

The graph the relations form is acyclic by construction.
Because the control is read-only and authors nothing in return, the crosswalk runs one way, from a writable obligation to a control that is a sink with no outgoing crosswalk edge, so no cycle can close and the obligation is always the authoring end with no tie-breaker needed.
`subsetOf`, with its derived inverse `supersetOf`, is a hierarchical edge and is held acyclic by the same rule that governs the method's other hierarchical edges, the precaution that matters should a later many-to-many crosswalk ever chain such edges; `equivalentTo` and `intersectsWith` are symmetric, and like the other associative relations they are not subject to the acyclic rule.

## Relations

- derivedFrom: [Intent mappable to external frameworks](../stakeholder/mappable-to-external-frameworks.md){id=note:req:ddh4kfx}
- enacts: [Single Source of Truth](../../principles/single-source-of-truth.md){id=note:principle:8691937}
- decidedBy: [The compliance crosswalk pack](../../decisions/compliance-crosswalk-pack.md){id=note:dec:ve053yf}
- delivers: [A Mapping That Outlives Each Framework Version](../../offerings/framework-crosswalk/gc-mapping-outlives-its-framework-version.md){id=note:gc:dab3yx7}
- delivers: [Mapping Authored Beside the Obligation](../../offerings/framework-crosswalk/pr-mapping-authored-beside-the-obligation.md){id=note:pr:84wcxrm}
- delivers: [Coverage You Can Show](../../offerings/framework-crosswalk/pr-coverage-you-can-show.md){id=note:pr:gc0y6pr}
- delivers: [A Framework Imported Once](../../offerings/framework-crosswalk/pr-framework-imported-once-as-intent.md){id=note:pr:aq7cvq3}
