---
id: note:pain:9thn95r
name: A Trace Cannot Terminate Through a Cycle
kind: pain
persona:
  - "[Verifier](../../personas/verifier.md){id=note:persona:vk7m3qp}"
status: current
subkind: risk
---

A Verifier following a behavior back to the intent that asked for it can be sent around a loop that never reaches a root: an artifact transitively depends on itself through the authored relations, so the trace does not terminate and there is no well-defined answer to what governs what.

## Relations

- partOf: [Trust and drift visibility](../trust-intent-is-honored.md){id=note:need:46tkxcn}
- framedBy: [Trace Behavior to Intent](job-trace-behavior-to-intent.md){id=note:job:4pw4tqd}
