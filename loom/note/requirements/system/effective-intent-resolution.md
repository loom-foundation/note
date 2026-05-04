---
id: note:req:5xnajsm
name: Effective-intent resolution
kind: requirement
level: system
type: functional
status: current
---

Note shall ensure the effective intent at any scope is deterministically computable by composing inherited intent.

Where two inherited sources conflict and are comparable along the scope graph, the source at the nearer scope shall govern, because the nearer source is itself authored intent.

Where conflicting sources are not comparable, or where a nearer source removes rather than strengthens or replaces an inherited obligation, the conflict shall be surfaced for explicit resolution rather than resolved automatically.

The result shall remain traceable to each contributing source.

Effective Intent shall not be stored as a separate source of truth within a live corpus.

## Rationale

A single linear chain can be merged naively, but multi-source inheritance can present conflicts.

A conflict between comparable sources is authored intent, a nearer scope refining a farther one, and resolves by proximity; a conflict between incomparable sources, and any removal of an inherited obligation, is surfaced rather than resolved, because picking a winner there would be a silent guess.

Proximity is a partial order: where nearer is undefined, the conflict surfaces.

The procedure is decided in [Cascade conflict resolution](../../decisions/cascade-conflict-resolution.md){id=note:dec:9c4tk2n}.

Keeping the derivation traceable lets a reader or auditor see, at any scope, both the effective obligation and how it was composed from its contributing sources; this is the inheritance equivalent of traceability, and it is what lets a surfaced conflict be resolved at the right scope rather than guessed at.

Storing the resolved result as its own artifact would create a second source that drifts; the one deliberate exception, which carries provenance and severs the link, is materialization ([Materialization of inherited intent](materialization-of-inherited-intent.md){id=note:req:dssf1pp}).

The resolution procedure is specification.

## Relations

- derivedFrom: [Hierarchically scoped intent](../stakeholder/hierarchically-scoped-intent.md){id=note:req:6n6jdyq}
- delivers: [Obligations Ride in the Slice](../../offerings/right-sized-context/pr-obligations-in-the-slice.md){id=note:pr:0d8rpg8}
