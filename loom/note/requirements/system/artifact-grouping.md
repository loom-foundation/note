---
id: note:req:n6w4k9t
name: Grouping of artifacts
kind: requirement
level: system
type: functional
status: current
---

Note shall provide for the artifacts of a kind to be grouped by their placement in sub-directories of the kind, the directory being the single source of truth for the grouping, so that artifacts can be organized for navigation and for views derived from a group.

Where a group has overview prose or context common to its members, that overview shall live with the group as part of its single source of truth, not in a separate central register; whether a group has such an overview at all is proportionate to the group.

The grouping shall not affect an artifact's identity or the resolution of references to it, and whether a kind uses grouping shall be proportionate to its size.

## Rationale

A sub-directory is the natural way a reader groups files, and a single source of truth for the grouping avoids the drift and the upkeep a second, mirrored statement of it would carry.

Identity stays in the frontmatter identifier and is location-independent ([Requirement levels](../../decisions/requirement-levels-and-identity.md){id=note:dec:nc2yrf4}), so moving an artifact to another group changes its group, by intent, and never breaks a reference.

Grouping is a navigation axis distinct from the scope axis: scope is a multi-parent graph a directory tree cannot fully express, whereas a group is a partition the tree expresses exactly, which is why the directory can be authoritative here.

The directory convention and the derivation of group views are specification; the choices behind them are recorded in [Grouping of artifacts by directory](../../decisions/artifact-grouping.md){id=note:dec:q8k3w2n}, and the co-located group overview in [Group overviews as co-located README files](../../decisions/group-overview-readme.md){id=note:dec:rd6w3k2}.

## Relations

- derivedFrom: [A corpus navigable by group](../stakeholder/groupable-corpus.md){id=note:req:h3k8w2m}
- decidedBy: [Grouping of artifacts by directory](../../decisions/artifact-grouping.md){id=note:dec:q8k3w2n}
- decidedBy: [Group overviews as co-located README files](../../decisions/group-overview-readme.md){id=note:dec:rd6w3k2}
