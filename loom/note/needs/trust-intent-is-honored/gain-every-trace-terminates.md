---
id: note:gain:frzr64n
name: Every Trace Terminates
kind: gain
persona:
  - "[Verifier](../../personas/verifier.md){id=note:persona:vk7m3qp}"
status: current
expectation: expected
---

A Verifier following a behavior back to the intent that asked for it always reaches a root in finitely many steps, because no artifact transitively depends on itself; resolution is well-defined and the trace can be trusted to end.

## Relations

- partOf: [Trust and drift visibility](../trust-intent-is-honored.md){id=note:need:46tkxcn}
- framedBy: [Trace Behavior to Intent](job-trace-behavior-to-intent.md){id=note:job:4pw4tqd}
