---
id: note:req:vttexty
name: Detectable divergence
kind: requirement
level: system
type: functional
status: current
---

Note shall ensure it is detectable that an implementation no longer honors the contract a specification describes, as a signal distinct from staleness.

The running of any such check shall be routed to the Orchestrating Authority, since it requires execution Note does not perform.

## Rationale

A change in referenced text does not prove behavior diverged, and conflating the two leaves divergence undetected.

Note represents the relationship and the obligation to check; whether and how the check is run belongs to the Orchestrating Authority, consistent with representation-not-enforcement ([Representation, not enforcement](representation-not-enforcement.md){id=note:req:agncpcc}).

The mechanism is specification.

## Relations

- derivedFrom: [Detectable drift](../stakeholder/detectable-drift.md){id=note:req:d6m4q7z}
- delivers: [Impediments Surface as Divergence](../../offerings/trust-by-inspection/pr-impediments-surface-as-divergence.md){id=note:pr:mj3py3d}
