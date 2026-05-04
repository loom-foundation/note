---
id: note:req:m520064
name: Implementation traceable to intent
kind: requirement
level: stakeholder
type: functional
status: current
---

An actor shall be able to determine, by inspection, which intent a unit of implementation claims to realize, with that claim recognizable and resolvable, so the chain from intent to verification reaches into the implementation that realizes it rather than stopping at the boundary of the corpus.

## Source

See the Source of [Trace intent into the implementation that realizes it](../../needs/trace-intent-into-implementation.md){id=note:need:jxhnj01}.

## Rationale

A unit of implementation, a module of source code or another implementation artifact, sits outside the corpus, yet it is where intent is finally realized and where divergence is felt.

When nothing connects that unit to the intent it claims to realize, the chain from intent to verification stops at the corpus boundary, an editor cannot see what governs a change, and the unit's reliance drifts unnoticed.

This requirement states the legibility property, that the claim be recognizable by inspection and resolvable to the artifact it names, and leaves how such a claim is written and recognized to specification.

## Relations

- addresses: [Trace intent into the implementation that realizes it](../../needs/trace-intent-into-implementation.md){id=note:need:jxhnj01}
- relieves: [No Specification-to-Code Link](../../needs/trace-intent-into-implementation/pain-nothing-connects-spec-to-code.md){id=note:pain:q7cwxns}
- relieves: [Implementation Reliance Goes Stale Invisibly](../../needs/trace-intent-into-implementation/pain-reliance-goes-stale-invisibly.md){id=note:pain:khqp1rv}
