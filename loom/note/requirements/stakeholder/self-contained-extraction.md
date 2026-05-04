---
id: note:req:qq6eywy
name: Self-contained extraction of inherited intent
kind: requirement
level: stakeholder
type: functional
status: current
---

When a scope is extracted into its own repository, the intent it inherited shall be able to travel with it and resolve standalone, without continued access to the repositories it inherited from.
The extracted intent shall carry provenance, what it was derived from and at what version, so its lineage remains auditable after the link to the source is severed.
Where extraction re-homes an artifact under a new identity rather than preserving it, every inbound reference to the prior identity shall be kept whole or every resulting break surfaced, so the move severs no relation silently.

This is an opt-in discipline (see [Progressive, right-sized adoption](progressive-adoption.md){id=note:req:srzdd07}): single-repository projects never need it.

## Source

See the Source of [Inherited intent on fork](../../needs/carry-inherited-intent-on-fork.md){id=note:need:29519ms}.

## Rationale

At a spin-out the source repositories may become unreachable, yet the extracted unit must still carry the obligations it inherited.

Extraction therefore differs from a cross-repository reference ([Cross-repository reference resolution](cross-repo-references.md){id=note:req:ph82t8q}): a reference keeps a live link to intent that still lives elsewhere, whereas extraction inlines the effective intent and severs the link.

Recording provenance is what keeps that deliberate decoupling distinguishable from drift.

Locating other repositories, and the authority to extract a scope, are operational concerns outside the method.

## Relations

- addresses: [Inherited intent on fork](../../needs/carry-inherited-intent-on-fork.md){id=note:need:29519ms}
