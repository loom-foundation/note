---
id: note:dec:q8k3w2n
name: Grouping of artifacts by directory
kind: decision
status: current
decided: 2026-06-03T01:50:32Z
---

Artifacts of a kind are grouped by their placement in sub-directories of the kind.
The directory is the single source of truth for the grouping; there is no mirroring frontmatter field.
Sett derives grouped navigation and any per-group view, such as a group's relation diagram, from the directory structure and the artifacts' relations.
Grouping does not affect identity, is proportionate to a kind's size, and is distinct from scope.

## Context

Each artifact is one file ([Artifacts are Markdown with YAML frontmatter](artifact-file-format.md){id=note:dec:pxnjmcd}), and as the corpus grows a kind accumulates many files.

Terminology already organized its terms into clusters within a single file; once each term is its own file, that cluster view is gone unless grouping is expressed another way.

The same will hold for any kind that grows large.

The question is where the grouping lives: in the directory, in the frontmatter, or in both.

## Decision

- **The directory is the grouping.**
  A kind's artifacts are grouped by placing them in sub-directories of the kind; the sub-directory under the kind names the group.
  The directory is the single source of truth for the grouping.
- **No mirroring frontmatter field.**
  A grouping stated in both the directory and a `group` field is the same fact authored twice: it drifts, and it taxes every move with a field update.
  One source avoids both, which is the single-source-of-truth principle applied to grouping.
- **Identity is unaffected.**
  The identifier in frontmatter is location-independent ([Requirement levels](requirement-levels-and-identity.md){id=note:dec:nc2yrf4}), so moving an artifact to another group changes its group, by intent, and never breaks a reference.
  This is why the directory can be authoritative for grouping without making location load-bearing for identity.
- **Sett derives the views.**
  Grouped navigation and a group's diagram are computed from the directory structure and the artifacts' relations, never hand-authored ([Terminology with typed term-relations](terminology-and-term-relations.md){id=note:dec:s9k4w7n} already fixes that diagrams are derived).
- **Proportionate.**
  A small kind stays flat and uses no groups; sub-directories appear when a flat listing becomes hard to scan.
- **Distinct from scope.**
  Scope is a multi-parent graph a directory tree cannot fully express, so scope is authoritative in frontmatter and the directory only mirrors it ([Adopter corpus placement](corpus-placement.md){id=note:dec:q2v7nk3}); a group is a single-membership partition the tree expresses exactly, so for grouping the directory is authoritative.
  Matching each axis to its structure is what keeps the two consistent rather than contradictory.
- **Single membership.**
  This mechanism places an artifact in one group.
  If membership in several groups is ever genuinely needed, it is a separate, opt-in addition, not a field imposed on every artifact.

## Forces and trade-offs

- One source of truth, the directory, removes the move-time upkeep and the drift a mirrored field would carry, at the cost that an artifact lives in exactly one group.
  Accepted, because single membership is the actual pattern (the terminology clusters), and multi-group membership can be added later if it proves real.
- Making the directory authoritative for grouping while scope stays frontmatter-authoritative is a deliberate split, not an inconsistency: it matches a partition to a tree and a graph to frontmatter.

## Alternatives considered

- **A `group` frontmatter field mirroring the directory.**
  Rejected: it states one fact twice, drifts, and taxes every move with an update, for a multi-membership benefit the corpus does not currently need.
- **A `group` field as the sole source, directory left flat.**
  Rejected: it is invisible to a reader browsing the files with no tool, the very legibility grouping is meant to restore; the sub-directory is the natural human grouping.
- **No grouping; a flat listing per kind.**
  Rejected: it is the legibility loss this decision exists to prevent once a kind grows large.

## Driven by

- groundedIn: [Requirement levels](requirement-levels-and-identity.md){id=note:dec:nc2yrf4}
- groundedIn: [Adopter corpus placement](corpus-placement.md){id=note:dec:q2v7nk3}
- groundedIn: [Terminology with typed term-relations](terminology-and-term-relations.md){id=note:dec:s9k4w7n}
