---
id: note:req:64eknb1
name: Visible, attributable deviation
kind: requirement
level: system
type: constraint
status: current
---

Note shall ensure that every replacement or removal of inherited intent is visible at the scope where it occurs, carries a rationale, and is attributable, so the deviation can be reviewed.

Note shall not decide who is permitted to deviate.

## Rationale

Dropping an inherited obligation is high-stakes and must be reviewable, not a silent local edit.

The three properties earn their place separately: visibility at the deviating scope means a reviewer does not have to diff against the parent to discover that an obligation was dropped; the rationale answers why; attribution answers who, so the deviation can be taken up with the right person.

Together they make a dropped obligation legible rather than buried.

Making the deviation legible is Note's; routing it to an approver is the Orchestrating Authority's, which keeps the boundary intact ([Representation, not enforcement](representation-not-enforcement.md){id=note:req:agncpcc}).

## Relations

- derivedFrom: [Hierarchically scoped intent](../stakeholder/hierarchically-scoped-intent.md){id=note:req:6n6jdyq}
- delivers: [Deviation Visible and Attributed](../../offerings/scoped-intent/pr-deviation-visible-and-attributed.md){id=note:pr:kx1gvdq}
