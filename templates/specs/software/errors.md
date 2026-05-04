---
id: <namespace>:spec:<opaque>
name: <Name>
kind: specification
status: draft
authority:
  - contracts/errors/problem-detail.schema.yaml
---

This specification defines the error response contract for <system or service name>.

## Authority

The authoritative contract is the JSON Schema (RFC 9457, IETF) at `contracts/errors/problem-detail.schema.yaml`.
That schema governs on any divergence from this document.
An implementation's conformance to the contract is a separate Verification, not an assertion of this specification.

## Relations

- satisfies: [<Requirement>](../../requirements/system/<requirement>.md){id=<namespace>:req:<opaque>}
