---
id: note:dec:qc2nc57
name: Pain subkind field
kind: decision
status: current
decided: 2026-06-10T22:28:14Z
---

The Pain kind gains an optional `subkind` frontmatter field with the closed value set `problem`, `obstacle`, `risk`, available at every profile, scoping to Pain only.

## Context

The Pain term already classifies pains into three sub-kinds drawn from the Value Proposition Canvas lineage: an undesired outcome or problem the persona already endures, an obstacle that stands in the way of a Job, and a Risk, a potential, not-yet-realized undesired outcome the persona fears.
The term noted that recording a pain's sub-kind as an attribute was a later, profile-gated refinement not carried at the time of authoring.

Two forces now make the field worth landing.

First, consumers of the corpus (humans and agents alike) want to filter pains by sub-kind: all risks the persona carries, all obstacles to a Job, and so on.
Without a machine-readable field, that query requires reading prose.

Second, the Pain term's own classification already provides the closed value set; the decision is therefore about when and how to record it, not about what the values are.

## Decision

- **Field name: `subkind`.**
  The field is named `subkind`, following the corpus's own vocabulary: the Pain term already names the concept "sub-kinds", making `subkind` the established term for this axis.
- **Closed value set: `problem`, `obstacle`, `risk`.**
  The three values correspond directly to the term's three sub-kinds.
  `problem` names the "undesired outcome or problem" sub-kind: the term pairs the two words because both describe the same category, and `problem` is the shorter, equally precise token that carries the full meaning.
  `obstacle` and `risk` are taken verbatim from the term.
- **Optional at every profile.**
  The field is optional and available at the `bare` profile and above.
  A profile gates disciplines (the what and how of authoring); an optional field is not a discipline, it is an enrichment an author applies when the sub-kind is known and worth recording.
  Making the field profile-gated would require a pain author operating at any profile below `strict` to leave out a simple, low-cost classification, with no benefit.
- **Scope: Pain only.**
  The Gain kind has a symmetric classification (the Kano expectation ladder: required, expected, desired, unexpected).
  That ladder is a different structure and already has the term's own vocabulary.
  Extending a parallel `subkind` to Gain is the symmetric case deliberately not taken here; it is a separate decision if ever needed.

## Forces and trade-offs

Adding a frontmatter field to a kind increases the schema surface.
The cost is low: the field is optional, so existing pains without it remain valid, and raising a profile never invalidates an artifact that was valid under a lighter one.

The field name `subkind` is a compound that does not appear in the Value Proposition Canvas.
The canvas labels these "types of pains"; Note cannot reuse "type" because `type` already names the requirement-typing axis ([Type](../terms/requirement-typing/type.md){id=note:term:mwwzghp}).
`subkind` follows the corpus's own term, which calls them sub-kinds, and is coined here with that justification ([Reuse established vocabulary before coining new terms](established-vocabulary-first.md){id=note:dec:8f3m5vk}).

`problem` for "undesired outcome or problem" collapses a paired phrase to its second element.
The pairing in the term exists because both nouns are common; `problem` is preferred as the closed-vocabulary token because it is shorter and unambiguous in this context, and the full description lives in the term's body, not in the token.

## Alternatives considered

- **Field name `type`.**
  Rejected: `type` is already in use on the Requirement kind to name the functional, non-functional, and constraint axis.
  Reusing it on Pain for a different classification would produce a collision across kinds and confuse any reader or tool that looks for `type` in frontmatter.
- **Field name `kind`.**
  Rejected: `kind` is reserved in the common frontmatter envelope as the artifact-kind discriminator.
  A second `kind` field on Pain would shadow the common field.
- **Field name `category`.**
  Rejected: `category` has no established meaning in the corpus or in its lineage, and introduces a synonym where `subkind` is already the right word given the term's own vocabulary.
- **Profile-gating the field at `strict`.**
  Rejected: a pain's sub-kind is a simple, low-cost classification that adds filtering value at any profile.
  The profile mechanism gates disciplines, not individual optional enrichments; gating this field would add ceremony without adding rigor.
- **Extending `subkind` to Gain at the same time.**
  Deliberately not taken here.
  The Kano expectation ladder for Gain (required, expected, desired, unexpected) is a different structure requiring its own decision.
  Landing it as a parallel extension to this decision would conflate two separate classification questions; it is recorded as the symmetric case under consideration, not as a deferred TODO.

## Driven by

- groundedIn: [Single Source of Truth](../principles/single-source-of-truth.md){id=note:principle:8691937}
- groundedIn: [Proportionality](../principles/proportionality.md){id=note:principle:es0vhzn}
