---
id: note:req:2kvyew2
name: Defined migration across majors
kind: requirement
level: system
type: constraint
status: current
---

A new major version shall ship with a defined migration from the previous major, and shall be able to read the previous major's corpus well enough to drive that migration.

A major release that leaves a conformant corpus with no forward path shall not be permitted.

## Rationale

A break confined to a major step ([Within-major backward compatibility](within-major-compatibility.md){id=note:req:c62shkd}) is only safe if that step has a defined way across.

Requiring the migration to exist, and the new major to read the old corpus well enough to drive it, is what turns "no version strands a corpus" into an obligation the method must meet before it releases.

The method defines the migration; the tool executes it, per Sett's own migration-execution requirement.

How a migration is expressed and run is specification.

## Relations

- derivedFrom: [Non-breaking evolution with a guaranteed forward path](../stakeholder/non-breaking-evolution.md){id=note:req:peh9g30}
