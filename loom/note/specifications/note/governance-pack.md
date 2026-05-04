---
id: note:spec:gfz6q22
name: The governance pack
kind: specification
status: current
authority: []
---

This specification fixes the governance pack: an opt-in built-in kind package for the governing instruments an organization authors to direct itself.
It declares the pack's three kinds, policy, standard, and procedure, each with its id kind-segment, the per-kind frontmatter and body sections it adds beyond the common envelope, and the relation endpoint rows it contributes to the verb catalogue.

It extends [The substrate](substrate.md){id=note:spec:tkhd63e}, which fixes the file envelope, the identity scheme, the conformance floor, the universal lifecycle, the relation machinery, the citation surfaces, the conformance profiles, the pack mechanism, and the manifest.
The substrate's rules are not restated here; this specification supplies only what the governance pack adds on top of them.
The pack is enabled by naming `governance` in the manifest `packs`; a corpus that does not is unaffected by it.

## The three kinds

| Kind | Kind-segment | Role |
|---|---|---|
| policy | `pol` | A mandated direction, signed and owned, that mandates a set of obligations. |
| standard | `std` | A compulsory mechanism, format, or threshold the organization imposes on itself, derived from a policy. |
| procedure | `proc` | The ordered, role-assigned steps that carry a policy or standard out when a trigger fires. |

Each kind-segment is fixed here and agrees with the `kind` field at minting, per the substrate's identity rule.
Every kind carries the uniform opaque id; no kind carries a slug.

## Per-kind frontmatter

The fields below are added per kind, beyond the common required envelope (`id`, `name`, `kind`, `status`) and the optional common fields the substrate fixes.

| Kind | Field | Required | Value |
|---|---|---|---|
| policy | `approver` | required | A citation, or a list of citations, of the persona artifacts naming the role authorized to approve the instrument; the standard citation form written as a quoted YAML string. The role is the authority; the person who fills it is incidental. |
| policy | `approver_name` | optional | A literal name of the individual who approved, recorded beside the role where an adopter wants the person on the record. |
| policy | `effective_date` | required at `current` and `obsolete`; omitted otherwise | An RFC 3339 date, or date-time ending in `Z`, at which the instrument takes force. Omitted while `tbd`, `draft`, or `rejected`, because the instrument is not yet in force. |
| policy | `review_due` | optional | An RFC 3339 date by which the instrument is next reviewed; a lapsed date is a reportable signal, not an ill-formed artifact. |
| standard | `approver` | required | As for policy. |
| standard | `approver_name` | optional | As for policy. |
| standard | `effective_date` | required at `current` and `obsolete`; omitted otherwise | As for policy. |
| standard | `review_due` | optional | As for policy. |
| procedure | `owner` | required | A citation of the persona artifact naming the role that owns and runs the procedure. |
| procedure | `approver` | optional | As for policy, where a controlled procedure is signed off; optional because an operational procedure may rest on its owner alone. |
| procedure | `effective_date` | optional | As for policy, where a procedure is signed off. |
| procedure | `review_due` | optional | As for policy. |

`approver` and `owner` are persona citations by the same rule a need's `persona` field follows: the role is named once as an artifact and reused, never re-described per instrument.

## Body structure by kind

Every body opens with an unheaded lead, a single statement of the artifact's substance, and the designation is never repeated as a body heading.
The sections below are level-2 headings in the canonical order shown.
At `bare` the lead alone is required; the sections marked required are what `standard` expects.

### policy

| Section | Req/Opt | Content |
|---|---|---|
| *(lead)* | required | The mandated direction: what the instrument requires, and why it is in force. No ordered steps and no mechanism choice; those are a procedure and a standard beneath it. |
| `## Authority` | optional | Commentary on the approval, and a citation to the external record of the approval event, kept by the Orchestrating Authority. The `approver` field names the role; this section is its evidence and commentary, the counterpart to a specification's `## Authority`. |
| `## Relations` | optional | `enacts` the principle the policy serves, where one grounds it; a crosswalk to an external control where the compliance pack is enabled. A policy authors no downward edge to the obligations it mandates: those are authored on their own ends through `implements`, and the policy reads them off the derived `implementedBy`. |

### standard

| Section | Req/Opt | Content |
|---|---|---|
| *(lead)* | required | The compulsory mechanism, format, or threshold, stated declaratively; it may name the mechanism, because the agreed mechanism is its substance. It carries no external force: a mechanism an external force imposes is a constraint requirement crosswalked to that force, not a standard. |
| `## Authority` | optional | As for policy: the approval evidence and commentary. |
| `## Relations` | required | `implements` the policy it makes concrete; `enacts` a principle where one grounds it; a crosswalk to an external control where the compliance pack is enabled. |

### procedure

| Section | Req/Opt | Content |
|---|---|---|
| *(lead)* | required | The procedure's purpose and the outcome it produces. |
| `## Trigger` | required | The condition that initiates the procedure. |
| `## Steps` | required | The ordered steps, each naming the role that performs it. A step effects a change in the world; a step that yields a verdict, names a verification method, or carries an expected result is a verification mis-filed, not a procedure step. |
| `## Roles` | optional | The roles the steps assign, gathered once where naming them aids the steps. |
| `## Relations` | required | `implements` the policy or standard it carries out. A procedure is `verifiedBy` a drill verification, a derived view; the verification authors `verifies`. |

## Verb endpoint rows

The pack contributes the endpoint rows below to the substrate's verb catalogue.
The substrate fixes each verb's name, direction, and derived inverse; the pack supplies which kinds the verb joins, and the corpus's effective catalogue is the union of its enabled packs' rows.
Each edge is authored once, on the dependent end, and reads as a true sentence `<dependent> <verb> <governing>`.

| Verb | Authored on | To | Inverse |
|---|---|---|---|
| `implements` | standard, procedure, requirement | policy or standard | `implementedBy` |
| `enacts` | policy, standard | principle | `enactedBy` |
| `verifies` | verification | procedure | `verifiedBy` |

`implements` is the governance verb: a standard implements the policy it makes concrete, a procedure implements the policy or standard it carries out, and a constraint requirement that is a control implements the standard or policy it answers.
Its inverse `implementedBy` is the coverage view, the set of standards, procedures, and obligations that carry an instrument out, read off the instrument without the edge being authored twice.

`enacts` is the substrate verb the spine pack sources from a requirement or a convention; the governance pack adds policy and standard as further sources, so a governing instrument may name the principle it puts into practice.
The `verifies` row adds procedure as a target, so a drill may verify that a procedure holds, the procedure being a thing done rather than a thing asserted.

The decision edges `groundedIn`, `amends`, and `decidedBy` are substrate-level; the governance pack supplies their endpoint kinds where a decision shapes a policy, standard, or procedure, but does not redeclare the verbs.

## Rationale

Declaring the governance pack in its own specification, separate from the substrate and from the spine, is what lets the kinds an organization earns only when it governs ride the same machinery without weighting every corpus with them.
The three kinds are held together because they share a lifecycle the spine kinds do not: authored by a governance role, ratified and re-attested on a review cadence, and read by an auditor, against the obligations they put in force.

A control is deliberately not among them: a control is a measure, carried in Note by a constraint requirement crosswalked to its source, so the pack adds the instruments an organization authors and leaves the external catalog to the compliance pack.

A `process`, the coarser cross-functional flow above a procedure, is recognized but deferred: this version carries the procedure and holds the process as a later addition to the pack, the boundary the Procedure term and the governing decision record draw ([Governance as an opt-in pack](../../decisions/governance-pack.md){id=note:dec:59ptf2z}).

## Relations

- satisfies: [Declarable kind packages](../../requirements/system/declarable-kind-packages.md){id=note:req:ekfkzzt}
- satisfies: [Work in a declared kind vocabulary](../../requirements/stakeholder/work-in-a-declared-kind-vocabulary.md){id=note:req:jkkpqbv}
- decidedBy: [Governance as an opt-in pack](../../decisions/governance-pack.md){id=note:dec:59ptf2z}
