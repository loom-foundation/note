---
id: note:term:6g971kr
name: Reference Closure
kind: term
status: current
---

The smallest set of artifacts that contains a selection and everything an actor needs to read it correctly and act on it faithfully, so the set is self-contained: the selection plus, transitively, every artifact drawn in by either of two pulls, stopping at the corpus boundary.

An artifact is drawn in by an **edge pull** when a load-bearing relation verb leads to it, the holder being incomplete without its target; a reference-only relation cites its target without pulling it.
An artifact is drawn in by a **structural pull** when it is constitutive of an in-closure artifact's meaning or validity with no edge to declare: the terms, conventions, and principles in force at that artifact's scope, which carry no per-artifact edge naming what they govern and so are pulled by their standing at the scope rather than by a verb.
A closure satisfying only the edge pull can be formally complete, with no dangling reference, yet leave an actor unable to interpret what they received; the structural pull is what keeps it interpretable.
A pull whose target lives in another corpus is an external reference, recorded as a boundary of the closure rather than followed into the upstream.

## Inclusion test

Given a selection, would an actor be left unable to read or faithfully act on an in-closure artifact if this artifact were left out, either because a reference would point at something not present or because a term, convention, or principle the artifact depends on would be missing?
If the artifact is reached from the selection by a pull edge within the corpus, or is a term, convention, or principle in force at an in-closure artifact's scope, it is in the Reference Closure; an artifact reached only by a reference-only relation, or living in another corpus, is not.

## Relations

- *contrasts with* [Materialization](materialization.md){id=note:term:3yted77} (a closure is the set of intent a selection leans on; materialization is the act of freezing such a set locally and severing its live links, one thing a consumer may do with a closure)
- *relates to* [Cascade](cascade.md){id=note:term:5b6cbtr} (selecting a scope expands to the effective intent the cascade resolves there, and the closure is then taken of that set; the cascade composes intent across scopes, the closure gathers what a selection depends on)

## Origin

General English (Oxford: "closure" as "the fact of bringing something to an end" and, in the set-theoretic sense, the smallest superset of a set that satisfies a stated property).

The lineage is the mathematical sense of closure under an operation, the least set containing a seed and closed under given rules; narrowed here to closure under both the corpus's load-bearing relations and the terms, conventions, and principles in force at an artifact's scope, bounded at the corpus edge, so an extracted selection carries everything it depends on and everything needed to interpret it, and nothing it merely cites.
