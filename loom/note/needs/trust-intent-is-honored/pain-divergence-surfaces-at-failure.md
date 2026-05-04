---
id: note:pain:1e0h3d0
name: Divergence Surfaces at Failure
kind: pain
persona:
  - "[Verifier](../../personas/verifier.md){id=note:persona:vk7m3qp}"
status: current
subkind: risk
---

A Verifier has no signal that behavior has drifted from its specification until the running system fails in production, by which point the cost to trace and reverse the drift is many times higher than catching it at the review that should have stopped it.

## Relations

- partOf: [Trust and drift visibility](../trust-intent-is-honored.md){id=note:need:46tkxcn}
- framedBy: [Learn When Dependency Changed](job-learn-when-dependency-changed.md){id=note:job:rzm745f}
- framedBy: [Trace Behavior to Intent](job-trace-behavior-to-intent.md){id=note:job:4pw4tqd}
