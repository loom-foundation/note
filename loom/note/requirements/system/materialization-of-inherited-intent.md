---
id: note:req:dssf1pp
name: Materialization of inherited intent
kind: requirement
level: system
type: functional
status: current
---

Note shall ensure the effective intent a scope inherited can be captured as standalone artifacts within that scope, so the scope resolves without continued access to the repositories it inherited from.

Each materialized artifact shall carry provenance: the source it was captured from and the version at which it was captured.
This provenance is the authoritative record of the capture; no separate index of materialized sources is required.

Materializing severs the live link.

## Rationale

Materialization handles the spin-out moment, when the outer repositories are no longer present ([Self-contained extraction of inherited intent](../stakeholder/self-contained-extraction.md){id=note:req:qq6eywy}).

It is the one deliberate exception to effective intent never being stored separately ([Effective-intent resolution](effective-intent-resolution.md){id=note:req:5xnajsm}): it inlines and severs, producing a local copy that will, by design, diverge from the former parent.

This is what distinguishes materialization from a cross-repository reference ([Cross-repository resolution](cross-repository-resolution.md){id=note:req:dxxvabc}): a reference keeps a live link to intent that still lives elsewhere, whereas materialization captures that intent locally and breaks the link.

Recording provenance is what keeps that intended decoupling distinguishable from drift.

Where the captured copies are placed and how they are named is decided in [Cross-repository inheritance and materialization](../../decisions/cross-repository-inheritance.md){id=note:dec:h4w9k2t}.

The authority to extract a scope is operational, outside Note.

## Relations

- derivedFrom: [Self-contained extraction of inherited intent](../stakeholder/self-contained-extraction.md){id=note:req:qq6eywy}
