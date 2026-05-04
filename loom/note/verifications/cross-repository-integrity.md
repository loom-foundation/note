---
id: note:ver:xr3p0mh
name: Cross-repository integrity
kind: verification
status: current
method: analysis
---

This verification confirms the constructs that let a corpus span, leave, or seed repositories: every id carries its declared namespace, a reference to an absent repository degrades to unresolved rather than invalid, a materialized copy of inherited intent carries full provenance, an extracted closure stands alone, and a fork or promotion leaves no reference behind that silently dangles.
The checks are standing rules over the files: in a corpus that has not yet spanned repositories, forked, or promoted, the affected criteria pass vacuously and are reported as unexercised rather than as confirmed in use.
The check computes and reports findings only, and the verdict belongs to the Orchestrating Authority.

## Criteria

A pass requires that:

- the manifest declares the corpus namespace, every artifact id carries it, and no two corpora in reach declare the same one, so an id names its corpus wherever the file travels;
- every reference whose namespace is not locally resolvable is classified unresolved, never invalid, and no check fails an artifact for the absence of another repository;
- every materialized block of inherited intent carries complete provenance (source id, source scope, the commit or version materialized at, and the date), so a copy is auditable against its origin;
- the reference closure of any extraction sample is self-contained: each member's references resolve inside the extracted set or are marked as boundary references, with no silent dangling edge;
- after a fork or a promotion, every reference touching the moved or re-homed intent either resolves to the new location or is surfaced as needing re-pointing, with none left silently broken.

A pass is zero failures over the exercised constructs, with the unexercised ones enumerated as vacuous.

## Procedure

By analysis.
A static reader checks the manifest's namespace against every artifact id; classifies every reference as resolved, boundary, or unresolved and confirms no unresolved reference is treated as a failure elsewhere; validates the provenance fields of every materialized block; extracts the closure of a sampled selection into a bare directory and re-runs resolution inside it; and, where history records a fork or promotion, re-resolves every reference that named the moved intent.
The reader only reads; it executes nothing, so the check is reproducible by anyone with the repository.

## Evidence

A run produces a report: the namespace census, the reference classification counts, each materialized block's provenance, the extraction resolution result, and the exercised-versus-vacuous status of each criterion.
The report is kept with the run by the Orchestrating Authority; it is not stored in this artifact.

## Relations

- verifies: [A corpus may span repositories](../requirements/stakeholder/corpus-spans-repositories.md){id=note:req:e3bvftj}
- verifies: [Cross-repository reference resolution](../requirements/stakeholder/cross-repo-references.md){id=note:req:ph82t8q}
- verifies: [Declared namespace identity](../requirements/stakeholder/declared-namespace-identity.md){id=note:req:78hqr3n}
- verifies: [Cross-repository resolution](../requirements/system/cross-repository-resolution.md){id=note:req:dxxvabc}
- verifies: [Materialization of inherited intent](../requirements/system/materialization-of-inherited-intent.md){id=note:req:dssf1pp}
- verifies: [Self-contained extraction of inherited intent](../requirements/stakeholder/self-contained-extraction.md){id=note:req:qq6eywy}
- verifies: [Promotion of intent](../requirements/system/promotion-of-intent.md){id=note:req:nc9k2w6}
- verifies: [Reference integrity through a fork](../requirements/system/reference-integrity-through-fork.md){id=note:req:x2zgx4f}
- verifies: [Intent promotable to a broader scope](../requirements/stakeholder/promotable-intent.md){id=note:req:mx4w8k3}
