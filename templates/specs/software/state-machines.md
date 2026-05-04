---
id: <namespace>:spec:<opaque>
name: <Name>
kind: specification
status: draft
authority:
  - contracts/state-machines/<entity>.yaml
---

This specification governs the lifecycle of `<Entity>`: its valid states, permitted transitions, guards, and side effects.

## Authority

The authoritative contract is the YAML state machine definition at `contracts/state-machines/<entity>.yaml`, versioned with the project.
Where this document and the YAML diverge, the YAML governs.
Conformance of an implementation to this specification is a separate Verification and is not established here.

## Relations

- satisfies: [<Requirement>](../../requirements/system/<requirement>.md){id=<namespace>:req:<opaque>}
