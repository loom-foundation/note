---
id: note:spec:6kjja5r
name: The spine pack
kind: specification
status: current
authority: []
---

This specification fixes the spine pack: the default built-in kind package, the sharp, V-model-shaped trace spine and the kinds that anchor it.
It declares the pack's eleven kinds, each with its id kind-segment, the per-kind frontmatter and body sections it adds beyond the common envelope, and the relation endpoint rows it contributes to the verb catalogue.

It extends [The substrate](substrate.md){id=note:spec:tkhd63e}, which fixes the file envelope, the identity scheme, the conformance floor, the universal lifecycle, the relation machinery, the term-relation set, the citation surfaces, the conformance profiles, the pack mechanism, and the manifest.
The substrate's rules are not restated here; this specification supplies only what the spine pack adds on top of them.

The spine pack is the default a corpus carries when it names no pack ([The default spine pack](../../decisions/spine-pack.md){id=note:dec:4tzn3av}); it is the package the substrate's pack mechanism resolves to absent any other configuration.

## The eleven kinds

The pack declares eleven kinds: need, requirement, specification, decision, verification, acceptance-criterion, term, persona, convention, principle, and context.

| Kind | Kind-segment | Role on or around the spine |
|---|---|---|
| need | `need` | A want, recorded in the persona's terms. |
| requirement | `req` | The obligation that addresses a need. |
| specification | `spec` | The design commitment that satisfies a requirement. |
| verification | `ver` | The executable check that confirms a design or obligation holds. |
| acceptance-criterion | `ac` | The solution-free condition under which a requirement or need is acceptable. |
| decision | `dec` | A recorded choice that shaped the spine, and its why. |
| convention | `conv` | An agreed coordination rule binding the making of artifacts. |
| term | `term` | A word the corpus uses with one specific meaning. |
| persona | `persona` | A class of actor a need is wanted by. |
| principle | `principle` | A transverse normative anchor that guides judgment. |
| context | `ctx` | The holistic boundary statement of what is in and out of scope. |

Each kind-segment is fixed here and agrees with the `kind` field at minting, per the substrate's identity rule.
Every kind carries the uniform opaque id; no kind carries a slug ([Uniform opaque identity](../../decisions/identity-and-designations.md){id=note:dec:jhgkwja}).

## Per-kind frontmatter

The fields below are added per kind, beyond the common required envelope (`id`, `name`, `kind`, `status`) and the optional common fields the substrate fixes.
A kind not listed adds no frontmatter beyond the envelope.

| Kind | Field | Required | Value |
|---|---|---|---|
| need | `persona` | required | A citation, or a list of citations, of the persona artifacts the need is wanted by; each entry is the standard citation form (name label, relative path, id) written as a quoted YAML string; the id is the authoritative part, the label and path refreshable conveniences; by reference rather than free text ([Terms and personas as first-class, scoped kinds](../../decisions/terms-and-personas-as-kinds.md){id=note:dec:t4w8k2n}). |
| need | `validation` | optional | One of `assumed`, `inferred`, `observed`, `established`, `invalidated`: how validated the need's embedded claim is, drawn from the classification the Validation term defines; the evidence behind a raise is cited in the artifact's `## Source` ([Validation evidence in the Source](../../conventions/validation-evidence-in-source.md){id=note:conv:8wafpx1}). Omit when the claim is not graded ([The validation field](../../decisions/validation-field.md){id=note:dec:vf2m8qe}). |
| requirement | `level` | optional | `stakeholder` or `system`. A profile may require it. |
| requirement | `type` | optional | `functional`, `non-functional`, or `constraint`. A profile may require it, `type` where the solution-free check is enforced. |
| decision | `decided` | required at `current` and `obsolete`; omitted otherwise | An RFC 3339 UTC timestamp ending in `Z`; the wall-clock time may be `00:00:00` when unrecorded. Omitted while `tbd`, `draft`, or `rejected`, because the ratification event has not occurred ([Proposable decisions](../../decisions/proposable-decisions.md){id=note:dec:ekpecn7}). |
| verification | `method` | required | One of `test`, `analysis`, `inspection`, `demonstration`, `formal-proof`. |
| specification | `authority` | required at `strict` | A list of repository-relative paths to the external authority documents the design answers to (for example an OpenAPI document or a JSON Schema), each a file outside the corpus; an empty list declares the specification answers to no external authority. The source of truth for the specification's independent authority; the optional `## Authority` section is its commentary ([Independent authority on specifications](../../decisions/specification-authority.md){id=note:dec:av7k3mq}). |
| principle | `altitude` | optional | One of `value`, `operating`, `authoring`: the altitude at which the weighted commitment operates and the reader it serves, drawn from the classification the Principle term defines. `value` is carried into everything (a held good of who we are), `operating` guides day-to-day work, `authoring` governs how the corpus itself is written; a principle that operates at more than one records its home altitude. Omit when not worth recording ([Principle altitude field](../../decisions/principle-altitude-field.md){id=note:dec:3vg9jdh}). |

A decision may be authored as a draft proposal: the context laid out, options weighed, and a recommendation made, with `status: draft` and no `decided` field; the timestamp is set when the decision is ratified to `current`.

A term and a persona carry no per-kind frontmatter beyond the envelope; their identity is the uniform opaque id, with the designation in `name` and any further designations in `aliases`.

The `altitude` field on a principle is optional at every profile: an enrichment an author applies when the altitude is worth recording, not a profile-gated discipline.
It is a reading-and-routing lens carried on the single principle kind, not a new kind and not a relation; a requirement or convention `enacts` a principle whatever its altitude.

## Body structure by kind

Every body opens with an unheaded lead, a single statement of the artifact's substance, and the designation is never repeated as a body heading.
The sections below are level-2 headings in the canonical order shown.
At the `bare` profile the lead alone is required; the sections marked required are what `standard` expects.

A defined Term or Persona is written in Title Case in prose, every significant word capitalized, so it reads as defined Note vocabulary and resolves against the terminology or persona set rather than common English; the lowercase form is reserved for a literal frontmatter token a term may name, the YAML key `status` or the value `draft`, written as code.
The same Title Case form is carried by a Term's or Persona's own `name`, so the word as written in prose and the designation on the artifact match on lookup.

Where an artifact carries a `persona` field, its lead names the persona that field cites, in the Title Case a defined persona carries per the rule above, so the holder reads as the defined persona and the prose agrees with the field; where the field cites several personas who share one want, the lead evokes them by their shared situation rather than naming each in turn.
An artifact that reaches its persona through the trace rather than through a field of its own is written in that persona's terms and need not name it.
The persona named in prose is a display mention, not a second source: the `persona` field stays authoritative, and a rename refreshes that citation as any defined term named in prose is refreshed.
This is method behavior, not a corpus-local choice: it holds wherever a kind carrying a `persona` field is authored, the discovery pack extending it to that pack's persona-bearing kinds.

### need

| Section | Req/Opt | Content |
|---|---|---|
| *(lead)* | required | The want, in the persona's terms, naming the persona the `persona` field cites, per the lead-naming rule above, including why it matters: the stakes if it goes unmet. |
| `## Source` | optional | External citations grounding the need: a standard, a policy, a paper, a URL. |
| `## Illustrative situations` | optional | Concrete scenarios that shaped the need. |

A need names its persona by the `persona` frontmatter field, not by a body relation.

### requirement

| Section | Req/Opt | Content |
|---|---|---|
| *(lead)* | required | The obligation, stated solution-free (solution-free unless `type` is `constraint`). |
| `## Source` | optional | External citations, where an external force or authority grounds the obligation. |
| `## Rationale` | recommended | Why the obligation holds; what is left to lower levels. |
| `## Acceptance criteria` | optional on-ramp | A blessed lightweight on-ramp: one or more solution-free conditions authored inline, until a criterion earns its own file ([The acceptance-criterion kind](../../decisions/acceptance-criterion-kind.md){id=note:dec:sxv0tq9}). The standalone acceptance-criterion kind is the canonical, promoted form. |
| `## Relations` | required | A stakeholder requirement `addresses` the need it serves; a system requirement is `derivedFrom` a stakeholder or coarser requirement; either may `enacts` a principle. |

`## Relations` is the one required section: it carries the requirement's traceability.

### specification

| Section | Req/Opt | Content |
|---|---|---|
| *(lead)* | required | The design commitment this fixes. |
| *(design sections)* | required | One or more `##` sections giving the schema, format, or mechanism. |
| `## Authority` | optional | Commentary on the `authority` field: which standard governs which part, the rule that the external document governs on divergence, the human-readable names. The external-citation register, the counterpart to a need's or a requirement's `## Source`; the field, not this section, is the source of truth ([Independent authority on specifications](../../decisions/specification-authority.md){id=note:dec:av7k3mq}). |
| `## Rationale` | recommended | Why this design, where the requirement and the authority leave a choice open, and absent where they determine it. A choice weighed against named alternatives is a decision record cited by `decidedBy`, not expanded here. |
| `## Relations` | required | `satisfies` the requirement(s) it designs for, and `derivedFrom` a coarser requirement where the specification refines one. |

A specification carries no `enacts`: it reaches a principle transitively through the requirement it satisfies.
A specification declares the independent authority its design answers to in the `authority` frontmatter field, the source of truth a checker reads; the optional `## Authority` section is its commentary, the external-citation register and counterpart to a need's or a requirement's `## Source`.
Both are distinct from a verification, which checks an implementation against the specification.

### verification

| Section | Req/Opt | Content |
|---|---|---|
| *(lead)* | required | What is verified and to what standard of passing, summarized; the verdict is owned by the Orchestrating Authority, not captured here. |
| `## Criteria` | required | What constitutes a pass. |
| `## Procedure` | required | How the check is made under the method named in frontmatter. |
| `## Evidence` | optional | A pointer to where a run's evidence lives, kept by the Orchestrating Authority; never the verdict. |
| `## Relations` | required | `verifies` the requirement, specification, convention, or acceptance-criterion the check directly establishes. |

### acceptance-criterion

| Section | Req/Opt | Content |
|---|---|---|
| *(lead)* | required | The solution-free condition under which a requirement or need is acceptable: the measurable threshold or observable outcome by which "acceptable" is judged, naming no mechanism. |
| `## Out of scope` | recommended | What the criterion does not require, guarding against a reading broader than intended. Recommended at `standard`. |
| `## Relations` | required | `qualifies` exactly one requirement or need, the item whose acceptance it defines. |

An acceptance-criterion is the declarative what-acceptable, distinct from a verification, which is the executable check that confirms the condition holds.
One criterion is one artifact with one id.

### decision

| Section | Req/Opt | Content |
|---|---|---|
| *(lead)* | required | A one-paragraph summary of what was decided. |
| `## Context` | required | The situation and the forces in play. |
| `## Decision` | required | The choice, as bullets where it has parts. |
| `## Forces and trade-offs` | required | What the choice costs and why it is accepted. |
| `## Alternatives considered` | required | What was rejected and why. |
| `## Driven by` | required | The typed list of `groundedIn` and `amends` edges, one per line, per the substrate's decision-edge grammar; not free prose. |
| `## Worked example` | optional | A concrete illustration. |

`## Driven by` carries only `groundedIn` and `amends`; the reverse, that a decision determined an artifact's content, is authored as `decidedBy` on that artifact, per the substrate's decision edges.

A decision may carry additional level-2 sections after the required set: the required sections are canonical and come first, and an additional section carries record the canonical set does not ([Decisions may carry sections beyond the required set](../../decisions/decision-sections-open.md){id=note:dec:d3cxs3c}).

### term

| Section | Req/Opt | Content |
|---|---|---|
| *(lead)* | required | The genus-and-differentia definition. |
| `## Inclusion test` | profile | A decision question that classifies a candidate as in or out. |
| `## Relations` | optional | Typed links from the substrate's closed term-relation set, one per line, each authored once on the end shown. |
| `## Origin` | profile | The grounding: the relevant general-English sense, plus the standards or professional lineage; a one-line note for a pure coinage. |
| `## Examples` / `## See also` | optional | Concrete cases; navigation pointers that are not typed relations. |

A term carries the opaque identity, with no slug: it is referenced and cross-referenced by designation, resolved by closed-vocabulary lookup against the terms and personas in force at the reading scope.

### persona

| Section | Req/Opt | Content |
|---|---|---|
| *(lead)* | required | A one-paragraph role description: who the actor is, optionally including the actor's stake or what it is looking for. No headed sections. |

A persona participates by reference from a need's `persona` frontmatter field, not by a relation verb.
Like a term, it carries the opaque identity, with no slug.

### convention

| Section | Req/Opt | Content |
|---|---|---|
| *(lead)* | required | The agreed practice, stated declaratively in one or two sentences; it may name the mechanism, format, or style it fixes, because the agreed mechanism is the substance. No *shall*: a convention binds the making of artifacts by agreement, not the system by obligation. |
| `## Rationale` | optional | Why this option was agreed, where the weighing is not already a decision record; the coordination value, not a restatement of the rule. |
| `## Relations` | optional | `enacts` the principle the convention serves, where one grounds it. |

A convention is exempt from the solution-free rule by kind ([Conventions as a first-class kind](../../decisions/conventions-first-class.md){id=note:dec:4g730rg}); where alternatives were genuinely weighed, a decision record carries the why and the convention names it through its own `decidedBy`.

### principle

| Section | Req/Opt | Content |
|---|---|---|
| *(lead)* | required | The principle statement: the named, weighted commitment, in one or two sentences. |
| `## Why this matters` | required | The rationale, and the risk the principle mitigates or the gain it realizes. |
| `## How to apply` | required | The litmus for when the principle bears, and how to honor it. |
| `## Considered alternative` | recommended | The rejected opposite, and why it was not taken. |
| `## Relations` | optional | Authored links to other principles or terms, if any. A principle authors no `enacts`; its `enactedBy` inverse, the obligations that enact it, is a derived view. |
| `## Origin` | profile | The grounding: the relevant general-English sense, plus the standards or professional lineage. |

A principle is a transverse normative anchor, not a node on the need-to-requirement spine ([Principles as a first-class kind](../../decisions/principles-first-class.md){id=note:dec:eym5t5g}): a requirement or convention names the principle it `enacts`, pointing at the principle, while the principle itself authors no `enacts`.

### context

| Section | Req/Opt | Content |
|---|---|---|
| *(lead)* | required | The boundary statement: what is inside, outside, and crossing. |
| `## External entities` | required | The actors and systems the system interacts with. |
| `## What crosses the boundary` | required | The ports: what passes in and out. |
| `## What is out of scope` | required | Stated negatively, on purpose. |

A `## Source` and a `## Rationale`, where both appear on a kind, are separate sections on purpose: Source records the external citations that ground a claim, Rationale records the internal reasoning, and keeping them apart makes evidential circularity visible.
Grounding is acyclic: a cited Source must not itself derive from the artifact it grounds.

## Verb endpoint rows

The pack contributes the endpoint rows below to the substrate's verb catalogue.
The substrate fixes each verb's name, direction, and derived inverse; the pack supplies which kinds the verb joins, and the corpus's effective catalogue is the union of its enabled packs' rows.
Each edge is authored once, on the dependent end, and reads as a true sentence `<dependent> <verb> <governing>`.

| Verb | Authored on | To | Inverse |
|---|---|---|---|
| `addresses` | requirement | need (or, in the discovery pack, a job) | `addressedBy` |
| `derivedFrom` | requirement, specification | requirement | `refinedBy` |
| `satisfies` | specification | requirement | `satisfiedBy` |
| `verifies` | verification | requirement, specification, convention, or acceptance-criterion | `verifiedBy` |
| `enacts` | requirement, convention | principle | `enactedBy` |
| `qualifies` | acceptance-criterion | requirement or need | `qualifiedBy` |

`addresses` joins a requirement to the need it serves, on every need and whatever packs are enabled; the spine never bends to a pack.
The discovery pack adds the facet endpoints, and a requirement may relieve, create, or address a facet directly wherever no offering facet covers it.

`enacts` is sourced from a requirement or a convention in the spine pack; an enabled pack may extend the source set through the substrate's union rule, as the governance pack does in adding policy and standard.
A specification reaches a principle transitively through the requirement it satisfies, so a specification never carries `enacts`; reading the principle along the satisfy edge keeps the value authored once, on the nearest obligation.

`qualifies` joins an acceptance-criterion to the one requirement or need whose acceptance it defines.
The `verifies` row includes acceptance-criterion as a target, so a verification may check a criterion directly; the requirement is then met transitively, the verification checking the criterion and the criterion qualifying the requirement.

The decision edges `groundedIn`, `amends`, and `decidedBy` are substrate-level, fixed once in [The substrate](substrate.md){id=note:spec:tkhd63e}; the spine pack supplies their endpoint kinds (decision, requirement, specification, convention, need, principle) but does not redeclare the verbs.

### The acceptance-criterion section on-ramp

A `## Acceptance criteria` section authored on a requirement is a permitted authoring on-ramp, so an author need not mint a separate file for every criterion from the first draft.
The standalone acceptance-criterion kind is the canonical, promoted form: where a criterion is traced to, referenced, or verified, it earns its own file, and a tool promotes a bundled section into its own acceptance-criterion artifacts ([The acceptance-criterion kind](../../decisions/acceptance-criterion-kind.md){id=note:dec:sxv0tq9}).

## Rationale

Declaring the spine pack in its own specification, separate from the substrate and from the discovery pack, is what lets one machinery carry a sharp trace spine without welding every kind into one document, and lets kind-legality be checked per enabled pack.

The spine carries the kind set most efforts earn: the four trace kinds that close the need-to-requirement-to-specification-to-verification chain, the rule and quality kinds that bind it, the boundary and vocabulary kinds that make it legible, and the principle that anchors it.
Holding the discovery kinds, the risk kind, and the plan pack out of the spine keeps the default honest: a corpus on the spine pack carries the kinds nearly every effort uses and none it would have to read past.

Fixing the kinds, their fields, and their sections here, while the substrate fixes the envelope and the verb machinery, is the same split the pack mechanism is designed around: the pack supplies the kinds and the endpoint rows, the substrate supplies everything kind-agnostic.

## Relations

- satisfies: [A provided default package](../../requirements/system/provided-default-package.md){id=note:req:rfdr0e7}
- satisfies: [Independently validatable specifications](../../requirements/system/independently-validatable-specifications.md){id=note:req:fph0vnr}
- decidedBy: [The default spine pack](../../decisions/spine-pack.md){id=note:dec:4tzn3av}
- decidedBy: [The acceptance-criterion kind](../../decisions/acceptance-criterion-kind.md){id=note:dec:sxv0tq9}
- decidedBy: [Principles as a first-class kind](../../decisions/principles-first-class.md){id=note:dec:eym5t5g}
- decidedBy: [Principle altitude field](../../decisions/principle-altitude-field.md){id=note:dec:3vg9jdh}
- decidedBy: [Conventions as a first-class kind](../../decisions/conventions-first-class.md){id=note:dec:4g730rg}
- decidedBy: [Terms and personas as first-class, scoped kinds](../../decisions/terms-and-personas-as-kinds.md){id=note:dec:t4w8k2n}
- decidedBy: [Proposable decisions](../../decisions/proposable-decisions.md){id=note:dec:ekpecn7}
- decidedBy: [EARS requirement syntax](../../decisions/ears-requirement-syntax.md){id=note:dec:p7k3w9n}
- decidedBy: [Independent authority on specifications](../../decisions/specification-authority.md){id=note:dec:av7k3mq}
- decidedBy: [The validation field](../../decisions/validation-field.md){id=note:dec:vf2m8qe}
