---
id: <namespace>:spec:<opaque>
name: <Name>
kind: specification
status: draft
authority:
  - contracts/schemas/<entity>.schema.yaml
---

This specification governs the canonical entity schemas for <system or bounded context>.

## Authority

The governing standard is JSON Schema 2020-12, authored in YAML syntax (one file per entity at `contracts/schemas/<entity>.schema.yaml`).
Where this document and any contract file diverge, the contract file governs.
An implementation's conformance to these schemas is a separate Verification and is not asserted here.

## Relations

- satisfies: [<Requirement>](../../requirements/system/<requirement>.md){id=<namespace>:req:<opaque>}
