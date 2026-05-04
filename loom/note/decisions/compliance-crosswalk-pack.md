---
id: note:dec:ve053yf
name: The compliance crosswalk pack
kind: decision
status: current
decided: 2026-07-02T00:00:00Z
---

The method defines a **compliance** pack: an opt-in built-in package that adds typed **crosswalk** relations by which a requirement or convention records its correspondence to a control in an external framework, distinguishing equivalence, a subset relationship, and a partial overlap.
The pack adds relations, not a kind: the framework's controls are represented as read-only requirement-shaped artifacts brought in by the existing capture machinery, and the correspondence is the typed, authored-once edge between an obligation and such a control.
The pack adds no status or coverage field: coverage is a derived view, implementation status is a tool's derived reading, and a control that does not apply or is met a different way is recorded by the cascade's existing deviation operators, not by a new declaration.

## Context

A sustained body of work, whether a software system, a hardware product, a process, or a methodology like this corpus, often must answer to a control framework owned by someone else: a security standard, a regulatory catalog, a customer's control set ([Crosswalk intent to the frameworks it answers to](../needs/crosswalk-to-external-frameworks.md){id=note:need:5mmrydr}).
The governance practice for this is the Requirements Traceability Matrix and control mapping: each obligation linked to the control it satisfies, its status, and its owner; and the machine-readable form is OSCAL, whose `component-definition` model carries `implemented-requirements` and whose `mapping` model carries the relationship types `equivalent`, `subset-of`, and `intersects-with`.

Most of what a control program needs, the corpus already has.
A control as an obligation is a constraint-typed Requirement, with the regulation in its `## Source`; the mechanism that meets it is a Specification; the check is a Verification; tailoring a framework's baseline per system, the OSCAL profile, is the cascade's strengthen, replace, and disinherit; and the traceability matrix is the corpus's own relation graph, computed from the files.
What has no home is the one genuinely new thing: a typed, checkable correspondence from an obligation to an external control, and a representation for the external controls to point at.
The verb catalogue is closed and method-owned ([Reuse established vocabulary before coining new terms](established-vocabulary-first.md){id=note:dec:8f3m5vk}), so this correspondence cannot be added by an adopter inventing a verb; it is added at the method level, as a pack ([Kind-agnostic substrate and kind packages](substrate-and-kind-packages.md){id=note:dec:w4awceq}).

The shape of the answer is bounded by two standing commitments.
A correspondence is a relationship, so it rides the authored-once typed-relation machinery, not a free-text note a checker cannot follow ([Single Source of Truth](../principles/single-source-of-truth.md){id=note:principle:8691937}).
And whether an obligation is met is never authored as state; it is computed and reported, and the verdict belongs to the Orchestrating Authority ([Compute and Report](../principles/compute-and-report.md){id=note:principle:6e7f28k}).

## Decision

- **A built-in compliance pack, opt-in by the manifest.**
  A corpus that answers to an external framework lists `compliance` in its manifest `packs`; a corpus that does not pays nothing for it.
  The pack is built-in and method-defined, like the spine and discovery packs, so a `compliance` relation means the same thing in every corpus that reads cold.

- **The pack adds typed crosswalk relations, not a kind.**
  It contributes relation endpoints, authored on a requirement or convention, naming an external control: `equivalentTo` (the obligation and the control demand the same thing, symmetric), `subsetOf` with its derived inverse `supersetOf` (the obligation covers part of what the control demands), and `intersectsWith` (the two overlap without either containing the other, symmetric).
  The three reuse OSCAL's `mapping` relationship types rather than coining new ones ([Reuse established vocabulary before coining new terms](established-vocabulary-first.md){id=note:dec:8f3m5vk}).
  The relation is authored once, on the obligation, and never on the control; a `subsetOf` runs from the obligation's coverage to the control.
  Because the control is read-only and authors nothing back, the crosswalk graph is bipartite and one-directional and so cannot cycle: `subsetOf` and its derived inverse `supersetOf` are held acyclic like any hierarchical edge, and the symmetric `equivalentTo` and `intersectsWith` are exempt, as the method's associative relations are.

- **The external control is read-only intent, brought in by existing machinery.**
  A framework's controls are represented as requirement-shaped artifacts under the framework's namespace, referenced where they live or captured locally by the cross-repository and capture machinery the method already defines ([Cross-repository inheritance and materialization](cross-repository-inheritance.md){id=note:dec:h4w9k2t}).
  The crosswalk relation resolves to such a control by its durable id, so the pack adds the relations and invents no second way to reference an artifact and no second kind for the framework side.

- **The pack adds no status, coverage, or owner field.**
  Coverage, which controls an obligation answers and which controls nothing answers, is a derived view read off the relations, never an authored fact.
  An implementation status is a tool's derived reading, not a field on the artifact.
  A control that does not apply to a system, the OSCAL `not-applicable`, is the cascade's `disinherit` with its rationale; a control met a different way, the OSCAL `alternative`, is the cascade's `replace`; both are recorded once, where the deviation already lives, and carry the rationale and attribution a bare status cannot ([Visible, attributable deviation](../requirements/system/visible-attributable-deviation.md){id=note:req:64eknb1}).

- **A crosswalk kind is deferred within the pack.**
  A complex many-to-many mapping that needs its own justification, an obligation that answers the union of two controls and the reason it does, cannot be carried by a bare edge.
  A `crosswalk` kind for that case is designed but not landed, to be added to the pack only when such mappings prove real, the same deferral discipline the risk and plan packs follow ([The risk kind](risk-kind-deferred.md){id=note:dec:ge1r86x}).
  Until then the typed relations carry the one-to-one and small many-to-one cases, and a justification that earns recording is a decision record the obligation cites.

- **Tailoring reuses the cascade.**
  Fitting a framework's baseline to a system, the OSCAL profile, is the strengthen, replace, and disinherit the cascade already provides; the pack adds no tailoring mechanism of its own.

## Forces and trade-offs

Adding relations rather than a kind is the lightest change that resolves the gap, and it clears Earned Substance where a kind would not: the correspondence is genuinely a relationship, the relation machinery already exists, and a `crosswalk` kind would duplicate the obligation, the specification, and the reference it would otherwise compose.
The cost is that a bare edge carries no per-mapping justification; that cost is paid only by the complex mapping, which is exactly the case the deferred kind is held in reserve for, and otherwise by a decision record where the reasoning earns one.

Reusing OSCAL's three relationship types costs a moment's fidelity check against the standard and buys immediate recognition for anyone who maps controls, and a clean export path, since the corpus's relations name the same distinctions the interchange format does.

Holding the framework's controls as ordinary read-only artifacts, rather than a new external-reference construct, keeps one referencing mechanism and one identity scheme.
It carries one nuance the tool must respect: a pinned external standard is meant to track the published revision, not to diverge from it, which is the opposite of the spin-out case materialization was first designed for; the import side records this, and the method only fixes that the controls are addressable intent the relation can resolve.
How a mapping carries when the standard issues a new revision, so the correspondence is not re-authored each version, is settled separately ([Crosswalk carry-forward across a framework version](framework-version-carry-forward.md){id=note:dec:07ck41n}).

Refusing to author an implementation status is the decisive boundary.
A status field would re-admit the drift the method exists to kill, a green report outrunning the build, and it would duplicate, as a weaker authored claim, what the relations and verifications already compute.
Deriving the status keeps the compliance view honest by construction, and routes `not-applicable` and `alternative` through the deviation operators, which already make a dropped or substituted obligation visible, attributed, and reasoned.

## Alternatives considered

- **Ship a `crosswalk` kind now.**
  Rejected against Earned Substance: the one-to-one and small many-to-one cases are carried by a typed edge, and a kind earns its place only for the justified many-to-many mapping, which is deferred until it proves real rather than shipped on speculation.

- **Add an authored `implementation-status` field, mirroring OSCAL `implemented-requirements` directly.**
  Rejected: it crosses the representation boundary, authoring "met" as state, and it duplicates the computed coverage and the verification verdict as a weaker, drift-prone claim.
  Status is derived and reported; the not-applicable and alternative cases are the cascade's deviations.

- **Record the correspondence as free-text prose in the obligation's `## Source`.**
  Rejected: prose is not a typed edge, so coverage cannot be computed, a crosswalk cannot be checked, and a mapping cannot be surfaced when its control changes.
  Prose remains the fallback only for an adopter who declines the pack and wants a non-checkable note.

- **Invent a new external-reference construct for framework controls.**
  Rejected against Single Source of Truth: the controls are addressable artifacts under their own namespace, reached by the existing cross-repository and capture machinery; a second referencing mechanism would be a parallel identity scheme to keep in step.

- **Coin fresh verb names for the relationship types.**
  Rejected: OSCAL's `equivalent`, `subset-of`, and `intersects-with` are the established distinctions of cross-framework mapping, and reuse buys recognition and a clean export where a coinage would buy only novelty.

## Driven by

- groundedIn: [Crosswalk intent to the frameworks it answers to](../needs/crosswalk-to-external-frameworks.md){id=note:need:5mmrydr}
- groundedIn: [Kind-agnostic substrate and kind packages](substrate-and-kind-packages.md){id=note:dec:w4awceq}
- groundedIn: [Reuse established vocabulary before coining new terms](established-vocabulary-first.md){id=note:dec:8f3m5vk}
- groundedIn: [Cross-repository inheritance and materialization](cross-repository-inheritance.md){id=note:dec:h4w9k2t}
- groundedIn: [Single Source of Truth](../principles/single-source-of-truth.md){id=note:principle:8691937}
- groundedIn: [Earned Substance](../principles/earned-substance.md){id=note:principle:yecemfe}
- groundedIn: [Proportionality](../principles/proportionality.md){id=note:principle:es0vhzn}
- groundedIn: [Compute and Report](../principles/compute-and-report.md){id=note:principle:6e7f28k}

## Worked example

An adopter answers to OWASP ASVS.
Sett imports the catalog once, pinned, as read-only artifacts under an `owasp-asvs` namespace (the paths and ids below are illustrative, not artifacts of this corpus).
The adopter's own constraint requirement, "when an agent requests a path outside the session root, the system shall deny it," records its correspondence as a relation naming the control by its durable id:

```markdown
## Relations

- equivalentTo: ASVS V1.2.3
  → owasp-asvs/v5.0.0/requirements/system/v1-2-3-path-confinement.md
  (id owasp-asvs:req:k4w7n9t)
```

A sandbox service with no filesystem drops the obligation with a `disinherit` deviation and its rationale; that control reads as not-applicable for the sandbox, with the reason attached.
Nothing authors a status: coverage of ASVS, and each control's implementation status, are computed from these relations, the deviations, and the verifications.
