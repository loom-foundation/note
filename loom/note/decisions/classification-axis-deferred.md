---
id: note:dec:t8qrs9h
name: Classification as a generic axis
kind: decision
status: current
decided: 2026-06-19T00:00:00Z
---

Sensitivity classification is a cross-cutting axis any artifact may carry, not a property of any one kind: the method will model it as a generic, manifest-declared label with method-defined propagation, represented and computed but never enforced, complementary to the governance and compliance packs and bound to neither.
The axis is named and scoped here; its full design is a separate thread, not settled in this record.

## Context

An organization documenting policies and standards asks to mark them confidential, restricted, or secret.
The pull is to add a `classification` field to the governance kinds, and the pull is wrong: a classification is not a governance property.

A specification can be secret; source the corpus cites can be secret; a need can be restricted.
A national-security adopter classifies artifacts across every kind, and a governing instrument is only one of them.
Sensitivity is therefore an axis of its own, orthogonal to the ones the method already separates: a profile gates rigor, a pack gates kind availability, a status gates maturity, a scope fixes where intent is load-bearing, and a classification would gate sensitivity.
Folding it into the governance pack would repeat the conflation the method's one-job-per-axis discipline exists to prevent.

It also sits exactly where Compute and Report draws the line.
The method can represent a classification and compute its propagation; it cannot decide who may read a secret artifact.
That decision is access control, which belongs to the Orchestrating Authority, the seam at which the method already stops.

## Decision

- **Classification is a generic axis, not a governance field.**
  No governance kind carries a `classification` field; the governance pack reaches the axis, where it is present, by the same mechanism every other kind does.

- **The scheme is declared, the label is carried, the propagation is method-defined.**
  The set of levels and their ordering, an unclassified-to-top-secret ladder or a traffic-light protocol, is a scheme declared once in the manifest, the way packs, profile, and scope are; an artifact carries a label from that scheme; and the effective classification of an artifact is computed by a method-defined rule, the high-water mark of its own label and those it derives from or is contained by.

- **Represented and computed, never enforced.**
  The method labels an artifact, computes its effective classification, and surfaces it; who may read it is access control, decided and enforced by the Orchestrating Authority.
  The axis informs which intent a context slice carries; it gates nothing.

- **Opt-in and zero-cost when unused.**
  Like scope, a corpus that declares no classification scheme carries no label and pays nothing; the axis is engaged only by a corpus that needs it.

- **The full design is deferred.**
  Whether the axis lands as a substrate field or a small built-in pack, the exact propagation rule, and its interaction with the relevant-context slice are settled in a later thread; this record fixes that the axis is generic, represent-not-enforce, and separate from governance, so the governance pack ships without a classification field rather than with the wrong one.

## Forces and trade-offs

Naming the axis now, rather than adding a field later, costs one decision record and keeps the governance kinds clean: a classification field on a policy would be copied onto a specification the first time a secret system was specified, and the duplication is the signature of the misplacement.

Deferring the design is safe for the reason the risk kind's deferral is: a generic axis is additive against the substrate, touching no kind's existing fields, so landing it later breaks no corpus authored before it.

## Alternatives considered

- **Carry a `classification` field on policy and standard.**
  Rejected: sensitivity attaches to any kind, so a governance-only field both under-serves the adopter who classifies a specification and miscategorizes an axis as a property; the conflation is the error the one-job-per-axis discipline guards.

- **Let the method enforce access from the classification.**
  Rejected: an authority the files cannot enforce is advisory dressed as structural, by Compute and Report; the method represents and computes the label and leaves access control to the Orchestrating Authority.

## Driven by

- groundedIn: [Kind-agnostic substrate and kind packages](substrate-and-kind-packages.md){id=note:dec:w4awceq}
- groundedIn: [The risk kind](risk-kind-deferred.md){id=note:dec:ge1r86x}
- groundedIn: [Compute and Report](../principles/compute-and-report.md){id=note:principle:6e7f28k}
- groundedIn: [Proportionality](../principles/proportionality.md){id=note:principle:es0vhzn}
- groundedIn: [Earned Substance](../principles/earned-substance.md){id=note:principle:yecemfe}
