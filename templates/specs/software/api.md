---
id: <namespace>:spec:<opaque>
name: <Name>
kind: specification
status: draft
authority:
  - contracts/<service>.openapi.yaml
---

This specification governs the HTTP request-response surface that <Service> exposes to its consumers.

## Authority

The governing contract is an OpenAPI 3.1 document (YAML syntax).
OpenAPI 3.1 aligns with JSON Schema Draft 2020-12, enabling direct `$ref` references to entity schemas defined elsewhere in the project.
The external document at the path listed in `authority` governs on any divergence between it and this file.
An implementation's conformance to the contract is a separate Verification; it is not established here.

## Relations

- satisfies: [<Requirement>](../../requirements/system/<requirement>.md){id=<namespace>:req:<opaque>}
