---
id: note:term:6wmj8e9
name: Verification
kind: term
status: current
---

A representation of how a Requirement, Specification, Convention, or Acceptance Criterion is checked: the criteria that constitute a pass and the method by which the check is made.

A Verification holds the standard of passing, not the verdict; running the check and owning its result belong to the Orchestrating Authority (see `context.md`).

The kind is opt-in per the adopted profile and earns its place only where the rigor is wanted.

## Inclusion test

Does it state what would count as passing and by which method (test, analysis, inspection, demonstration, or formal proof), without holding the run's verdict or dispatching the run?

If it records a result as authoritative truth, it has crossed the boundary into the Orchestrating Authority's concern.

## Relations

- *verifies* [Requirement](requirement.md){id=note:term:tr9zna6}
- *carries* [Verification Method](verification-method.md){id=note:term:mx6w20w}

## Origin

ISO/IEC/IEEE 29148 and the INCOSE tradition, where verification confirms that a system meets its specified requirements by one of four methods (test, analysis, inspection, demonstration), kept distinct from validation (fitness for the stakeholder's purpose).

The criterion-not-verdict split follows executable-specification practice, where the specification states the expected behavior and a separate run produces the result.
