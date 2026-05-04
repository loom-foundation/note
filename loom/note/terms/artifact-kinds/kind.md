---
id: note:term:1vm1yqf
name: Kind
kind: term
status: current
---

The classification that says what sort of artifact a file is: a member of the set declared by the Kind Packages the corpus has enabled.

A Kind fixes the body shape an artifact must take and the relations it may carry; it is recorded in the `kind` frontmatter field and forms the middle segment of a Durable Identifier (`namespace:kind-segment:opaque`).
The legal kinds in a corpus are exactly those the enabled Kind Packages declare: enabling the spine pack introduces need, requirement, specification, decision, verification, acceptance-criterion, term, persona, convention, principle, and context; enabling the discovery pack adds offering, value-proposition, system, job, pain, gain, pain-reliever, and gain-creator.
There is no global fixed enum; the effective kind set is a property of the corpus's manifest.

## Inclusion test

Does the label answer "what sort of artifact is this?", fixing the artifact's body shape and the relations it may hold, rather than what the artifact is about (its content), what quality it must exhibit (its type), or where its obligation sits (its level)?
Is the label declared by a Kind Package enabled in the corpus?

If both hold, it is a Kind in scope.

## Relations

- *contrasts with* [Type](../requirement-typing/type.md){id=note:term:mwwzghp} (the quality axis of a Requirement: functional, non-functional, constraint)
- *contrasts with* [Level](../requirement-levels/level.md){id=note:term:60yb5qr} (the refinement axis of a Requirement: stakeholder, system)

## Origin

Oxford: "a class or type of people or things having similar characteristics".

Chosen over "type" precisely because "type" already names the Requirement-typing axis (functional, non-functional, constraint) in this corpus; a distinct word keeps the artifact-classification axis and the requirement-quality axis from colliding.

The role is standard in document and modeling systems, where an element's kind (or stereotype) fixes its schema and its admissible relations.
