---
id: note:req:agncpcc
name: Representation, not enforcement
kind: requirement
level: system
type: constraint
status: current
---

Note shall confine itself to representing intent, design, rationale, relationships, lifecycle state, and scope, and to defining checkable rules over them.

Note shall not assume responsibility for actor identity, role assignment, access control, dispatch, building, independent verification, or the authority to permit any transition or deviation.

The full boundary is fixed in `context.md`.

## Rationale

Because authoring is open to any actor with basic reading and writing ([Universal participation](../stakeholder/universal-participation.md){id=note:req:j4kecn7}), nothing in a file can bind who edits it; a safety property the files cannot enforce would be advisory dressed as structural.

Identity and permission must therefore live in the Orchestrating Authority that holds them.

Stating this as a requirement keeps a future reader or agent from mistaking Note for the enforcement layer.

## Relations

- derivedFrom: [Universal participation](../stakeholder/universal-participation.md){id=note:req:j4kecn7}
- enacts: [Compute and Report](../../principles/compute-and-report.md){id=note:principle:6e7f28k}
