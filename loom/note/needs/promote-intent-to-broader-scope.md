---
id: note:need:hq7k4w2
name: Promote intent to a broader scope
kind: need
persona:
  - "[Systems Engineer](../personas/systems-engineer.md){id=note:persona:25fdjrx}"
  - "[Organization or Platform Owner](../personas/organization-owner.md){id=note:persona:6ek4j8b}"
  - "[Reviewer or Auditor](../personas/reviewer-auditor.md){id=note:persona:9jz2a3w}"
status: current
validation: inferred
---

When intent first authored in one unit turns out to apply across many, a Systems Engineer or an Organization or Platform Owner wants to move it to the unit that should own it, so that every team beneath that unit picks it up once, rather than leaving it misplaced or copying it into each team that needs it.

## Source

The ordinary refactoring pattern of pulling a definition up to where it is shared, applied to intent on the scope graph, and the single-source-of-truth cost of copying intent up rather than moving it.

The inverse direction, freezing inherited intent down into a scope, is already captured as materialization.

Reasoned from the scope model rather than observed in the field.

External to this corpus and not derived from it.
