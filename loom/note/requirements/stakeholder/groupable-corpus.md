---
id: note:req:h3k8w2m
name: A corpus navigable by group
kind: requirement
level: stakeholder
type: functional
status: current
---

A reader shall be able to find and traverse the artifacts of a kind as named groups, and an author shall be able to assign an artifact to a group, so that a corpus too large to scan as a flat list stays navigable.

Any view derived from a group, such as a diagram, shall come from the group's members rather than being maintained separately.

## Source

See the Source of [Navigate related intent as groups](../../needs/navigate-related-intent-by-group.md){id=note:need:w7k2n4p}.

## Rationale

Grouping is what keeps a large kind legible once each artifact is its own file: the cluster that a single file made visible has to be recoverable from the files themselves.

This obligation states that artifacts can be grouped, the groups traversed, and any view derived from a group kept single-sourced from its members, and leaves how a group is expressed and rendered to the system requirement and to specification.

## Relations

- addresses: [Navigate related intent as groups](../../needs/navigate-related-intent-by-group.md){id=note:need:w7k2n4p}
- decidedBy: [Grouping of artifacts by directory](../../decisions/artifact-grouping.md){id=note:dec:q8k3w2n}
