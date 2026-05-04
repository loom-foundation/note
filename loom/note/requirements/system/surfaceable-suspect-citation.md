---
id: note:req:v3k7m1n
name: Surfaceable suspect-citation signals
kind: requirement
level: system
type: functional
status: current
---

Note shall ensure that structural signals that a citation may not hold, computable from the files alone, are surfaceable for review, without asserting whether the citing unit actually honors the cited intent.

## Rationale

A citation can resolve and be fresh and still be false: a unit copied elsewhere carries a citation that was never realized in the copy, or a refactor leaves a citation stapled to the wrong block.

Some symptoms of this are visible in the files themselves, without running anything: for example the same id cited from units that share no other relationship, or a citation that no longer sits beside the kind of unit the cited obligation governs.

These are structural signals: properties of the citation graph and the files that carry it, computable by inspection, the same substrate text-staleness and lifecycle-staleness are computed from.

Surfacing such a signal says only that a citation is worth a human's second look, not that the code is wrong.

Whether the citing unit actually honors the obligation is divergence: it requires executing or analyzing behavior, which Note does not perform, and it stays routed to the Orchestrating Authority ([Detectable divergence](detectable-divergence.md){id=note:req:vttexty}).

This requirement is bounded strictly to the file-computable structural signal and the surfacing of it for review; it makes no behavioral claim and confers no judgment, consistent with the System computing and reporting a derived view and deciding nothing ([Representation, not enforcement](representation-not-enforcement.md){id=note:req:agncpcc}).

Which structural signals are computed, and how each is recognized, are specification.

## Relations

- derivedFrom: [Detectable drift](../stakeholder/detectable-drift.md){id=note:req:d6m4q7z}
