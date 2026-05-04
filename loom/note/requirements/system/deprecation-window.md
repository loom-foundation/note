---
id: note:req:af33evm
name: Deprecation window before removal
kind: requirement
level: system
type: constraint
status: current
---

A feature shall be marked deprecated, with warning, for at least one minor cycle before it may be removed in a major version.

## Rationale

A forward path is only real if adopters have notice.

A deprecation window gives a corpus time to adapt while both the old and the new behavior are still available, so removal at a major step is the end of a signaled process rather than a surprise.

The length is stated as an obligation; how a deprecation is surfaced is specification.

## Relations

- derivedFrom: [Non-breaking evolution with a guaranteed forward path](../stakeholder/non-breaking-evolution.md){id=note:req:peh9g30}
