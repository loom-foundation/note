---
id: <namespace>:spec:<opaque>
name: <Name>
kind: specification
status: draft
authority:
  - contracts/events/<channel>.asyncapi.yaml
---

This specification covers the asynchronous event contract for <channel>.

## Authority

The governing contract is an AsyncAPI 3.x document at `contracts/events/<channel>.asyncapi.yaml`.
That file defines channels, operations, message schemas, and protocol bindings; on any divergence between this document and the contract file, the contract file governs.
Conformance of a specific implementation to that contract is a separate Verification, not part of this Specification.

## Relations

- satisfies: [<Requirement>](../../requirements/system/<requirement>.md){id=<namespace>:req:<opaque>}
