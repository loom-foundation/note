---
id: note:req:ph82t8q
name: Cross-repository reference resolution
kind: requirement
level: stakeholder
type: functional
status: current
---

When the corpus is split across more than one repository, a relation in one repository shall be able to reference an artifact in another by its stable identity, and scope inheritance shall resolve across repository boundaries, so the corpus stays one connected whole rather than fragmenting at the repository edge.

Where a referenced repository is not currently resolvable, the reference shall be reported as unresolved rather than invalid, and global properties shall be asserted only over the resolvable closure (see the validation-state term under `terms/`).

This is an opt-in discipline (see [Progressive, right-sized adoption](progressive-adoption.md){id=note:req:srzdd07}): single-repository projects never need it.

## Source

See the Source of [Operate one corpus across many repositories](../../needs/operate-corpus-across-repositories.md){id=note:need:03gs33j}.

## Rationale

Stable, location-independent identity is what makes a reference resolvable regardless of which repository holds the target.

Unlike extraction ([Self-contained extraction of inherited intent](self-contained-extraction.md){id=note:req:qq6eywy}), the repositories coexist and the reference stays live;
nothing is inlined or severed.

Distinguishing unresolved from invalid keeps validation honest: a well-formed link to a repository out of reach is not a broken link.

Locating the other repositories is an operational concern outside the method.

## Relations

- addresses: [Operate one corpus across many repositories](../../needs/operate-corpus-across-repositories.md){id=note:need:03gs33j}
- delivers: [A Cross-Repository Dependency Recorded as Intent](../../offerings/corpus-across-repositories/pr-cross-repository-dependency-as-intent.md){id=note:pr:vrejk49}
