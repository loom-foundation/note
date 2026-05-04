---
id: note:req:e3bvftj
name: A corpus may span repositories
kind: requirement
level: stakeholder
type: functional
status: current
---

Note shall let one corpus, under a single namespace, span several repositories declared as the member roots of a root manifest, so that intent kept as sibling repositories functions as one corpus rather than many, with one trace graph, one coverage closure, and one identity space across the members.

## Rationale

A system is often built as several repositories for reasons of ownership, team boundary, or release cadence, yet its intent is one body; binding the members into one corpus lets a reference, a cascade, and a coverage check cross the repository edge instead of dead-ending at it.
The root manifest names the members so a tool, or a reader, can assemble the whole from one place; the members are located by relative path in a co-located workspace, or by URL when they are not, the same way cross-repository references resolve.

## Relations

- relieves: [Whole-Organization Picture Assembled by Hand](../../needs/operate-corpus-across-repositories/pain-no-unified-view.md){id=note:pain:v7rfr1a}
- creates: [One System Reads as One Corpus](../../needs/operate-corpus-across-repositories/gain-one-system-one-corpus.md){id=note:gain:hztec2a}
- decidedBy: [The multi-root corpus](../../decisions/multi-root-corpus.md){id=note:dec:0n14gqx}
