---
id: note:req:x2zgx4f
name: Reference integrity through a fork
kind: requirement
level: system
type: functional
status: current
---

Note shall ensure that a fork (materialization that re-homes an artifact to its own namespace under a new durable identifier, rather than a faithful frozen mirror that preserves it) severs no inbound reference silently.

Where materialization re-homes an artifact under a new identifier, references to the prior identifier shall be re-pointed to the new one, or every resulting break shall be surfaced.

## Rationale

This is the fork branch of materialization ([Materialization of inherited intent](materialization-of-inherited-intent.md){id=note:req:dssf1pp}).
The mirror-versus-fork distinction is fixed in [Cross-repository inheritance and materialization](../../decisions/cross-repository-inheritance.md){id=note:dec:h4w9k2t}: a faithful frozen mirror keeps the upstream identifier, so existing references resolve unchanged, whereas a fork re-homes the artifact to its own namespace under a new identifier.
That decision settles the mirror side but leaves the fork side, where the identifier changes, silent on the references that pointed at the old one; this requirement closes that gap.

It is the same reference-keeping obligation that promotion already carries ([Promotion of intent](promotion-of-intent.md){id=note:req:nc9k2w6}), here on the fork path rather than the promotion path: in both, an artifact is re-homed under a new identifier, so inbound references must be re-pointed or their breaks surfaced lest a relation break unseen.
Holding this across a corpus boundary is what keeps Note checkable from the files alone at the seam a cross-corpus consumer relies on.

The prior identifier is already recorded as provenance for every materialized artifact ([Materialization of inherited intent](materialization-of-inherited-intent.md){id=note:req:dssf1pp}); that record is what makes a re-pointed reference resolvable and a surfaced break diagnosable, so this requirement adds no new provenance obligation, only the reference-keeping one.

The mechanism (re-pointing a reference in place, reporting a break, or carrying the cross-boundary resolution path in a provenance map) is specification and tooling, not obligation.

## Relations

- derivedFrom: [Self-contained extraction of inherited intent](../stakeholder/self-contained-extraction.md){id=note:req:qq6eywy}
