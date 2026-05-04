# Crosswalking to control frameworks

How an adopter whose system answers to an external control framework, a security standard, a regulatory catalog, or a customer's control set, maps its own obligations to that framework and shows coverage, without keeping a spreadsheet beside the corpus.
This is orientation and applied guidance, not normative text; the binding rules live in [The compliance crosswalk pack](../loom/note/decisions/compliance-crosswalk-pack.md){id=note:dec:ve053yf}, with the tool-side import and reporting machinery recorded in Sett's own compliance-tooling decision.

## What this is, and when to reach for it

A control framework is someone else's catalog of obligations you must satisfy: NIST 800-53, OWASP ASVS, ISO 27001, an internal policy set, a customer's security questionnaire.
The governance practice for answering to one is the Requirements Traceability Matrix, each of your obligations linked to the control it satisfies, with a status and an owner, and the machine-readable form of that practice is OSCAL.

Most of what you need, Note already has, and you should reach for it before reaching for the pack:

- A **control you must meet** is a constraint-typed Requirement, with the framework named in its `## Source`.
- The **mechanism that meets it** is a Specification; the **check** is a Verification.
- **Tailoring a framework's baseline per system**, the OSCAL profile, is the cascade ([Scope and cascade](scope-and-cascade.md)).
- The **traceability matrix itself** is the corpus's own relation graph, computed from the files.

The one thing the spine does not give you is a typed, checkable correspondence from your obligation to a specific *external* control, and a representation for those external controls to point at.
That is what the **compliance pack** adds, and the rest of this document is how to adopt and use it.

If you answer to no external framework, you need none of this; the pack is opt-in and a corpus that does not enable it pays nothing for it.

## The model in one line

> Your **obligation** (a Requirement or Convention) records a typed **crosswalk** to an external **control** (a read-only, imported artifact). Coverage and status are **computed** from those crosswalks, the verifications, and the cascade, never authored.

Nothing in the pack is a status field. You author the *correspondence*; the matrix, the gaps, and each control's implementation status are derived views.

## Day one: enable the pack

Add `compliance` to your manifest's `packs` (alongside `spine`, and `discovery` if you use it):

```markdown
---
methodVersion: 0.5.0
namespace: acme
profile: standard
packs: [spine, compliance]
---
```

That one line makes the crosswalk relations legal in your corpus.
It adds no new status, no new kind to author, and no obligation on a corpus that answers to no framework.
The pack and the relations it adds are fixed in [Typed framework crosswalk](../loom/note/requirements/system/typed-framework-crosswalk.md){id=note:req:p2ry9tv}.

## Bring the framework in

You do not re-type the catalog.
A framework is imported once, as read-only, provenance-bearing requirement-shaped artifacts under the framework's own namespace, pinned to the version you adopted (Sett's framework-catalog-import requirement).
The import is the framework-shaped case of the interchange the tool already performs, landed by the same capture machinery the method uses for any inherited intent ([Cross-repository inheritance and materialization](../loom/note/decisions/cross-repository-inheritance.md){id=note:dec:h4w9k2t}).

Imported controls land under their namespace, each carrying its provenance:

```
loom/note/
└── owasp-asvs/
    └── v5.0.0/
        └── requirements/system/
            └── v1-2-3-path-confinement.md   # owasp-asvs:req:…, provenance: framework, version, date
```

Two things to know about an imported framework:

- It is **read-only**. You never hand-edit an imported control. When the standard publishes a new version, you re-import; you do not patch the frozen copy.
- It is **pinned to track, not to diverge**. Unlike intent you materialize at a spin-out (which is meant to drift from its former parent), an imported standard is meant to follow the published revision, so a revision is a fresh import.

You may import a full **catalog** or a tailored **profile** (the baseline your system actually answers to).

## Crosswalk your obligation to a control

You record the correspondence on your obligation, in its `## Relations`, with one of three typed verbs that reuse OSCAL's mapping relationship types:

| Verb | Use when | Direction |
|---|---|---|
| `equivalentTo` | your obligation and the control demand the same thing | symmetric |
| `subsetOf` (inverse `supersetOf`) | your obligation covers part of what the control demands | obligation → control |
| `intersectsWith` | the two overlap, neither contains the other | symmetric |

The relation is authored **once, on your obligation**, never on the imported control, and it resolves to the control by its durable id.

A worked example. Your own constraint requirement:

```markdown
---
id: acme:req:7k2m9q0
name: Agent path confinement
kind: requirement
level: system
type: constraint
status: current
---

When an agent requests a path outside the session root, the system shall deny the access.

## Source

ACME-SEC-POLICY §4.2.

## Relations

- equivalentTo: [ASVS V1.2.3](../../owasp-asvs/v5.0.0/requirements/system/v1-2-3-path-confinement.md){id=owasp-asvs:req:k4w7n9t}
```

An obligation may carry more than one crosswalk where it answers to controls in more than one framework; each is its own line.
A Convention may crosswalk too, for the controls that bind how you author rather than what the system does.

## Tailor the baseline per system (this is the OSCAL profile, for free)

A framework rarely applies whole to every system.
Tailoring is the cascade you already use, not a new mechanism:

- A system that needs **more** than the baseline strengthens the obligation: a silent `add`.
- A system that meets a control **a different way** records a `replace` with its rationale. This is OSCAL's `alternative`.
- A system the control **does not apply to** drops it with a `disinherit` and its rationale. This is OSCAL's `not-applicable`.

Because the deviation carries a reason and is attributed through Git, a not-applicable or alternative control is *more* legible than a bare OSCAL status: you can always see who excepted it and why ([Scope and cascade](scope-and-cascade.md)).

```markdown
## Deviation

- disinherit [Agent path confinement](../../requirements/system/agent-path-confinement.md){id=acme:req:7k2m9q0} from acme.
  Rationale: the analytics sandbox has no filesystem surface; confinement is a category error here.
```

## The compliance view is generated, not kept

This is the load-bearing habit.
You author obligations, crosswalks, deviations, and verifications.
You do **not** maintain a `controls.yaml` or an OSCAL document by hand; the tool generates them from your corpus, so the report can never disagree with the system it describes (Sett's computed-compliance-reporting requirement).

What the tool derives:

- **The coverage matrix and the gaps**: which controls your obligations answer, and which controls nothing yet answers (your plan of action).
- **Each control's implementation status**, across the full OSCAL set, computed rather than declared:

  | OSCAL status | derived from |
  |---|---|
  | `implemented` | a covering obligation whose verification passes |
  | `planned` | a covering obligation with no design or check yet |
  | `partial` | incomplete coverage, or a verification failing or merely present rather than passing |
  | `not-applicable` | a control dropped by a `disinherit` deviation |
  | `alternative` | a control met another way by a `replace` deviation |

- **An OSCAL export**: a `component-definition` whose `implemented-requirements` carry the derived status and owner, for an assessor to consume, with no enterprise compliance platform to stand up.

## What is deliberately *not* a field

Three things you might expect to author, you do not, by design:

- **Implementation status** is derived (the table above), never a field you set. Authoring "implemented" would let a green report outrun the build; the status is read from your verifications and deviations instead.
- **The responsible party** is drawn from the record, your commit history and code-owners, never a field on the artifact.
- **A "control" kind.** A control is just a Requirement (the obligation), a Specification (the mechanism), or a Convention (the agreed practice). The pack adds the *correspondence*, not a redundant kind.

A complex many-to-many mapping that needs its own justification (your one obligation answers the union of two controls, and the reason matters) is not yet a first-class artifact; record the reasoning in a Decision the obligation cites. A dedicated `crosswalk` kind for that case is designed but deferred until such mappings prove common.

## A note on threat taxonomies

A control catalog (OWASP ASVS, NIST 800-53) is what you crosswalk to.
A *threat* taxonomy (the OWASP Agentic Top 10, where "excessive agency" is a risk, not a control) is a different thing: your obligation does not crosswalk to it, it *mitigates* it. Mitigation is carried by the risk model, not the compliance pack; pick the pack that matches the framework you are mapping.

## Normative sources

The orientation here restates what these fix:

- [The compliance crosswalk pack](../loom/note/decisions/compliance-crosswalk-pack.md){id=note:dec:ve053yf}: the opt-in pack, the three crosswalk relations, the relations-not-a-kind choice, and the no-authored-status boundary.
- Sett's compliance-tooling decision, on the tool side: import as materialized read-only artifacts, derived coverage and status, OSCAL export, and the generated-not-authored discipline.
- [Intent mappable to external frameworks](../loom/note/requirements/stakeholder/mappable-to-external-frameworks.md){id=note:req:ddh4kfx} and [Typed framework crosswalk](../loom/note/requirements/system/typed-framework-crosswalk.md){id=note:req:p2ry9tv}: the obligations the pack satisfies.
- [Crosswalk intent to the frameworks it answers to](../loom/note/needs/crosswalk-to-external-frameworks.md){id=note:need:5mmrydr}: the need this all serves.

See also [profiles.md](profiles.md) for choosing a rigor profile, and [The substrate](../loom/note/specifications/note/substrate.md){id=note:spec:tkhd63e} for the identity and relation machinery the crosswalk rides.
