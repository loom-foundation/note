---
id: note:req:zscyz82
name: Independent versioning of method and tool
kind: requirement
level: system
type: constraint
status: current
---

Note and its reference tool shall version independently, so that the evolution of one does not force a version change on the other.

## Rationale

The forward-path guarantee must hold for an adopter who never runs Sett, so the method's evolution and migration cannot depend on the tool's release cadence, nor the reverse.

Because every operation Sett performs corresponds to one a person could perform unaided, the manual-operation parity the tool's own requirements fix, not-being-stranded never depends on the tool; independent versioning keeps that separation explicit.

Which version scheme each uses is specification.

## Relations

- derivedFrom: [Non-breaking evolution with a guaranteed forward path](../stakeholder/non-breaking-evolution.md){id=note:req:peh9g30}
