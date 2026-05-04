---
id: note:req:sp8g0my
name: Checkable well-formedness and identity
kind: requirement
level: system
type: functional
status: current
---

Note shall ensure that every artifact's well-formedness and identity are checkable from the file alone: both the structure common to all kinds (the envelope every artifact shares) and the body shape specific to each kind.

A validator shall be able to decide whether a need, a requirement, a specification, or a decision record is well-formed, not merely whether its envelope is.

## Rationale

The rest of the method presupposes this schema: tiered conformance speaks of well-formed frontmatter and required fields, and typed relations and stable identity attach to fields this defines.

Stating it makes the corpus self-describing: the format every artifact, these requirements included, is written in is the format the method requires.

Which fields and sections are mandatory at a given tier is decided by the profile ([Tiered conformance](tiered-conformance.md){id=note:req:bth0rxp}), which selects from the vocabulary this requirement defines; the schemas themselves are specification.

## Relations

- derivedFrom: [Inspectable traceability](../stakeholder/inspectable-traceability.md){id=note:req:sg0npmv}
- derivedFrom: [Durable, portable intent](../stakeholder/durable-portable-intent.md){id=note:req:93kczqj}
- derivedFrom: [Universal participation](../stakeholder/universal-participation.md){id=note:req:j4kecn7}
