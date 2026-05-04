---
id: <namespace>:spec:<opaque>
name: <Name>
kind: specification
status: draft
authority:
  - contracts/config/<service>.schema.yaml
---

This specification governs the configuration surface of <service>: every key, its type, default, valid values, sensitivity classification, and source mapping.

## Authority

The authoritative contract is a JSON Schema 2020-12 document at `contracts/config/<service>.schema.yaml`
(YAML syntax, Draft 2020-12, with Loom `x-sensitive` and `x-source` extension keywords).
Where this specification and the contract diverge, the contract governs.
A markdown table derived mechanically from the schema may accompany the contract as a readable view; it is not a second authority.
Conformance of a specific implementation to the contract is a separate Verification, not part of this specification.

## Relations

- satisfies: [<Requirement>](../../requirements/system/<requirement>.md){id=<namespace>:req:<opaque>}
