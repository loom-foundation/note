---
id: note:dec:07ck41n
name: Crosswalk carry-forward across a framework version
kind: decision
status: current
decided: 2026-07-02T00:00:00Z
---

When a framework issues a new version, its controls are materialized side by side as new read-only artifacts under the new version namespace, and the lineage from each new control to the prior-version control it replaces is recorded once, on the new control, with the existing `supersedes` citation; the obligation's crosswalk edge is never moved or rewritten.
Carry-forward of a mapping to the new version, and the changed, added, and removed report, are a derived view read off the supersession chain and the two controls' own text, never an authored status.
The Statement of Applicability rides the same chain: a `disinherit` or `replace` deviation authored against a prior-version control is reported against that control's successor, surfaced for re-justification when the control changed.

## Context

The compliance pack settled how an obligation records its correspondence to an external control: a typed crosswalk edge (`equivalentTo`, `subsetOf`, `intersectsWith`) authored once on the obligation, resolving to a read-only, version-pinned control by its durable id, with coverage derived and never authored ([The compliance crosswalk pack](compliance-crosswalk-pack.md){id=note:dec:ve053yf}).
What that decision left open is the version bump.
A framework revises (ISO 27001:2022 after :2013; ASVS v5.1.0 after v5.0.0), and the new edition is materialized as fresh read-only artifacts under the new version namespace by the materialization machinery ([Cross-repository inheritance and materialization](cross-repository-inheritance.md){id=note:dec:h4w9k2t}).
Because a faithful frozen mirror keeps the upstream's id and a re-homed copy takes a new one, the new edition's controls carry new opaque ids by construction; they are not the prior edition's artifacts.
The adopter's obligations still carry edges to the prior edition's control ids.

The corpus already promises that mappings carry across this bump without redoing them each revision ([Mapping Survives Framework Version Change](../needs/crosswalk-to-external-frameworks/gain-mapping-survives-framework-version-change.md){id=note:gain:c59jzs3}), but the mechanism was unspecified.
The shape of the answer is bound by three standing commitments.
Whether a mapping carries, and whether a control changed, is computed and reported, never authored as state ([Compute and Report](../principles/compute-and-report.md){id=note:principle:6e7f28k}).
The fact of "which control this is" and "which control replaced which" each has exactly one home, cited elsewhere rather than restated ([Single Source of Truth](../principles/single-source-of-truth.md){id=note:principle:8691937}).
And the bar for a new field or kind is high: the lineage between two control versions is the same relationship the method already carries with `supersedes` and `superseded_by`, so a new construct must justify itself against that reuse ([Earned Substance](../principles/earned-substance.md){id=note:principle:yecemfe}).

## Decision

- **Cross-version lineage is the existing `supersedes` citation, authored once on the new control.**
  When a new edition is materialized, each new-version control that continues a prior-version control records that lineage with a `supersedes` citation in its own frontmatter, naming the prior control by its durable id; because the prior-version control is a read-only frozen mirror, its `superseded_by` is not authored, the read-only exception ([The substrate](../specifications/note/substrate.md){id=note:spec:tkhd63e}) to the authored supersession pair ([Universal artifact lifecycle and its transitions](artifact-lifecycle.md){id=note:dec:gfwq0mv}), and the retired side's view is derived from the successor's `supersedes`.
  The citation is authored on the framework side, by whoever materializes the new edition, because that is the one party with knowledge of what replaced what, and it gives the lineage a single home rather than scattering it across every adopter's edges.
  Authoring nothing means no lineage: a new control with no `supersedes` simply derives as added, and a prior control with no successor derives as removed, which is the safe loud default rather than a silent guess.

- **The crosswalk edge is never moved, re-pointed, or rewritten.**
  The obligation's edge stays authored against the prior-version control's id exactly as the adopter wrote it; it is the adopter's deliberate semantic claim and the authoritative record of what they evaluated.
  Carry-forward to the new edition is computed by following the prior control's `supersedes` chain to its successor, transitively across intervening editions, so an edge to a v5.0.0 control resolves through v5.1.0 to v6.0.0 when each hop is recorded; a broken hop halts the chain and surfaces as a gap rather than a guess.
  No tool rewrites the edge from a vendor delta: a rewrite would destroy the single authored source and erase the provenance an audit rests on.

- **Carry-forward, change, addition, and removal are one derived report.**
  From the supersession chain and the two controls' own materialized text, the report is computed, never authored: an obligation's edge whose prior control has a single successor *carries forward* to that successor; multiple successors (a one-to-many split) report all successors and flag the edge for review, the tool choosing none; two prior controls sharing one successor (a many-to-one merge) both carry to it; a new-version control with no inbound supersession is *added*, and an uncovered one is a gap; a prior control whose edge has no successor in the new edition is a *removal* to surface.
  Whether a carried control *changed* is a derived signal from comparing the prior and successor control bodies, not a field on the citation; textual identity is reported as a signal toward "no review needed," and any divergence is reported as "review this mapping," but the method asserts only the lineage, leaving the equivalence verdict to the Orchestrating Authority.

- **The lineage citation records succession, not retirement.**
  A `supersedes` between two control editions records that the new control continues the old one; it does not by itself set the prior control's `status`, because an adopter in a transition period answers to both editions at once.
  The prior edition's controls keep their own lifecycle: they are retired to `obsolete` only when the adopter stops answering to that edition, which is the adopter's call, not an effect of the citation.

- **The Statement of Applicability rides the same chain.**
  A `disinherit` (not-applicable) or `replace` (met another way) deviation is authored against a control by its id ([Scope and cascade representation](scope-and-cascade-representation.md){id=note:dec:e3v7s8q}); at a version bump it is reported against that control's successor by the same supersession walk, so the exception and its rationale carry forward with the mapping rather than vanishing.
  A deviation whose control changed is surfaced for re-justification exactly as a changed mapping is; a deviation whose control was removed is surfaced as a removal, so a dropped exception is never silent.

- **No new field, kind, or identity scheme is added.**
  The mechanism is the existing `supersedes` and `superseded_by` citations plus a derivation rule the tool runs; carry-forward is reported, the framework-native key is never a resolution path, and the opaque id remains the one identity.

## Forces and trade-offs

Reusing `supersedes` rather than coining a cross-version-identity construct is the lightest change that closes the gap, and it clears Earned Substance: the lineage between two editions is genuinely "the new artifact replaces the old," which is exactly what `supersedes` already means ([Reuse established vocabulary before coining new terms](established-vocabulary-first.md){id=note:dec:8f3m5vk}), so a new construct would duplicate it and stand up a second identity axis to keep in step.
The cost is that the field's canonical story is lifecycle retirement, so the decision must say plainly that a cross-version citation does not retire the prior control; that one sentence is cheaper than a parallel mechanism.

Authoring the lineage once, on the framework side, keeps carry-forward to a single home and leaves every adopter's edges untouched, so the same materialized edition serves all adopters and no adopter re-keys anything for an unchanged control.
The cost is that an edition materialized with no supersession citations yields a wall of false gaps; that cost falls in the safe direction, a loud over-report rather than a silent green, and the report distinguishes "uncovered because new" from "no lineage authored yet" so the materializer is nudged to record it.

Deriving "changed versus unchanged" from the control bodies, rather than authoring a classification, keeps the report honest by construction, but textual identity is only a signal: a control can be byte-identical yet shift in scope through a changed reference or definition.
The method therefore claims only the lineage and surfaces the comparison; the equivalence verdict stays with the Orchestrating Authority, and the conservative reading is to treat a control as needing review until shown unchanged.

Refusing to rewrite the adopter's edges preserves the authored source and its provenance at the cost that carry-forward is a report the adopter acts on rather than an automatic edit; that is the intended boundary, since the value of the edge is that a human asserted it.

## Alternatives considered

- **Rewrite the obligation's edges with a published vendor delta.**
  Rejected against Single Source of Truth and the representation boundary: rewriting destroys the adopter's authored claim and erases the provenance an audit needs, a partial delta leaves an undetectable half-migrated state, and it makes the tool an author of the very intent it exists to report on ([Compute and Report](../principles/compute-and-report.md){id=note:principle:6e7f28k}).
  Carry-forward belongs in the lineage between the controls, authored once, not scattered as rewrites across every adopter's files.

- **Resolve the crosswalk edge by the control's framework-native key (for example the string `V1.2.3`) instead of the opaque id.**
  Rejected against Single Source of Truth: a framework-native key is a second home for "which control this is," and keys are renumbered, split, merged, and even reused for a different control across editions, so an edge would silently re-bind to the wrong control with no warning.
  The opaque id exists precisely to prevent that silent semantic drift.

- **Add a stable cross-version control-identity construct shared by both editions' artifacts.**
  Rejected against Earned Substance: `supersedes` already expresses "this control succeeds that one," so a new construct earns nothing, adds a field and an identity axis to maintain, and forces an ambiguous assignment on every split and merge that the supersession graph reports without guessing.

- **Author a per-version "carried forward" status on the edge or a re-attestation field on the deviation.**
  Rejected: it re-admits authored coverage state, the drift the pack decision exists to kill, and creates a second source beside the derived report.
  Accountability for accepting a carry-forward rests on Git provenance and the deviation's own rationale, as the cascade already refuses a self-declared author field ([Scope and cascade representation](scope-and-cascade-representation.md){id=note:dec:e3v7s8q}); where a dated re-review note is later wanted, the existing optional `last_reviewed` field carries it without a new one.

## Driven by

- groundedIn: [Crosswalk intent to the frameworks it answers to](../needs/crosswalk-to-external-frameworks.md){id=note:need:5mmrydr}
- groundedIn: [The compliance crosswalk pack](compliance-crosswalk-pack.md){id=note:dec:ve053yf}
- groundedIn: [Cross-repository inheritance and materialization](cross-repository-inheritance.md){id=note:dec:h4w9k2t}
- groundedIn: [Scope and cascade representation](scope-and-cascade-representation.md){id=note:dec:e3v7s8q}
- groundedIn: [Reuse established vocabulary before coining new terms](established-vocabulary-first.md){id=note:dec:8f3m5vk}
- groundedIn: [Compute and Report](../principles/compute-and-report.md){id=note:principle:6e7f28k}
- groundedIn: [Single Source of Truth](../principles/single-source-of-truth.md){id=note:principle:8691937}
- groundedIn: [Earned Substance](../principles/earned-substance.md){id=note:principle:yecemfe}

## Worked example

An adopter answers to OWASP ASVS v5.0.0, materialized under an `owasp-asvs/v5.0.0/` namespace, and has authored an edge from its own path-confinement obligation to control V1.2.3, plus a `disinherit` of a control its sandbox cannot apply.
ASVS v5.1.0 ships and is materialized side by side under `owasp-asvs/v5.1.0/`, with new opaque ids.
The materializer records lineage on the new controls:

```markdown
---
id: owasp-asvs:req:p9w2k4n
materialized:
  from: git+https://github.com/OWASP/ASVS.git
  at: v5.1.0
  commit: 1c4f9ab
  on: 2026-06-21
supersedes: "[ASVS V1.2.3 (v5.0.0)](../../v5.0.0/requirements/system/v1-2-3-path-confinement.md){id=owasp-asvs:req:k4w7n9t}"
---
```

The adopter touches no obligation file.
A tool walks each edge's prior control to its v5.1.0 successor and reports: V1.2.3 carries forward, with the two control bodies textually identical, so no review is flagged; a reworded control carries with a "review this mapping" flag; a brand-new v5.1.0 control with no `supersedes` is an uncovered gap; and the disinherited control, whose v5.1.0 successor exists, carries its not-applicable rationale forward, flagged for re-justification only because its text changed.
Nothing authors a "carried" or "covered" status; the whole picture is derived from the supersession chain, the controls' text, and the deviations.
