---
id: note:req:dxxvabc
name: Cross-repository resolution
kind: requirement
level: system
type: functional
status: current
---

Note shall ensure a relation can reference an artifact in another repository by its stable identity, and that scope inheritance resolves across repository boundaries, so the traceability graph and the cascade stay whole when the corpus is distributed.

A cross-repository reference on which a global property depends, one feeding an inheritance, a cascade, or a coverage closure, shall resolve at an explicitly identified version of the referenced repository, so that dependency is reproducible and does not shift unless the version is deliberately changed.
A cross-repository reference made only to navigate or to record a relationship need not be version-pinned: it may resolve live against the referenced repository as currently checked out, the same convenience an in-corpus relative path gives, with the durable id the authoritative anchor from which a staled path is recovered.

Where a referenced repository is not currently resolvable, the reference shall be reported as unresolved, distinct from invalid, and global properties (acyclicity, coverage, effective intent) shall be asserted only over the resolvable closure.

## Rationale

Stable, location-independent identity ([Stable, location-independent identity](stable-identity.md){id=note:req:sfmkwmm}) is what makes a reference resolvable regardless of which repository holds the target.

The repositories coexist and the reference stays live, distinct from materialization, which severs the link.

Reporting unresolved rather than invalid keeps validation honest: a well-formed link to a repository out of reach is not a broken link.

How the version is pinned and recorded is decided in [Cross-repository inheritance and materialization](../../decisions/cross-repository-inheritance.md){id=note:dec:h4w9k2t}.

Locating other repositories is operational, outside Note: a repository may be reached by a remote URL or by a local filesystem path, so cross-repository resolution requires no online service.

In a co-located workspace of sibling repositories, a navigation reference resolves from the files alone, exactly as an in-corpus relative path does; version pinning is the discipline reproducible inheritance adds on top, not a cost every cross-repository link pays.

## Relations

- derivedFrom: [Cross-repository reference resolution](../stakeholder/cross-repo-references.md){id=note:req:ph82t8q}
- delivers: [Your Own Cadence Without Cutting the Link](../../offerings/corpus-across-repositories/gc-own-cadence-without-cutting-the-link.md){id=note:gc:e9rrqgn}
- delivers: [A Reference That Resolves Across the Edge](../../offerings/corpus-across-repositories/pr-reference-that-resolves-across-the-edge.md){id=note:pr:vyhxzb7}
