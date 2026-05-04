---
id: note:dec:3vg9jdh
name: Principle altitude field
kind: decision
status: current
decided: 2026-06-27T00:00:00Z
---

The Principle kind gains an optional `altitude` frontmatter field with the closed value set `value`, `operating`, `authoring`, available at every profile, scoping to Principle only.
The field records the home altitude at which a weighted commitment operates and the reader it serves; it is a within-kind reading lens, not a new kind and not a relation.

## Context

A corpus that grows a sizable body of principles finds them operating at different levels and serving different readers: bedrock commitments naming who its authors are (its values), operating commitments that guide day-to-day work, and authoring commitments that govern how the corpus itself is written.
All three are weighted commitments balanced against others, which is what the Principle inclusion test admits ([Principle](../terms/artifact-kinds/principle.md){id=note:term:q2snn7e}); they differ by altitude, not by being principle-versus-rule.
The distinction is load-bearing for grouping, filtering, and routing: values and operating principles belong on a manifesto, authoring principles on a corpus-authoring guide, and an actor wants to read or review each through the right lens without inferring it from prose.

The value level pressed hardest, because "value" and "principle" are distinct in the literature: a value is a held good ranked by priority (Rokeach, Schwartz), while a principle is a weighted, action-guiding standard balanced in the moment (Dworkin), and the Agile Manifesto keeps four values and twelve principles as separate tiers.
Note nonetheless records a value as a principle at the `value` altitude rather than as a separate kind, for a structural reason the method's own rule fixes.

A distinction earns a separate kind only when it carries a distinct inbound relation, the test that makes a pain and a gain different kinds because one is relieved and the other created ([Atomic facets](atomic-facets.md){id=note:dec:af3k9w2}).
A value carries no relation a principle lacks: a requirement or convention `enacts` it and a decision is `groundedIn` it, exactly as for any principle, and where operating principles genuinely derive from values that derivation is an ordinary principle-to-principle relation authored in `## Relations`.
So value-versus-principle is an altitude, a field on the one Principle kind, not a kind boundary; a separate Value layer was already rejected on these grounds ([Principles as a first-class kind](principles-first-class.md){id=note:dec:eym5t5g}), a rejection this decision leaves standing.

## Decision

- **An optional `altitude` field on Principle.**
  The closed value set is `value`, `operating`, `authoring`, defined as terms under [the Principle altitudes vocabulary](../terms/principle-altitudes/altitude.md){id=note:term:a1h1jre}: `value` is a bedrock commitment carried into everything, `operating` guides day-to-day work, `authoring` governs how the corpus itself is written.

- **Field name: `altitude`.**
  Named for the level at which a commitment operates.
  `facet` is rejected because the corpus already uses "facet" for the members of a Need or Offering; `subkind` is rejected because it already names the Pain axis and is used on other kinds, and precision to each axis, not parallel names, is the corpus's naming discipline ([Gain expectation field](gain-expectation-field.md){id=note:dec:c1m3hpn}).

- **Value token: `value`.**
  The bedrock altitude is named `value` because that is what such a commitment is, a held good the corpus carries into everything.
  The token is read in the scope of the `altitude` field, where it names a level, distinct from the value-proposition and value-map concepts of the discovery pack.

- **The home altitude, single-valued.**
  A principle that operates at more than one altitude records its home altitude, the one that fixes where it is published and read.
  The field is a placement-and-routing lens, not a claim that the altitudes partition the principles; genuine multi-altitude is surfaced by principle-to-principle relations, not by listing several values.

- **Optional at every profile.**
  The field is optional and available at the `bare` profile and above; an optional enrichment an author applies when the altitude is worth recording, not a profile-gated discipline.

- **Scope: Principle only.**
  Altitude classifies principles; it is not a generic axis on every kind.
  A cross-kind, sensitivity-style axis is a separate, deferred thread ([Classification as a generic axis](classification-axis-deferred.md){id=note:dec:t8qrs9h}).

- **The Principle-versus-Convention boundary holds.**
  An authoring principle is the weighted value (for example Single Source of Truth); the concrete, arbitrary practice that puts it into effect (a casing scheme, a file layout) is a Convention that `enacts` it.
  A rule that matters only by agreement among workable equals is a Convention, not an authoring Principle, and carries no altitude.

## Forces and trade-offs

Adding a field to a spine kind increases the universal schema surface, against Earned Substance.
It is accepted because the field is optional and zero-cost when unused, the closed set has a single authoritative home in the terms, and the altitude distinction recurs for any corpus that keeps both the principles governing its product and the principles governing its own authoring.

Recording a value as a `value`-altitude principle rather than as its own kind keeps the model honest to the atomic-facets rule and avoids reopening a settled rejection, at the cost of telling an adopter that their values are principles at a level rather than a separate artifact kind.
This is accepted because the alternative buys a kind that carries no distinct relation, inverts the principle coverage signal (a bedrock value an obligation does not point at would read as a pruning candidate), and needs a verb that overlaps `enacts` and `groundedIn`.

Single-valued altitude loses information where a principle genuinely spans levels; accepted because the field's job is to route a principle to one home, and the span, where it matters, is recoverable through authored principle-to-principle relations.

## Alternatives considered

- **A distinct Value kind (the values-over-principles split).**
  Rejected: a value carries no inbound relation a principle lacks, so by the atomic-facets rule it is a field, not a kind; a Value layer was already rejected under Earned Substance ([Principles as a first-class kind](principles-first-class.md){id=note:dec:eym5t5g}), minting it would invert the principle coverage signal on a corpus's most load-bearing commitments, and it would need a `serves` verb redundant with `enacts` and `groundedIn`.
  Where a corpus genuinely derives principles from values, that derivation is an authored principle-to-principle relation, not a new kind.

- **Token `identity` for the bedrock altitude.**
  Rejected: the commitments at this level are values, held goods, and `identity` names what they express rather than what they are; `value` is the precise token, read in the scope of the `altitude` field.

- **Field name `facet` or `subkind`.**
  Rejected: `facet` collides with the Need and Offering members; `subkind` is the Pain axis and is used on other kinds with a different value set.

- **A multi-valued altitude set.**
  Rejected as the default: the field exists to route a principle to its single home; genuine multi-altitude is carried by explicit principle-to-principle relations.

- **Leave the classification corpus-local and unsanctioned.**
  Rejected as the method-level answer: an unsanctioned field is silently ignored by a checker and drifts into spelling variants, and the lens is general enough to earn a sanctioned home.

- **Profile-gate the field at `strict`.**
  Rejected: a principle's altitude is a low-cost classification that adds routing value at any profile; the profile mechanism gates disciplines, not optional enrichments.

## Driven by

- groundedIn: [Principles as a first-class kind](principles-first-class.md){id=note:dec:eym5t5g}
- groundedIn: [Atomic facets](atomic-facets.md){id=note:dec:af3k9w2}
- groundedIn: [Earned Substance](../principles/earned-substance.md){id=note:principle:yecemfe}
- groundedIn: [Single Source of Truth](../principles/single-source-of-truth.md){id=note:principle:8691937}
- groundedIn: [Proportionality](../principles/proportionality.md){id=note:principle:es0vhzn}

## Worked example

A corpus that keeps a manifesto and a corpus-authoring guide marks each principle with its home altitude:

```markdown
---
id: acme:principle:8r2k4wq
name: Single Source of Truth
kind: principle
status: current
altitude: authoring
---

State each fact once, in one authoritative home, and derive every other view from it.
```

A reader assembling the corpus-authoring guide filters principles to `altitude: authoring`; the manifesto is the `value` and `operating` principles; a principle whose altitude is left blank is simply not yet routed, not malformed.
