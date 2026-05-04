---
id: note:req:k4w7n9t
name: Single authoritative term-relation
kind: requirement
level: system
type: constraint
status: current
---

Each relationship between two terms shall have exactly one authoritative representation, authored on one end;
its inverse and any diagram of the term graph shall be derived from it, never authored separately.

## Rationale

This lifts the single-authoritative-representation rule from artifact relations ([Single authoritative representation per relationship](single-authoritative-relation.md){id=note:req:s5fh0e8}) to relationships between terms, for the same reason: a relationship stored in two places, a diagram and prose, drifts, and there is no authoritative side to adjudicate.

Authoring the relationship once and deriving the rest is the single-source-of-truth discipline applied to the term graph.

Which end stores the relationship, and how the derived views are produced, are specification.

## Relations

- derivedFrom: [Stated-once, typed, checkable term-relations](typed-term-relations.md){id=note:req:n8w4k6m}
- enacts: [Single Source of Truth](../../principles/single-source-of-truth.md){id=note:principle:8691937}
