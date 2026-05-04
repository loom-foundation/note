---
id: note:req:bth0rxp
name: Tiered conformance
kind: requirement
level: system
type: constraint
status: current
---

Note shall ensure a minimal core determines whether a file is a valid artifact at all, and that every other discipline is opt-in.

A project, or a scope within it, shall declare which disciplines it adopts, and conformance shall be evaluated against that declared profile rather than the maximal rule set.

Adoption shall be monotonic: adopting more discipline shall never invalidate an artifact that was valid under less, shall never change an artifact's identity, and shall never break an existing relation; it may require adding fields or enriching content.

## Rationale

This is the mechanism that makes right-sizing real; it realizes [Progressive, right-sized adoption](../stakeholder/progressive-adoption.md){id=note:req:srzdd07} and the Proportionality principle.

The monotonicity clause is what lets a project raise its rigor by backfilling rather than migrating.

It is scoped deliberately to identity and linkage, since enriching content (for example, adopting independent validation of a specification that was previously plain prose) can cost authoring effort without breaking anything: the no-migration promise covers identity, links, and the file envelope, not content richness.

The named tiers and the core fieldset are specification.

## Relations

- derivedFrom: [Progressive, right-sized adoption](../stakeholder/progressive-adoption.md){id=note:req:srzdd07}
- derivedFrom: [Durable, portable intent](../stakeholder/durable-portable-intent.md){id=note:req:93kczqj}
- enacts: [Proportionality](../../principles/proportionality.md){id=note:principle:es0vhzn}
- delivers: [Full Rigor Demanded Only Where Stakes Are High](../../offerings/ceremony-that-scales/pr-full-rigor-where-stakes-are-high.md){id=note:pr:mm61hmy}
- delivers: [Rigor Rises Without Reworking What You Wrote](../../offerings/ceremony-that-scales/pr-rigor-rises-without-rework.md){id=note:pr:2t85jyy}
- delivers: [Ceremony That Scales With Stakes](../../offerings/start-where-you-are/pr-ceremony-that-scales.md){id=note:pr:hjdrmy9}
