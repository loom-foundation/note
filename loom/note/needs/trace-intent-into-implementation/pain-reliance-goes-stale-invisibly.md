---
id: note:pain:khqp1rv
name: Implementation Reliance Goes Stale Invisibly
kind: pain
persona:
  - "[Implementer](../../personas/implementer.md){id=note:persona:s4v9hn2}"
status: current
subkind: risk
---

When the intent an implementation realizes changes, the implementation's reliance on it goes stale with nothing to make the staleness visible: no link ties the implementation to the artifact, so no check can notice the divergence the way drift among the intent artifacts is already noticed.

## Relations

- partOf: [Trace intent into the implementation that realizes it](../trace-intent-into-implementation.md){id=note:need:jxhnj01}
- framedBy: [Find the Governing Obligations Before Changing a Unit](job-find-governing-obligations.md){id=note:job:awfc6g9}
