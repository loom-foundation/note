---
id: note:spec:kv2t9fm
name: The compliance pack
kind: specification
status: current
authority: []
---

This specification fixes the compliance pack: an opt-in built-in package that adds the typed crosswalk relations by which an obligation records its correspondence to a control in an external framework, distinguishing equivalence, a subset relationship, and a partial overlap.
It declares no kind: the pack contributes relation endpoint rows only, and the external controls those relations target are ordinary read-only artifacts brought in by the capture machinery the method already defines.

It extends [The substrate](substrate.md){id=note:spec:tkhd63e}, which fixes the file envelope, the identity scheme, the relation machinery, the pack mechanism, and the manifest; the substrate's rules are not restated here.
The pack is enabled by naming `compliance` in the manifest `packs`; a corpus that does not is unaffected by it.

## What the pack adds

The pack adds relations, not kinds ([The compliance crosswalk pack](../../decisions/compliance-crosswalk-pack.md){id=note:dec:ve053yf}).

A framework's controls are represented as requirement-shaped, read-only artifacts under the framework's own namespace, referenced where they live or captured locally as frozen copies by the cross-repository and capture machinery ([Cross-repository inheritance and materialization](../../decisions/cross-repository-inheritance.md){id=note:dec:h4w9k2t}).
A crosswalk relation resolves to such a control by its durable id, exactly as any reference does; the pack invents no second way to reference an artifact and no second kind for the framework side.

The pack adds no status, coverage, or owner field.
Which controls an obligation answers, and which controls nothing answers, is a derived view read off the relations; an implementation status is a tool's derived reading; a control that does not apply is the cascade's `disinherit` with its rationale, and a control met a different way is the cascade's `replace`, each recorded once where the deviation already lives ([Scope and cascade](scope-and-cascade.md){id=note:spec:1r673tc}).

## Verb endpoint rows

The pack contributes the endpoint rows below to the substrate's verb catalogue.
The substrate fixes each verb's name, direction, and derived inverse; the pack supplies which kinds the verb joins, and the corpus's effective catalogue is the union of its enabled packs' rows.
The three verbs reuse OSCAL's mapping relationship types (`equivalent`, `subset-of`, `intersects-with`) rather than coining new ones.

| Verb | Authored on | To | Inverse |
|---|---|---|---|
| `equivalentTo` | requirement, convention | an external control | (symmetric) |
| `subsetOf` | requirement, convention | an external control | `supersetOf` |
| `intersectsWith` | requirement, convention | an external control | (symmetric) |

When the governance pack is co-enabled, the pack contributes the same three rows sourced from `policy` and `standard`, so a governing instrument may record its own correspondence, as the governance pack's body sections anticipate ([The governance pack](governance-pack.md){id=note:spec:gfz6q22}).

`equivalentTo` states that the obligation and the control demand the same thing; `subsetOf` states that the obligation covers part of what the control demands, authored from the obligation's coverage to the control, with `supersetOf` its derived inverse; `intersectsWith` states that the two overlap without either containing the other.
Each relation is authored once, on the obligation, and never on the control; the control is read-only and authors nothing back, so the crosswalk graph is bipartite and cannot cycle.
`subsetOf` and its derived inverse are held acyclic like any hierarchical edge; the symmetric `equivalentTo` and `intersectsWith` are exempt, as the method's associative relations are.

## Carry-forward across framework versions

When a framework issues a new version, its controls are materialized side by side as new read-only artifacts under the new version namespace, and each new control that continues a prior one records that lineage once, in its own frontmatter, with the existing `supersedes` citation; the obligation's crosswalk edge is never moved, re-pointed, or rewritten.
Carry-forward, change, addition, and removal are one derived report read off the supersession chain and the two controls' own text, and a `disinherit` or `replace` deviation authored against a prior-version control is reported against that control's successor by the same walk ([Crosswalk carry-forward across a framework version](../../decisions/framework-version-carry-forward.md){id=note:dec:07ck41n}).

## Tailoring

Fitting a framework's baseline to a system is the cascade's strengthen, replace, and disinherit; the pack adds no tailoring mechanism of its own ([Scope and cascade](scope-and-cascade.md){id=note:spec:1r673tc}).

## Deferred within the pack

A `crosswalk` kind, for the complex many-to-many mapping that needs its own justification, is designed but not landed; until it proves real, the typed relations carry the one-to-one and small many-to-one cases, and a justification that earns recording is a decision record the obligation cites ([The compliance crosswalk pack](../../decisions/compliance-crosswalk-pack.md){id=note:dec:ve053yf}).

## Rationale

Declaring the pack in its own specification, though it introduces no kind, keeps the pack mechanism uniform: a corpus's effective verb catalogue is the union of its enabled packs' declared rows, each pack fixed in one specification a checker reads.
Holding the pack to relations keeps the lightest change that closes the gap: the correspondence is genuinely a relationship, the controls are ordinary addressable intent, and everything that would have been a field (status, coverage, applicability) is a derived view or an existing deviation operator.

## Relations

- satisfies: [Typed framework crosswalk](../../requirements/system/typed-framework-crosswalk.md){id=note:req:p2ry9tv}
- satisfies: [Mappable to external frameworks](../../requirements/stakeholder/mappable-to-external-frameworks.md){id=note:req:ddh4kfx}
- satisfies: [Declarable kind packages](../../requirements/system/declarable-kind-packages.md){id=note:req:ekfkzzt}
- decidedBy: [The compliance crosswalk pack](../../decisions/compliance-crosswalk-pack.md){id=note:dec:ve053yf}
- decidedBy: [Crosswalk carry-forward across a framework version](../../decisions/framework-version-carry-forward.md){id=note:dec:07ck41n}
