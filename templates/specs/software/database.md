---
id: <namespace>:spec:<opaque>
name: <Name>
kind: specification
status: draft
authority:
  - contracts/database/<database>.sql
---

This specification governs the target schema for the <database> database.

## Authority

The authority for this specification is the ANSI/PostgreSQL DDL file at `contracts/database/<database>.sql`.
That file is the executable source of truth: tables, columns, constraints, indexes, and foreign-key relationships are expressed there, not here.
On any divergence between this document and the DDL file, the DDL file governs.
Conformance of an implementation to this specification is a separate Verification artifact; it is not asserted here.

## Relations

- satisfies: [<Requirement>](../../requirements/system/<requirement>.md){id=<namespace>:req:<opaque>}
