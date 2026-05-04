---
id: note:dec:vf2m8qe
name: The validation field
kind: decision
status: current
decided: 2026-07-02T00:00:00Z
---

The Need, Pain, Gain, and Value Proposition kinds carry an optional `validation` frontmatter field with the closed value set `assumed`, `inferred`, `observed`, `established`, `invalidated`, available at every profile.
The field grades the embedded claim those kinds carry, that the problem is real and the persona has it, or that the offered value lands, so an unvalidated assumption is told from a confirmed finding; the tier meanings stay fixed by the Validation term, and the evidence behind a raise is cited per the evidence convention.

## Context

The corpus has long graded claims: the [Validation](../terms/validation/validation.md){id=note:term:13esbh9} term fixes the five tiers, [Validation evidence in the Source](../conventions/validation-evidence-in-source.md){id=note:conv:8wafpx1} fixes where a raise cites its evidence, and [Atomic facets](atomic-facets.md){id=note:dec:af3k9w2} already describes a need as carrying "an optional `validation`".
The field is in live use across this corpus's needs, pains, and value propositions.

What was missing was the declaration: no pack specification carried a `validation` row, so a checker built from the enabled packs alone, as the substrate promises, reported every use as an undeclared field.
A field the terms and docs teach but no specification declares is a rule the normative core does not own.

## Decision

- **Field name: `validation`.**
  The name the Validation term already gives the axis; no new word is coined.

- **Closed value set: `assumed`, `inferred`, `observed`, `established`, `invalidated`.**
  The five tiers the Validation term defines; the term stays the single home of their meanings.

- **Declared on need, pain, gain, and value-proposition.**
  Exactly the kinds whose substance embeds a validatable claim: that the problem is real and the persona has it, or that the offered value lands.
  The spine pack declares the need row; the discovery pack declares the pain, gain, and value-proposition rows.

- **Optional at every profile.**
  An enrichment an author applies when the confidence is known and worth recording, not a profile-gated discipline, mirroring `subkind` and `expectation`.

- **Evidence rides the existing convention.**
  A raised tier cites the evidence behind the raise per [Validation evidence in the Source](../conventions/validation-evidence-in-source.md){id=note:conv:8wafpx1}; this decision adds no second evidence mechanism.

## Forces and trade-offs

Declaring the field widens two pack schemas by one optional row each.
The cost is low: the field is optional, every existing use becomes conformant rather than newly obligated, and a corpus that grades nothing pays nothing.

Declaring it per kind, rather than once in the substrate's common optional set, keeps the substrate kind-agnostic: the graded claim is a property of the claim-bearing kinds, not of every artifact, and a `validation` on a decision or a term would grade nothing that `status` does not already say.

## Alternatives considered

- **Declare `validation` in the substrate's optional common frontmatter.**
  Rejected: the substrate knows no kind, and the field is meaningful only where an artifact embeds a validatable claim; a common field would invite grading artifacts whose maturity is already the `status` field's job.

- **Gate the field at `strict`.**
  Rejected: honesty about confidence is cheap and valuable at every profile, and the profile mechanism gates disciplines, not optional enrichments, the same reasoning as [Pain subkind field](pain-subkind-field.md){id=note:dec:qc2nc57}.

- **Leave the field taught by terms and docs only.**
  Rejected: it breaks the pack promise that kinds, fields, sections, and links are checkable from the files plus the declared packs alone, which is the defect this decision exists to close.

## Driven by

- groundedIn: [Adopt the method on a system that already exists](../needs/brownfield-adoption.md){id=note:need:b3k9w2t}
- groundedIn: [Incremental capture of recovered intent](../requirements/system/incremental-intent-capture.md){id=note:req:m2x8k5p}
- groundedIn: [Atomic facets](atomic-facets.md){id=note:dec:af3k9w2}
- groundedIn: [Single Source of Truth](../principles/single-source-of-truth.md){id=note:principle:8691937}
- groundedIn: [Proportionality](../principles/proportionality.md){id=note:principle:es0vhzn}
