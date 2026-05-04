---
id: note:dec:ghrzmwt
name: Documentation as package prose
kind: decision
status: current
decided: 2026-06-13T00:00:00Z
---

Package documentation lives beside the layer root as plain Markdown prose: a level-1 title, no frontmatter envelope, no id, no kind, no status.
There is no documentation kind, and an id is never granted to a file that is not an artifact of a declared kind.
A doc cites the corpus with the standard citation form, and the normative source is always the cited artifact, never the doc that restates it.

## Context

A doc explains, walks through, and restates what the corpus fixes; it states no want, no obligation, no choice, and no verification.
The layer root holds authored intent only, and generated material already sits beside it rather than inside it ([Kind templates](kind-templates.md){id=note:dec:vg3k34n}).

Exposition exerts a steady pull toward identity: a docs file looks like the artifacts around it, and an author (human or AI) reaching for consistency is tempted to stamp it with an envelope, inventing a kind the packs do not declare.
The kind set is closed precisely so that a checker can tell conformance from invention ([Kind-agnostic substrate and kind packages](substrate-and-kind-packages.md){id=note:dec:w4awceq}), so the pull must be answered by a recorded rule, not case by case.

## Decision

- **Docs are package prose beside the layer root.**
  A doc is plain Markdown with a level-1 title and no frontmatter envelope, in the package's `docs/` directory; the register is stated in `docs/README.md`.

- **There is no documentation kind.**
  A kind carries intent semantics that relations, checks, and verifications key off; a doc restates rather than states, so a documentation kind would make restatement itself a first-class artifact.

- **Identity requires a declared kind.**
  An id is minted only for an artifact whose `kind` an enabled pack declares.
  A file that deserves durable citability is adopted as an artifact of a declared kind; it is never stamped with an id alone.

- **Outside files participate outbound, by citation.**
  Any file outside the corpus cites intent through the in-code citation surface ([In-code intent citation](in-code-intent-citation.md){id=note:dec:nfaeyk9}); participation does not require being citable in return.

## Forces and trade-offs

Keeping docs envelope-free keeps the boundary checkable: everything carrying an id answers to a pack's schema, and a validator can hard-fail a slug or an undeclared kind without a list of exceptions.
The cost is that a doc is not a relation endpoint, so "which docs restate this spec" is computed from the docs' own citations rather than authored; accepted, because the citations already carry the direction that matters.

Restatement drifts, and placement does not cure drift.
The mitigation is the citation discipline: a doc that cites its normative sources by id gives a tool the edge it needs to flag a doc older than the artifact it restates.

## Alternatives considered

- **A documentation kind.**
  Rejected: it institutionalizes restatement as a first-class artifact against Single Source of Truth, carries no intent semantics for relations or checks to key off, and adds lifecycle ceremony to files that are current by being published.

- **Granting ids to arbitrary files without a kind (stamping).**
  Rejected: every relation is typed by its endpoints' kinds and every check keys off kind, so an id without a kind is a citation target with no contract; granted freely, it dissolves the closed boundary that makes the corpus checkable.

- **Placing docs inside the layer root.**
  Rejected: the layer root holds authored intent only, and a doc is not intent; the package root is the documented home for material that serves the corpus without being part of it.

## Driven by

- groundedIn: [Single Source of Truth](../principles/single-source-of-truth.md){id=note:principle:8691937}
- groundedIn: [Earned Substance](../principles/earned-substance.md){id=note:principle:yecemfe}
- groundedIn: [Kind templates](kind-templates.md){id=note:dec:vg3k34n}
- groundedIn: [Kind-agnostic substrate and kind packages](substrate-and-kind-packages.md){id=note:dec:w4awceq}
- groundedIn: [In-code intent citation](in-code-intent-citation.md){id=note:dec:nfaeyk9}
