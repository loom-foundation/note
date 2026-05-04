---
id: note:spec:w6nsgt1
name: The discovery pack
kind: specification
status: current
authority: []
---

This specification fixes the discovery pack: the opt-in kind package that carries the Value Proposition Canvas vocabulary, its eight kinds (offering, value-proposition, system, job, pain, gain, pain-reliever, gain-creator), each kind's id kind-segment, per-kind frontmatter and body sections, and the discovery verb rows the pack contributes to the substrate's relation catalogue.
It extends the substrate ([The substrate](substrate.md){id=note:spec:tkhd63e}) and adds, to the `need` kind the spine pack defines, the facets that turn a need into a profile.

It is one of the built-in packs the substrate names, enabled by listing `discovery` in the manifest's `packs`; a spine-only corpus holds none of its kinds.
The substrate's pack mechanism fixes what a pack specification declares (the kinds with their id kind-segments, the per-kind frontmatter, the body sections in canonical order, and the relation endpoint rows); this specification supplies those for the discovery pack and does not restate the mechanism.

## What the pack adds to the need

The `need` kind itself belongs to the spine pack ([The spine pack](spine-pack.md){id=note:spec:6kjja5r}); the discovery pack does not redefine it.
What the discovery pack adds is the need's facets and the reading they license.

When the discovery pack is enabled, a need is a *profile* over its Job, Pain, and Gain facets: the need carries its `persona`, an optional `validation`, its job-story lead, and its source, and its jobs, pains, and gains are member facet artifacts, one per file ([Atomic facets](../../decisions/atomic-facets.md){id=note:dec:af3k9w2}).
A facet may carry its own `persona`, narrowing whom it speaks for to a subset of the need's personas; omitted, the facet speaks for the need's whole set ([Facet persona field](../../decisions/facet-persona-field.md){id=note:dec:aj00tq7}).
An **offering** is a *value map* over its Pain Reliever and Gain Creator facets: it carries its benefit-led lead, and its relievers and creators are member facet artifacts, one per file.
Polarity is carried by the facet kind, never by a discriminator field on a shared kind: a pain is relieved and a gain is created, which are different inbound relations, so they are different kinds.

A need or an offering keeps its profile file *beside* its facet folder, never inside it.
A need's profile is `needs/<slug>.md`, sitting next to the directory `needs/<slug>/` that holds its Job, Pain, and Gain facets; an offering's profile is `offerings/<slug>.md`, beside `offerings/<slug>/`.
The profile and its facet folder share the slug; the profile is never placed inside its own facet folder (not `needs/<slug>/<slug>.md`).
Within a facet folder, where several facet kinds share one directory, a facet file's name is prefixed with its id kind-segment (`job-`, `pain-`, `gain-`, `pr-`, `gc-`) followed by the kebab-cased name, so the kinds read as distinct at a glance.

## Kinds and id kind-segments

The pack introduces eight kinds.

| Kind | Id kind-segment | Reading |
|---|---|---|
| `offering` | `offering` | A value map over its Pain Reliever and Gain Creator facets, written in full. |
| `value-proposition` | `vp` | The authored, customer-facing pitch of an offering. |
| `system` | `system` | The system-of-interest that provides the value: a product, service, hardware, or any arrangement, written in full. |
| `job` | `job` | A single job a need's persona is trying to get done. |
| `pain` | `pain` | A single pain the persona endures or fears. |
| `gain` | `gain` | A single gain the persona wants. |
| `pain-reliever` | `pr` | A single relief an offering provides for a pain. |
| `gain-creator` | `gc` | A single gain an offering creates. |

`offering`, `system`, `job`, `pain`, and `gain` are written in full, each being already short or a facet a reference should name; `value-proposition`, `pain-reliever`, and `gain-creator` abbreviate to `vp`, `pr`, and `gc`.

## Per-kind frontmatter

Each kind carries the common required frontmatter the substrate fixes (`id`, `name`, `kind`, `status`), plus the additions below.

| Kind | Adds | Values |
|---|---|---|
| `offering` | (none beyond the common envelope) | An offering carries no `type`; its polarity lives in its facet kinds. |
| `value-proposition` | `validation` (optional) | One of `assumed`, `inferred`, `observed`, `established`, `invalidated`: the tier grading the claim that the offered value lands, drawn from the classification the Validation term defines ([The validation field](../../decisions/validation-field.md){id=note:dec:vf2m8qe}). |
| `system` | (none beyond the common envelope) | A system carries no required field beyond the envelope; its versions are Git tags, and the build baseline a deployed version comprises is the Orchestrating Authority's record, not a field here. |
| `job` | `persona` (optional) | A citation, or a list of citations, of personas the facet speaks for, drawn from the parent need's `persona` set, each entry the standard citation form; omitted, the facet speaks for the need's whole persona set; present, it narrows to the listed subset, which pack-aware validation checks against the parent need ([Facet persona field](../../decisions/facet-persona-field.md){id=note:dec:aj00tq7}). |
| `pain` | `subkind` (optional) | One of `problem`, `obstacle`, `risk`: the sub-kind of pain drawn from the Value Proposition Canvas classification the Pain term defines. `problem` is an undesired outcome the persona already endures; `obstacle` stands in the way of a Job; `risk` is a potential, not-yet-realized undesired outcome the persona fears. Omit when the sub-kind is not known or not worth recording ([Pain subkind field](../../decisions/pain-subkind-field.md){id=note:dec:qc2nc57}). |
| `gain` | `expectation` (optional) | One of `required`, `expected`, `desired`, `unexpected`, the Kano expectation ladder drawn from the classification the Gain term defines. `required` maps to must-be quality whose absence is felt as a pain; `expected` is the standard one-dimensional outcome the persona anticipates; `desired` is a wanted outcome beyond the expected; `unexpected` is an attractive delight the persona did not anticipate. Omit when the level is not known or not worth recording ([Gain expectation field](../../decisions/gain-expectation-field.md){id=note:dec:c1m3hpn}). |
| `pain` / `gain` | `persona` (optional) | As on `job`: an optional narrowing of the parent need's persona set ([Facet persona field](../../decisions/facet-persona-field.md){id=note:dec:aj00tq7}). |
| `pain` / `gain` | `validation` (optional) | One of `assumed`, `inferred`, `observed`, `established`, `invalidated`: how validated the facet's claim is, drawn from the classification the Validation term defines; the evidence behind a raise is cited in the artifact's `## Source` ([The validation field](../../decisions/validation-field.md){id=note:dec:vf2m8qe}). |
| `pain-reliever` | (none beyond the common envelope) | |
| `gain-creator` | (none beyond the common envelope) | |

`subkind`, `expectation`, `validation`, and a facet's `persona` are optional at every profile: an optional enrichment is applied when the value is known and worth recording, not a profile-gated discipline.
The optional common frontmatter the substrate lists (`aliases`, `supersedes` / `superseded_by`, `scope`, `last_reviewed`, `obsoleted`, `materialized`) is available on these kinds as on any other.

## Body sections

Every body opens with an unheaded lead, then carries the level-2 sections below in the canonical order shown.

| Kind | Section | Req/Opt | Content |
|---|---|---|---|
| **offering** | *(lead)* | required | The value offered, in the persona's terms. Benefit-led, not solution-free, no *shall*. |
| | `## Relations` | required | `addresses` the need. |
| **value-proposition** | *(lead)* | required | The pitch, one sentence, in the persona's terms. Benefit-led, no *shall*. Matches the artifact's `name` field (without the trailing period). |
| | `## The case` | required at standard | The story in the persona's terms and the fit essence; the longer argument that follows the pitch. |
| | `## Relations` | required | `expresses` the offering. |
| **system** | *(lead)* | required | The system-of-interest that provides the value: a product, service, hardware, or any arrangement, in plain terms. |
| | `## Relations` | optional | `provides` the offerings, value-propositions, pain-relievers, or gain-creators it delivers. |
| **job** / **pain** / **gain** | *(lead)* | required | A single job, pain, or gain in the persona's terms, one per file. |
| | `## Relations` | required | `partOf` the need; a pain or gain may also be `framedBy` the job(s) it is felt against (optional). |
| **pain-reliever** / **gain-creator** | *(lead)* | required | A single relief an offering provides, or gain it creates, one per file, benefit-led. |
| | `## Relations` | required | `partOf` the offering, and `relieves` a pain (reliever) or `creates` a gain (creator). |

The lead is the only body content required at the `bare` profile; the required `## Relations` above is what the `standard` profile expects.

The spine pack's lead-naming rule carries into this pack: a facet that carries its own `persona` field names that persona in its lead, in Title Case; a facet that inherits its need's persona set, and an offering or value proposition, which carry no `persona` field and reach their persona through the trace, are written in that persona's terms and need not name it.

## Discovery verb rows

The substrate fixes each relation verb's name, direction, and derived inverse; the discovery pack contributes the endpoint rows below, and the effective catalogue for a corpus is the union of its enabled packs' rows.
The pack is closed over these endpoints: every kind a row names is available when the discovery pack is enabled.

| Verb | Authored on | To | Inverse |
|---|---|---|---|
| `expresses` | a value-proposition | the offering it pitches | `expressedBy` |
| `partOf` | a job, pain, or gain (to a need); a pain-reliever or gain-creator (to an offering) | the need or offering it is part of | `composedOf` |
| `relieves` | a pain-reliever, or a requirement for a facet no offering covers | the pain it relieves | `relievedBy` |
| `creates` | a gain-creator, or a requirement for a facet no offering covers | the gain it creates | `createdBy` |
| `framedBy` | a pain or gain | the job it is felt against, within the same need | `frames` |
| `delivers` | a requirement | the pain-reliever or gain-creator it delivers | `deliveredBy` |
| `addresses` | an offering (extending the spine row) | the need it serves | `addressedBy` |
| `provides` | a system | the offering, value-proposition, pain-reliever, or gain-creator it provides | `providedBy` |

A relation is authored once, on the dependent end shown; its inverse is a derived view, never authored.
The `addresses` verb is the spine pack's; the discovery pack extends it with the offering-to-need endpoint, so when both packs are enabled an offering and a requirement may each `addresses` a need.
The endpoints `relieves` and `creates` name a requirement source as well as a facet source: a requirement reaches a need-facet directly with that facet's polarity verb wherever no offering facet covers it.
Fit exclusivity is per facet: once an offering's reliever or creator covers a pain or gain, the direct requirement shortcut on that same facet is retired to the offering path, so the fit is never claimed twice.

The `framedBy` edge encodes, at facet granularity, the framing relation the need already states in prose: a need is a profile over several jobs, and a pain or gain is felt against a particular one of them (the Job kind being "the framing facet of a Need, the thing against which its Pains and Gains are felt").
It is authored on the dependent facet (the pain or gain) and its inverse `frames` is derived from the job, never authored.
The edge is optional and may repeat: a facet felt against one job authors one `framedBy`, a facet felt against several authors one edge each, and a facet that spans the whole need (or whose persona no job carries) authors none.
A `framedBy` target is a job that is `partOf` the same need as the facet; a target in a different need is a pack-aware-validation finding (the same tier as the facet-persona subset check), surfaced rather than resolved.
Because the edge is optional, its absence carries no completeness claim: `framedBy` yields the positive view "which jobs are framed by a pain or gain", not a proof that a job has none; an uncovered-job audit is informed by the edges but is not closed by their absence.

## The fit is derived

The **fit** between a need and an offering is the set of `relieves` (reliever to pain) and `creates` (creator to gain) edges between the offering's value map and the need's profile ([Offering, fit, and the value proposition](../../decisions/offering-fit-and-value-proposition.md){id=note:dec:cjqwsxt}).
The fit is computed from those edges and is never authored: an uncovered pain is a pain artifact with no inbound `relieves`, an orphan reliever is a pain-reliever with no `relieves` target, and both are reportable gaps rather than ill-formed artifacts.
A reliever or creator with no inbound `delivers` is a third reportable gap: value offered that no obligation yet realizes.
A value-proposition is the authored claim about the value; the fit, together with the `delivers` chain beneath it, is the evidence that substantiates it.

## The system-of-interest provides the value

The Value Proposition Canvas pairs the customer profile (the need's jobs, pains, and gains) with a value map of three elements: the Pain Relievers and Gain Creators an offering is composed of, and the **Products and Services** that provide them.
The `system` kind is that third element, written generally: the system-of-interest under design, a product, a service, a piece of hardware, or any arrangement that achieves a purpose ([System](../../terms/system-and-boundary/system.md){id=note:term:0jbwfkm}), the thing that provides the value an offering maps.
Earlier the pack mapped Products and Services to the System in prose only ([Offering, fit, and the value proposition](../../decisions/offering-fit-and-value-proposition.md){id=note:dec:cjqwsxt}); the `system` kind makes that provider a first-class, citable artifact, and `provides` makes the prose claim "the System provides the offering" an authored edge.

A system `provides` the offerings, value-propositions, pain-relievers, or gain-creators it delivers; the edge is authored on the system (the provider answers the value, so it carries the edge) and its inverse `providedBy` is derived, never authored.
It is optional and may repeat, and it is the offering-side counterpart of the need-side framing: just as a pain or gain names the job it is felt against, a reliever or creator names the system that provides it.
A coarse claim names a whole offering or value-proposition; a fine one names the specific relievers and creators a system provides, so that an offering implemented across several systems (one service per repository, say) records which system provides which facet, and full provision of an offering is then a derived view, like the fit.

Versions are tagged snapshots, not a kind: the corpus at a tag is that version's claimed value, the `provides` set a system carries there is what that version claims to deliver, and the increment between two versions is their diff (a Git tag is the common marker, but a model year or a published revision serves a non-Git adopter as well).
The set of commits a deployed version actually comprises is the Orchestrating Authority's record (a tag, a deployment manifest, or optional Records), never a field on the system, which would point durable intent down at a volatile build.

`provides` is an authored claim substantiated by computed evidence, exactly as a value-proposition is the claim a fit substantiates: the as-built truth is the upward in-code and in-commit `@intent` citations a downstream tool resolves against the deployed commits (for a non-code deliverable, the evidence is whatever the authority resolves against the as-built: a test report, a sign-off, a delivery record), and a divergence between what a system claims to provide and what its code cites is a reportable finding, not an authored correction.

The system-of-interest is the identity that provides value, distinct from the Context that states its boundary: a corpus with one system keeps it implicit in its single Context and authors a `system` artifact only when more than one system-of-interest must be told apart.
How a `system` relates to the per-service Context a multi-system corpus also authors is an open question this version does not settle ([The system-of-interest provides the value](../../decisions/system-of-interest-provides-value.md){id=note:dec:swar6np}, open questions).
Allocating a requirement to the system that owns it (a requirement `allocatedTo` a system) is a deliberate further step, deferred from this pack: this version encodes only the value-side provision, and the requirement-allocation edge is left to a later, separable decision.

## Raw and propositioned needs

A need is in one of two states, chosen need by need; neither state changes what the spine may say, because a pack is additive and enabling it never invalidates a relation that was legal without it.
A `requirement addresses need` edge is legal on every need, raw or propositioned.

A *raw* need carries no offering: its requirements may reach its facets directly, `relieves` its pains, `creates` its gains, and `addresses` its jobs, at facet granularity.

A *propositioned* need has an offering that `addresses` it.
The offering's relievers and creators carry the fit, with exclusivity per facet: once an offering facet covers a pain or gain, the direct requirement shortcut on that same facet is retired to the offering path.
Requirements `delivers` the relievers and creators, and that chain is the pack's purpose: a value proposition `expresses` the offering, the offering's facets relieve and create the need's facets, requirements deliver those facets, specifications satisfy the requirements, and verifications confirm them, so an authored pitch is substantiated by inspectable trace down to checked obligation.

Need-level coverage is a labeled union: obligations serving the need directly and obligations delivering its offering's facets are both reported, told apart.
A direct `addresses` edge beside a complete delivers chain is redundant and reported as such; an obligation outside the pitched value, a constraint or a non-functional floor, keeps the direct edge as its honest home and is surfaced as exactly that, information for the owner, never an error.
The value layer is therefore opt-in and adopted one need at a time: a corpus may leave most needs raw and propose value only where the pitch and the fit are worth the machinery.

## Rationale

Holding the eight Value Proposition Canvas kinds in their own pack is what lets one substrate carry a lean trace spine and a product-discovery vocabulary without welding the value model into every corpus: an effort that captures only its trace spine enables the spine pack alone and pays nothing for facets it does not use, and enables the discovery pack by one line of manifest configuration when it wants them.
Splitting the structured value (the offering), the computed correspondence (the fit), and the authored claim (the value-proposition) keeps three concepts the Canvas tradition blurs from sharing a word, and keeping the fit derived rather than authored makes coverage and gaps computable from the edges alone.
Carrying polarity in the facet kind, rather than a discriminator field, keeps a reference legible and relation validity kind-based.

## Relations

- satisfies: [Expressible value proposition](../../requirements/stakeholder/expressible-value-proposition.md){id=note:req:3pk9w2v}
- decidedBy: [Atomic facets](../../decisions/atomic-facets.md){id=note:dec:af3k9w2}
- decidedBy: [Offering, fit, and the value proposition](../../decisions/offering-fit-and-value-proposition.md){id=note:dec:cjqwsxt}
- decidedBy: [Pain subkind field](../../decisions/pain-subkind-field.md){id=note:dec:qc2nc57}
- decidedBy: [Gain expectation field](../../decisions/gain-expectation-field.md){id=note:dec:c1m3hpn}
- decidedBy: [Pains and gains framed by their job](../../decisions/pains-and-gains-framed-by-job.md){id=note:dec:tyf5xxw}
- decidedBy: [The system-of-interest provides the value](../../decisions/system-of-interest-provides-value.md){id=note:dec:swar6np}
- decidedBy: [The validation field](../../decisions/validation-field.md){id=note:dec:vf2m8qe}
