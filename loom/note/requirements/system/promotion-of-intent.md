---
id: note:req:nc9k2w6
name: Promotion of intent
kind: requirement
level: system
type: functional
status: current
---

Note shall ensure an artifact can be re-homed from its scope to a broader scope so that the scopes beneath the new home inherit it through the cascade.

Where the new home is a different namespace, the artifact shall be given a new durable identifier that is unique within the target corpus, and its prior identifier shall be recorded as provenance.

References to the prior identifier shall be re-pointed to the new one, or every resulting break shall be surfaced.

## Rationale

Re-homing intent up the scope graph is the inverse of materialization ([Materialization of inherited intent](materialization-of-inherited-intent.md){id=note:req:dssf1pp}): materialization copies inherited intent down and severs the link, whereas promotion moves local intent up and the cascade then carries it back down to the scopes beneath.

Because the namespace denotes the owning scope and is part of the durable identifier, a promotion across namespaces necessarily changes identity; minting a fresh identifier unique in the target, rather than carrying the old one across, avoids any clash with the target corpus's identifiers and keeps each identifier owned by exactly one corpus, while the recorded prior identifier preserves the lineage.

Re-pointing references is the same reference-keeping obligation as any relocation, the reference-preserving rule Sett's own requirements carry on the tool side, except that here the target identifier is new rather than preserved.

The procedure for minting, re-pointing, and recomputing the cascade is specification and tooling.

## Relations

- derivedFrom: [Intent promotable to a broader scope](../stakeholder/promotable-intent.md){id=note:req:mx4w8k3}
