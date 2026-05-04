---
id: note:ver:p4ck8fq
name: Pack legality and the conformance floor
kind: verification
status: current
method: analysis
---

This verification confirms that a corpus's kind vocabulary and rigor are exactly what its manifest declares: every kind, field, and body section validates against the enabled packs and the declared profile alone, the default pack applies where nothing is configured, and raising a profile never invalidates what a lighter profile accepted.
The check is a static pass over the manifest and the committed files; it computes and reports findings only, and the verdict belongs to the Orchestrating Authority.

## Criteria

A pass requires that:

- every artifact's `kind` is declared by a pack the manifest enables, and no check is applied against a kind or a discipline outside the declared packs and profile, so the adopter's declared vocabulary is the vocabulary validated;
- a corpus that names no `packs` validates against the spine pack, the provided default, with no further configuration;
- each per-kind required field and required body section reported against an artifact traces to a row in an enabled pack's specification, never to an out-of-band list;
- conformance is evaluated against the declared profile, and re-running the pass at the next-lighter profile over the same files yields no new failures, the monotonicity that makes rigor safe to raise;
- the tier in force for any sampled artifact is derivable from the files alone, its enclosing scope resolved against the declared profiles, with no stored per-artifact rigor field found or needed.

A pass is zero failures across the corpus at its declared profile.

## Procedure

By analysis.
A static reader parses the manifest for `packs` and `profile`, defaulting to the spine pack where `packs` is absent, and loads the kind, field, and section tables from the enabled packs' specifications.
It then validates every artifact against exactly those tables at the declared profile, and validates the same files once more at each lighter profile, confirming the failure set never grows as the profile lightens.
The reader only reads; it executes nothing, so the check is reproducible by anyone with the repository.

## Evidence

A run produces a report: the enabled packs and profile read from the manifest, the artifacts checked, any kind, field, or section failure with the pack row it traces to, and the per-profile failure counts demonstrating monotonicity.
The report is kept with the run by the Orchestrating Authority; it is not stored in this artifact.

## Relations

- verifies: [Declarable kind packages](../requirements/system/declarable-kind-packages.md){id=note:req:ekfkzzt}
- verifies: [A provided default package](../requirements/system/provided-default-package.md){id=note:req:rfdr0e7}
- verifies: [Work in a declared, checkable kind vocabulary](../requirements/stakeholder/work-in-a-declared-kind-vocabulary.md){id=note:req:jkkpqbv}
- verifies: [Tiered conformance](../requirements/system/tiered-conformance.md){id=note:req:bth0rxp}
- verifies: [Progressive, right-sized adoption](../requirements/stakeholder/progressive-adoption.md){id=note:req:srzdd07}
- verifies: [Derivable tier in force](../requirements/system/derivable-tier-in-force.md){id=note:req:t3rfrc5}
