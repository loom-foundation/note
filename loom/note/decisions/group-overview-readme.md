---
id: note:dec:rd6w3k2
name: Group overviews as co-located README files
kind: decision
status: current
decided: 2026-06-10T05:50:33Z
---

A group, which is a kind's sub-directory ([Grouping of artifacts by directory](artifact-grouping.md){id=note:dec:q8k3w2n}), may carry an overview in a co-located `README.md` in that directory.

The overview is plain prose, not a first-class artifact.

The same rule applies to every grouped kind and at the kind level, so `terms/validation/README.md`, `terms/README.md`, and `requirements/stakeholder/README.md` are all instances of one convention.

## Context

Grouping is by sub-directory, and the directory is the single source of truth for the grouping.

Group-level prose, the overview that introduces a group and any context common to its members, had no natural home in that model.

A central register is a second copy of the directory structure that must be re-synced whenever a group is added, renamed, or removed.
That is the single-source-of-truth cost ([Single Source of Truth](../principles/single-source-of-truth.md){id=note:principle:8691937}) and a drift vector in a reviewed, agent-edited corpus.

## Decision

- A group may carry a co-located **`README.md`** holding its overview prose.
  Having one is optional, by earned substance ([Earned Substance](../principles/earned-substance.md){id=note:principle:yecemfe}): a group authors one only when it has something to say.
  Where group-level prose does exist, though, it lives only here, with the group, never in a central register: co-location is the rule, and only the file's existence is the choice.
- The name is `README.md`, chosen because a Git host renders a directory's `README.md` inline above the file listing when the directory is opened, so the overview and the group's members appear together with no tool.
  No other name earns this: a group-named file or `index.md` or `overview.md` does not auto-render, and `README.md` reads the same to a human and to an agent.
- The overview is **plain prose, not a first-class artifact**: it carries no durable id and no `kind`.
  A group is a directory, not an entity that anything needs, verifies, or references by id, so minting a group kind would be ceremony that buys nothing.
  Where a group's shared context is genuinely load-bearing and referenced, it is a real artifact, a Term or a Context, that the README links to, rather than the README promoted to a kind.
  Symmetrically, a first-class artifact is never demoted to a group `README.md`: a need or offering profile keeps its own descriptively-named file beside its facet directory ([Atomic facets](atomic-facets.md){id=note:dec:af3k9w2}), so the README introduces a directory but never stands in for a member of it.
- The convention is **one rule for every kind and at every level**: a group's README at `terms/<group>/README.md` or `requirements/stakeholder/README.md`, and a kind's README at `terms/README.md`, are the same mechanism applied to a sub-directory.
- The **directory listing is the index**; no hand-maintained list of members is kept.
  A flat, clickable index, if wanted, is a derived view the tool generates, never authored, the rendered-navigable-presentation obligation on the Sett side.

## Forces and trade-offs

The README convention removes a central register that duplicated the directory set, so the grouping keeps one source of truth and group prose travels in the same pull request as the members it describes.

The cost is the loss of a single scrollable page that showed the whole vocabulary at once, and the cross-group narrative such a page carried.
That narrative is rare and belongs at the kind level (`terms/README.md`), not repeated in every group, so the loss is small and is paid once.

Choosing `README.md` over a semantic name trades a little self-description for the directory auto-render, which is the decisive ergonomic win and is free.

## Alternatives considered

A central register file.
Rejected: it is a second source of truth for the group set and drifts against the directories, the cost the grouping decision already pays to the single-source-of-truth principle.

A group-named file (`lifecycle.md` inside `lifecycle/`) or `index.md` / `overview.md`.
Rejected: none of these auto-render when a directory is opened, a group-named file duplicates the directory name and couples a rename to two places, and `index.md` is a static-site-generator convention a plain Git host does not treat specially.

A first-class group artifact (`kind: group`, with a durable id).
Rejected against earned substance: nothing needs, verifies, or references a group as an entity, so the ceremony buys nothing; load-bearing group context becomes a Term or a Context instead.

## Driven by

- groundedIn: [Grouping of artifacts by directory](artifact-grouping.md){id=note:dec:q8k3w2n}
- groundedIn: [Navigate related intent as groups](../needs/navigate-related-intent-by-group.md){id=note:need:w7k2n4p}
- groundedIn: [A corpus navigable by group](../requirements/stakeholder/groupable-corpus.md){id=note:req:h3k8w2m}
- groundedIn: [Single Source of Truth](../principles/single-source-of-truth.md){id=note:principle:8691937}
- groundedIn: [Earned Substance](../principles/earned-substance.md){id=note:principle:yecemfe}
