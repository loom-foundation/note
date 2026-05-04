---
id: note:term:r8bcg5d
name: Derivation
kind: term
status: current
---

The refinement of intent within the requirements layer: a finer Requirement records that it decomposes from a coarser one.

Derivation is distinct from Scope cascade: derivation refines intent down the requirements layer, cascade composes the same intent across scopes.

## Inclusion test

Are both endpoints Requirements, with one a refinement of the other?
If so it is Derivation, not satisfaction (which crosses from requirement to specification) and not cascade (which crosses scopes).

## Origin

General English (Oxford: "the obtaining or developing of something from a source or origin").

The sense is sharpened by systems-engineering practice, where a derived requirement is one decomposed from a higher-level requirement as the design is refined (for example in ISO/IEC/IEEE 29148 requirements engineering), and by the `derivedFrom` relation this corpus authors on the finer end.
