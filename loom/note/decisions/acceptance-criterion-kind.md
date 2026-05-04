---
id: note:dec:sxv0tq9
name: The acceptance-criterion kind
kind: decision
status: current
decided: 2026-06-12T00:00:00Z
---

An acceptance-criterion is a first-class kind in the spine pack: a solution-free condition, authored at commit time alongside its requirement, that defines what "acceptable" means for a requirement or a need.
It is declarative, the statement of what acceptable is, and it is distinct from a verification, which is the executable check that confirms the condition holds.
It carries the verb `qualifies` (acceptance-criterion to a requirement or a need; inverse `qualifiedBy`), and the `verifies` target set widens so that a verification may check an acceptance-criterion directly.
A `## Acceptance criteria` section on a requirement is a permitted authoring on-ramp; the standalone kind is the canonical, promoted form.

## Context

Between the obligation a requirement states and the executable check a verification runs sits a third thing the trace had no home for: the condition that says, in solution-free terms, what would make the requirement or the need acceptable.
A requirement states what must be true; an acceptance-criterion states the measurable threshold or observable outcome by which "true enough to accept" is judged; a verification is the procedure that establishes whether the criterion is met.
Folding the criterion into the verification collapses the declarative what-acceptable into the executable check, and the two have different authors, lifecycles, and audiences.

The persona evidence is real and pointed in opposite directions before it converged.
A Product Owner authors acceptance criteria as their primary artifact, solution-free and before any build, to fix what the team is being asked to deliver; a verification engineer authors the check later, often in a different register and against a chosen mechanism.
Across a startup lead (where the Product Owner and the engineer are the same person) and a regulated systems engineer (where they are different people governed by different standards), the criterion and the check came out as distinct artifacts with distinct moments of authorship.
The conflation loses the Product Owner's primary artifact entirely, and shipping a verification kind that silently carries acceptance semantics forces a later re-cut of the `verifies` endpoint set and of every verification authored in the meantime.

A kind is earned when it carries load at the point of reference and in its relations, and when its author, lifecycle, and audience differ from its neighbors'.
The acceptance-criterion clears that bar: it is authored solution-free, before build, per item, by the party accountable for what acceptable means, which is a different author, a different lifecycle moment, and a different audience from the verification that later checks it.
That is why it is a kind, not a section on the requirement.

## Decision

- **The acceptance-criterion is a first-class kind.**
  Its id kind-segment is `ac`, and its name is singular: an `acceptance-criterion` is one condition.
  One criterion is one artifact with one id, consistent with the rule that an independently referenced unit of intent is its own file.

- **It is solution-free and declarative.**
  An acceptance-criterion states the condition under which a requirement or need is acceptable, naming no mechanism, the same solution-free discipline a functional or non-functional requirement carries.
  It is the declarative what-acceptable, not the executable how-checked.

- **It is distinct from a verification.**
  A verification is the executable check; an acceptance-criterion is the condition the check confirms.
  The two are separate kinds with separate authors and separate lifecycle moments: the criterion is authored at commit time with the requirement, before build; the verification is authored against a chosen method, around build.

- **`qualifies` is its verb.**
  An acceptance-criterion authors `qualifies`, naming the requirement or need it makes acceptable; the inverse `qualifiedBy` is a derived view.
  A criterion qualifies exactly one of a requirement or a need, the item whose acceptance it defines.

- **The `verifies` target set widens to include acceptance-criterion.**
  A verification may verify an acceptance-criterion directly, in addition to the requirement, specification, and convention it could already target.
  The requirement is met transitively: the verification checks the criterion, the criterion qualifies the requirement, and the trace closes through `qualifies` and `verifies`.

- **`## Out of scope` is recommended at standard.**
  An acceptance-criterion reads more clearly when it names what it does not require alongside what it does, so at the standard profile a `## Out of scope` section is the recommended body shape, guarding against a criterion read as broader than intended.

- **A section is a permitted on-ramp; the kind is the canonical form.**
  A `## Acceptance criteria` section authored on a requirement is a blessed lightweight on-ramp, so an author need not mint a separate file for every criterion from the first draft.
  The standalone kind is the canonical, promoted form, and a tool promotes a bundled section into its own acceptance-criterion artifacts, exactly the bundled-draft-to-facets promotion pattern that [Atomic facets](atomic-facets.md){id=note:dec:af3k9w2} establishes.
  Where a criterion is traced to, referenced, or verified, it earns its own file; until then the section is enough.

## Forces and trade-offs

A new kind presses against Earned Substance, and the acceptance-criterion clears the bar on the three-consumers test: it is referenced (a verification verifies it, a requirement is qualified by it), it is the single source the Product Owner's acceptance artifact would otherwise scatter across prose or a tracker, and it is the declarative anchor a check is written against.

Per-criterion identity raises the file count, and at scale a corpus with three thousand requirements could face many thousands of criteria files.
The on-ramp absorbs this: a criterion lives as a section on its requirement until it is traced to, and is promoted to its own file only where the identity earns its keep, so the floor stays light and the ceremony falls only where a criterion is independently load-bearing.

Carving the criterion out of the verification now, in this version, costs a section in this decision and the widening of one endpoint set.
Deferring it would cost a semantic re-cut of the verification kind at the next version and a change of meaning for every verification authored in between, which is the more expensive path and the one a pre-release method can still avoid.

## Alternatives considered

- **Name the kind `acceptance-criteria`, plural.**
  Rejected: every other kind token is singular, and the one-unit-one-file rule plus per-criterion verification require that one artifact be one criterion, so the singular `acceptance-criterion` is the grammatically consistent token; the plural survives only in prose, for the concept.

- **Fold the acceptance-criterion into the verification kind.**
  Rejected: it loses the Product Owner's primary artifact, the solution-free statement of what acceptable means, and conflates the declarative condition with the executable check, forcing a later semantic re-cut of the `verifies` endpoint set when the two are finally separated.

- **Make the acceptance-criterion kind mandatory on every requirement.**
  Rejected: not every requirement earns an explicit criterion, and mandating one taxes the light cases with ceremony they do not need; the kind is available and recommended, its use the author's call, with the section on-ramp keeping even the used case cheap.

## Driven by

- groundedIn: [The default spine pack](spine-pack.md){id=note:dec:4tzn3av}
- groundedIn: [Earned Substance](../principles/earned-substance.md){id=note:principle:yecemfe}
- groundedIn: [Proportionality](../principles/proportionality.md){id=note:principle:es0vhzn}
- groundedIn: [Unambiguous, testable requirements](../needs/unambiguous-testable-requirements.md){id=note:need:e4k9w2n}
