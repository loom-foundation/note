---
id: note:dec:c1m3hpn
name: Gain expectation field
kind: decision
status: current
decided: 2026-06-10T22:51:18Z
---

The Gain kind gains an optional `expectation` frontmatter field with the closed value set `required`, `expected`, `desired`, `unexpected`, available at every profile, scoping to Gain only.

## Context

The Gain term already places gains on the Kano expectation ladder: from a *required* outcome through *expected* and *desired* ones to an *unexpected* delight.
The term noted that recording a gain's position on the ladder was a later, profile-gated refinement, not an attribute carried at the time of authoring.

The Pain kind recently gained a parallel optional `subkind` field ([Pain subkind field](pain-subkind-field.md){id=note:dec:qc2nc57}) to make its sub-kind classification machine-readable.
The same filtering rationale applies to gains: consumers want to retrieve all required gains, all delighters, or all standard expected outcomes across a need without reading prose.

Two forces motivate landing the field now.

First, the Kano classification already provides the closed value set; the decision is about when and how to record it, not about what the values are.

Second, the symmetry with the Pain `subkind` field makes the schema legible: Pain names what kind of negative experience this is; Gain names where on the expectation ladder this positive outcome sits.

## Decision

- **Field name: `expectation`.**
  The field is named `expectation` because the Kano model's own framing is expectation levels; the Gain term describes the axis as "the Kano expectation ladder".
  Using the word the model itself uses grounds the field in the established lineage without coining new vocabulary ([Reuse established vocabulary before coining new terms](established-vocabulary-first.md){id=note:dec:8f3m5vk}).
- **Closed value set: `required`, `expected`, `desired`, `unexpected`.**
  The four values correspond directly to the Kano model's four expectation tiers.
  `required` maps to Kano must-be quality, whose absence is felt as pain.
  `expected` maps to one-dimensional quality, the standard expectations a persona holds.
  `desired` maps to outcomes beyond the expected that the persona wants.
  `unexpected` maps to Kano attractive quality, a delight the persona did not anticipate.
- **Optional at every profile.**
  The field is optional and available at the `bare` profile and above.
  A profile gates disciplines; an optional field is an enrichment an author applies when the level is known and worth recording.
  Making it profile-gated would withhold a simple classification from authors at any profile below `strict`, with no benefit in return.
- **Scope: Gain only.**
  The Pain kind's parallel classification is `subkind` with the value set `problem`, `obstacle`, `risk`; the two axes are structurally distinct and each belongs only to its kind.

## Forces and trade-offs

Adding a frontmatter field increases schema surface.
The cost is low: the field is optional, existing gains without it remain valid, and raising a profile never invalidates an artifact valid under a lighter one.

The field name `expectation` is longer than `subkind` but names the axis precisely: it is the expectation ladder, not a sub-kind classification.
Using `level` would collide with the Requirement Level term; `level` already names the stakeholder-to-system refinement axis and appears as the `level` frontmatter field on requirements.
Using `kind` is reserved as the artifact-kind discriminator in the common frontmatter envelope.
Using `type` would collide with the Requirement Type term and its frontmatter field.

## Alternatives considered

- **Field name `level`.**
  Rejected: `level` is already in use on the Requirement kind to name the stakeholder-to-system refinement axis.
  Reusing it on Gain for the expectation ladder would produce a collision both in the term vocabulary and in frontmatter lookups.
- **Field name `type`.**
  Rejected: `type` is already in use on the Requirement kind to name the functional, non-functional, and constraint axis.
  The same collision reasoning as `level` applies.
- **Field name `kind`.**
  Rejected: `kind` is reserved in the common frontmatter envelope as the artifact-kind discriminator.
  A second `kind` field on Gain would shadow the common field.
- **Field name `tier`.**
  Rejected: `tier` names a Validation concept in the corpus (the Tier term), making it a collision with the validation vocabulary; `expectation` names the Kano axis precisely and is preferred.
- **Field name `subkind`.**
  Rejected: `subkind` was coined for the Pain axis because the Pain term's own vocabulary uses "sub-kinds".
  The Gain term uses "expectation ladder", not sub-kinds, so `subkind` would apply a Pain-specific coinage to a structurally different axis.
  Parallel field names across Pain and Gain are not a goal; precision to each axis is.
- **Profile-gating the field at `strict`.**
  Rejected: a gain's expectation level is a simple, low-cost classification that adds filtering value at any profile.
  The profile mechanism gates disciplines, not individual optional enrichments.

## Driven by

- groundedIn: [Single Source of Truth](../principles/single-source-of-truth.md){id=note:principle:8691937}
- groundedIn: [Proportionality](../principles/proportionality.md){id=note:principle:es0vhzn}
