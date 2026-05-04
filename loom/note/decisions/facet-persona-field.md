---
id: note:dec:aj00tq7
name: Facet persona field
kind: decision
status: current
decided: 2026-06-13T00:00:00Z
---

The Job, Pain, and Gain kinds gain an optional `persona` frontmatter field: a citation, or a list of citations, of personas the facet speaks for, drawn from the parent need's `persona` set.
Omitted, the facet speaks for the need's whole persona set; present, it narrows the facet to the listed subset.
Each entry uses the standard citation form, the id authoritative; pack-aware validation surfaces a facet persona that is not on the parent need.

## Context

A need may be wanted by more than one persona, and its `persona` field carries the full set.
A facet carries no persona of its own, so a job, pain, or gain authored under a multi-persona need reads as belonging to every persona on the need, even where it is felt or sought by only one.
That attribution is real intent with no place to live: the profile model makes the need the root that carries the who, and the facets members written in the persona's terms ([Atomic facets](atomic-facets.md){id=note:dec:af3k9w2}).

The corpus already has the shape for this: `subkind` on Pain and `expectation` on Gain are optional enrichment fields an author applies when the value is known and worth recording ([Pain subkind field](pain-subkind-field.md){id=note:dec:qc2nc57}; [Gain expectation field](gain-expectation-field.md){id=note:dec:c1m3hpn}).

## Decision

- **An optional `persona` field on `job`, `pain`, and `gain`.**
  The field is optional and available at every profile, on the three need-side facet kinds only.
  The need's own `persona` remains required spine frontmatter and is never derived from facets.

- **Omitted means the need's whole set.**
  A facet without the field speaks for every persona its need carries; absence is inheritance, not an unknown.

- **Present means a narrowing subset.**
  The field holds a citation, or a list of citations, of persona artifacts, in the standard citation form the need's own field uses (name label, relative path, id, the id authoritative).
  The listed personas narrow whom the facet speaks for; entry order carries no meaning.

- **The subset property is checked, and a violation is surfaced.**
  A facet's personas are a subset of its parent need's; the parent is computed through the facet's `partOf` relation.
  Pack-aware validation reports a facet persona missing from the need as a finding: either the need under-lists its personas or the facet is misplaced, and the tool reports the disagreement rather than resolving it.

- **An enrichment, not a discipline.**
  The field is not profile-gated, mirroring `subkind` and `expectation`: an author applies it when the narrowing is known and worth recording.

## Forces and trade-offs

Absence-as-inheritance keeps the single-persona majority clean: restating the need's persona on every facet would copy one fact downward into every member, the drift the persona-by-reference rule exists to prevent.
The cost is that absence is ambiguous between "speaks for all" and "not yet considered"; the model resolves the ambiguity by definition (absence means all), so a deliberate narrowing is always explicit.

A subset check binds the facet's claim to the need's, so the two cannot drift apart silently.
The check is computable from committed files alone: the facet's `partOf` names the need, and the need's `persona` names the set.

## Alternatives considered

- **No persona on facets (the prior state).**
  Rejected: under a multi-persona need, per-facet attribution is real intent with no place to live, and a reader must assume every facet belongs to every persona on the need.

- **A required `persona` on every facet.**
  Rejected: on the single-persona majority it restates the need's field without adding information, ceremony against Earned Substance and Proportionality.

- **Authoring personas on facets only and deriving the need's set upward.**
  Rejected: the need is the profile root and its `persona` is required spine frontmatter; deriving it would invert the profile model and leave a need's who unstated until facets exist.

- **A free-text qualifier in the facet's prose.**
  Rejected: prose attribution is not machine-readable, cannot be checked against the need's set, and drifts.

## Driven by

- groundedIn: [Atomic facets](atomic-facets.md){id=note:dec:af3k9w2}
- groundedIn: [Terms and personas as first-class, scoped kinds](terms-and-personas-as-kinds.md){id=note:dec:t4w8k2n}
- groundedIn: [Uniform opaque identity](identity-and-designations.md){id=note:dec:jhgkwja}
- groundedIn: [Single Source of Truth](../principles/single-source-of-truth.md){id=note:principle:8691937}
- groundedIn: [Earned Substance](../principles/earned-substance.md){id=note:principle:yecemfe}
- groundedIn: [Proportionality](../principles/proportionality.md){id=note:principle:es0vhzn}
