---
id: note:req:s5fh0e8
name: Single authoritative representation per relationship
kind: requirement
level: system
type: constraint
status: current
---

Note shall ensure that each relationship between two artifacts has exactly one authoritative representation, so the two endpoints cannot disagree about whether the relationship holds.

The inverse direction shall be a derived view, never authored.

## Rationale

This applies the Single Source of Truth principle ([Single Source of Truth](../../principles/single-source-of-truth.md){id=note:principle:8691937}) to relations: two authoritative copies of one fact drift (established), and with many actors editing at machine speed the two halves of a relationship recorded on both sides drift apart with no authoritative side to adjudicate.

One authoritative representation removes that class of bug, and a graph with no self-contradicting edges is in turn a precondition for the relationships to be legible by inspection.

Which side stores it, and how the inverse is computed, are specification; the choice of storing side also leaves an upstream artifact undisturbed when a new dependent points at it, which preserves its staleness signal ([Detectable staleness](detectable-staleness.md){id=note:req:46xm59a}).

## Relations

- derivedFrom: [Inspectable traceability](../stakeholder/inspectable-traceability.md){id=note:req:sg0npmv}
- enacts: [Single Source of Truth](../../principles/single-source-of-truth.md){id=note:principle:8691937}
