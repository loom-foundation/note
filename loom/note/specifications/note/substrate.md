---
id: note:spec:tkhd63e
name: The substrate
kind: specification
status: current
authority: []
---

This specification fixes the kind-agnostic substrate every Note artifact rides: the file envelope, the identity scheme, the conformance floor, the universal lifecycle, the relation machinery, the term-relation set, the three citation surfaces, the conformance profiles, the pack mechanism, and the manifest schema.
It knows no kind: the kinds, their fields, and their body sections are supplied by packs, each fixed in its own specification.

It is the schema that checkable well-formedness requires ([Checkable well-formedness and identity](../../requirements/system/checkable-well-formedness.md){id=note:req:sp8g0my}) and the foundation a pack specification extends ([Declarable kind packages](../../requirements/system/declarable-kind-packages.md){id=note:req:ekfkzzt}).

## File envelope

An artifact is a single UTF-8 text file: YAML frontmatter delimited by `---`, then a Markdown body, one artifact per file.

The body carries no level-1 heading; the designation lives in frontmatter.
Exactly one blank line separates the closing frontmatter delimiter from the lead, marking where configuration ends and substance begins.
The body opens with an unheaded lead, a single statement of the artifact's substance, and the designation is never repeated as a body heading.
Section headings are level 2, in the canonical order the artifact's pack fixes for its kind.

Prose is wrapped with semantic line breaks, one sentence per source line within a paragraph and a blank line between paragraphs; the discipline is recommended, not a conformance gate, and a line carrying more than one sentence is reportable, never invalid ([Semantic line breaks in artifact prose](../../decisions/semantic-line-breaks.md){id=note:dec:sw4k9n2}).

A file's name is descriptive kebab-case; it is a navigation convenience, never the identity.

A frontmatter value is a YAML scalar.
A value that contains a colon followed by a space is quoted, because an unquoted scalar containing `: ` parses as a nested mapping that a conforming YAML parser rejects.

## Identity

Every artifact carries an immutable `id` of three colon-separated segments:

```
<namespace>:<kind-segment>:<opaque>
```

- `<namespace>` is the corpus's namespace, declared once in its manifest; it is the identity-space boundary every artifact's id carries, the same across every repository the corpus spans.
- `<kind-segment>` abbreviates the kind; a pack fixes the segment for each kind it declares.
- `<opaque>` is a Crockford Base32 string: the digits `0` to `9` and the letters `A` to `Z` minus `I`, `L`, `O`, and `U`, written lowercase and compared case-insensitively, and unique within its namespace; a tool mints it from a cryptographically secure source and checks it against the corpus, and a sole author may instead allocate it by hand, for example sequentially with a small registry, as long as it stays unique.

The same opaque grammar serves every kind, with no exception ([Uniform opaque identity](../../decisions/identity-and-designations.md){id=note:dec:jhgkwja}).
The opaque length is configurable per corpus in the manifest, defaulting to seven characters; the configured length applies to newly minted ids and never forces a re-mint of an existing one.
Uniqueness is scoped to the namespace, not to a single repository: distinct namespaces never collide, and one namespace may span several repositories, where the per-repository collision check is a local backstop and the cryptographically random opaque at the configured length keeps parallel offline minting collision-free, confirmed by a workspace-assembly check rather than coordinated at the mint ([The multi-root corpus](../../decisions/multi-root-corpus.md){id=note:dec:0n14gqx}).

The id is immutable: it is minted once, and a move or a rename never changes it.
Every reference carries the target's id, so identity survives any reorganization of the tree.

The `kind` field is authoritative for the artifact's kind; the id's kind-segment is fixed from it at minting, and a checker asserts the two agree.

### Designations: `name` and `aliases`

An artifact carries a `name` field holding its designation: a concise label, never a summary of the body.
An optional `aliases` list holds additional designations of the same concept (a synonym in transition, an abbreviation, a prior name).
There is no `title` field.

A reference's visible text is the target's current `name`, refreshed after a rename; if it drifts, nothing breaks, because the id is the citation.
A reference never targets an alias; an alias is for lookup and display only.

A capitalized word in prose resolves against the names and aliases of the terms and personas in force at the reading scope.

Designation uniqueness is checked twice.
At minting, a designation (a name or an alias) is unique within its namespace; a tool refuses a duplicate outright.
At resolution, a designation that is ambiguous in the effective set at a reading scope (which inheritance across namespaces can create) is surfaced like a cascade tie, with the cascade's replace operator as the sanctioned resolution.

## The conformance floor

Whatever the profile, an artifact is well-formed only with a well-formed envelope, the common required frontmatter, the per-kind required frontmatter its pack declares, and a lead.

The common required frontmatter, on every kind:

| Field | Required | Value |
|---|---|---|
| `id` | required | `<namespace>:<kind-segment>:<opaque>`, immutable; the kind-segment agrees with `kind`. |
| `name` | required | The designation: a concise label, not a summary. |
| `kind` | required | The kind token, drawn from an enabled pack; authoritative for the kind-segment. |
| `status` | required | One of `tbd`, `draft`, `current`, `obsolete`, `rejected`. |

Optional common frontmatter:

| Field | Value |
|---|---|
| `aliases` | A list of additional designations. |
| `supersedes` / `superseded_by` | A citation of the replacing or replaced artifact, in the standard citation form (name label, relative path, id), used when one artifact replaces another; the id is the authoritative part, the label and path refreshable conveniences. The two are authored as a pair by the change that retires the predecessor, `supersedes` on the successor and `superseded_by` on the retired artifact, and a checker reports a one-sided or mismatched pair; where the retired artifact is read-only (a materialized frozen mirror), `superseded_by` is not authored and the retired side's view is derived from the successor's `supersedes`. |
| `scope` | The scope id at which the artifact is load-bearing; omitted, it takes the scope of its enclosing scope root ([Scope and cascade](scope-and-cascade.md){id=note:spec:1r673tc}). |
| `last_reviewed` | An ISO date; earns its place once an artifact is `current`. |
| `obsoleted` | An ISO date recording retirement; earns its place at `status: obsolete`. |
| `materialized` | A block (`from`, `at`, `commit`, `on`) present only on a frozen copy captured from another corpus ([Cross-repository inheritance and materialization](../../decisions/cross-repository-inheritance.md){id=note:dec:h4w9k2t}). |

A pack adds the per-kind required and optional frontmatter for each kind it declares.

A frontmatter field no enabled pack declares is a warning-tier finding: reported by name, preserved untouched by any tool that rewrites the artifact, and never an error, so a corpus written against a later minor of the same major stays valid to an earlier reader ([Unknown frontmatter fields are reported, never fatal](../../decisions/unknown-fields-reported.md){id=note:dec:nkf13dw}).

A materialized frozen copy lives under `materialized/<namespace>/<version>/` at its layer root, inside the corpus but clearly separate from authored intent, its per-artifact provenance the single record of the capture ([Cross-repository inheritance and materialization](../../decisions/cross-repository-inheritance.md){id=note:dec:h4w9k2t}).

## Lifecycle and transitions

Every artifact carries a `status` from one universal set, the same for every kind ([Universal artifact lifecycle and its transitions](../../decisions/artifact-lifecycle.md){id=note:dec:gfwq0mv}).

| Status | Meaning |
|---|---|
| `tbd` | A scaffolded placeholder: named, no authored substance yet. |
| `draft` | Authored substance present, not yet confirmed operative. |
| `current` | The confirmed operative source. |
| `obsolete` | Retired content, once operative, kept for history. A terminal state. |
| `rejected` | An authored proposal deliberately declined, kept as a record. A terminal state. |

The well-formed transitions:

| From | To | Meaning |
|---|---|---|
| `tbd` | `draft` | A placeholder gains authored substance. |
| `tbd` | `current` | Authored and confirmed operative in one act. |
| `draft` | `current` | The content is confirmed operative; for a decision this sets `decided`. |
| `draft` | `rejected` | An authored proposal is deliberately declined. |
| `current` | `obsolete` | Operative content is retired. |

`obsolete` follows only `current`; `rejected` follows only `draft`.
Motion is monotonic toward settled, then terminal; no transition runs backward, and a terminal artifact is never reinstated in place.
Reopening a settled question is a new artifact that may supersede the old one (`supersedes` on the successor, `superseded_by` on the retired artifact), never a rewrite of the original's lifecycle.

Deletion is not a transition: an unauthored `tbd` placeholder, or a `draft` abandoned with no conclusion, may be deleted.
The discriminator between deleting a draft and marking it `rejected` is whether a deliberate conclusion to decline was reached and is worth keeping.

The stage set and its transitions are fixed; a pack may narrow the set a given kind uses, never widen it.
Stage names may be surfaced as house terms through the manifest vocabulary map, but a committed file carries the canonical token.
Note defines which transitions are well-formed; who may perform one, and when a pipeline gates on a status, belongs to the Orchestrating Authority, and who performed it is carried by Git history, not a frontmatter field.

## Archive placement

A terminal artifact (`obsolete` or `rejected`) is placed under a single visible `archive/` directory at its layer root, mirroring the kind tree beneath it (`archive/decisions/...`, `archive/requirements/system/...`) ([Archive and retention](../../decisions/archive-and-retention.md){id=note:dec:gh7mhc4}).
Status stays authoritative; placement is the derived mirror a tool keeps in sync.
On a filename clash inside `archive/<kind>/`, the opaque id is suffixed.
The archive is part of the record and is not hidden.

## Relation machinery

A reference to another artifact is a Markdown link carrying the target's id:

```
[visible text](relative/path.md){id=<namespace>:<kind>:<opaque>}
```

The `{id=...}` is authoritative; the relative path is a navigation convenience a move may stale and a tool restores ([Inline citations use the reference-link form](../../decisions/inline-citation-form.md){id=note:dec:2dxr3xh}).

A relation is authored once, on the dependent end, and its inverse is a derived view, never authored ([Single authoritative representation per relationship](../../requirements/system/single-authoritative-relation.md){id=note:req:s5fh0e8}).
Every edge reads as a true sentence, `<dependent> <verb> <governing>`.
The hierarchical edges are acyclic.

A relation verb's name, direction, and derived inverse are fixed by the substrate; a pack contributes the verb's endpoints (which kinds it joins), and the effective verb catalogue for a corpus is the union of its enabled packs' endpoint rows.
A pack is closed over its endpoints: every verb row it declares has all its endpoint kinds available when the pack is enabled.

### The decision edges

A decision relates through typed edges, not free prose ([Typed decision edges](../../decisions/typed-decision-edges.md){id=note:dec:td3jw2y}).

| Verb | Authored on | To | Inverse |
|---|---|---|---|
| `groundedIn` | a decision | need, requirement, decision, or principle | `grounds` |
| `amends` | a decision | a still-current decision (in-place modification) | `amendedBy` |
| `decidedBy` | a requirement, specification, or convention | the decision that determined its content | `decides` |

A decision's `## Driven by` is the bullet list of its `groundedIn` and `amends` edges; the reverse relationship, that a decision determined an artifact's content, is authored on that artifact as `decidedBy`.
A decision authors no typed edge to a kind outside the `groundedIn` set; such a relationship, where real, is prose in the body.

## Term relations

Relations between terms are a separate closed set, authored once on the end shown, the hierarchical ones acyclic ([Terminology with typed term-relations](../../decisions/terminology-and-term-relations.md){id=note:dec:s9k4w7n}).

| Verb | Family | Authored on | Inverse |
|---|---|---|---|
| `is a` | generic | the subordinate concept | `subsumes` |
| `is a value of` | generic | the value | `ranges over` |
| `is part of` | partitive | the part | `is composed of` |
| `carries` | associative | the holder | `is carried by` |
| `scopes` | associative | the Context | `is scoped by` |
| `contrasts with` | associative, symmetric | the alphabetically-earlier term | (symmetric) |
| `relates to` | associative | either end, gloss required | (per gloss) |

A term's `## Relations` is a bullet list, one relation per line, written `- *verb* [Term](relative/path.md){id=...}` with an optional gloss; the subject term is implicit.
A pack verb is authorable between two terms wherever the owning pack defines an endpoint row for the kinds those terms name; the edge documents the kind model at the kind level, adding no endpoint legality and no instance-level obligation ([Pack verbs are authorable between terms](../../decisions/term-level-pack-verbs.md){id=note:dec:t3rmvrb}).

## Citation surfaces

Note cites a durable id across three surfaces; the id is the only load-bearing part of any citation.

**In-artifact**, within the corpus, uses the reference-link form above: in the body, with the relationship verb authored on the dependent end; in a frontmatter reference field, the same form without a verb.

**In-code**, from a file outside the corpus, carries the durable id behind the fixed marker `@intent`, with a human-readable label that is expected by convention but never checked ([In-code intent citation](../../decisions/in-code-intent-citation.md){id=note:dec:nfaeyk9}):

```javascript
// @intent Satisfies: acme:req:sp8g0my (checkout latency budget)
```

**In-commit**, a trailer at the foot of the message in the `Signed-off-by:`-style block, behind a Title-Case key, with the id never in the subject or prose ([Commit-message intent citation](../../decisions/commit-message-intent-citation.md){id=note:dec:hf8k2wd}).

The trailer and code-comment keys (`Satisfies:`, `Verifies:`, `Enacts:`, with `Refs:` the neutral fallback) are the expected, never-checked convention; a tool may raise advisory, non-blocking plausibility warnings on an unknown key or an implausible target kind.
The recommended default is `Refs:` unless the structural claim is verifiable.
The imperative state-change family (`Closes`, `Fixes`, `Resolves`) is excluded: a citation states a relationship, it never transitions state.
A committed file, including a code comment and a commit trailer, carries canonical tokens only; the vocabulary map is display and input normalization, never an authoring vocabulary.

## Conformance profiles

A profile is a pure rigor bundle; it carries no kind availability, which lives only in packs ([Conformance profiles as pure rigor bundles](../../decisions/conformance-profiles.md){id=note:dec:cf7n2wq}).

| Profile | Requires |
|---|---|
| `bare` | The floor: a well-formed envelope, the common required frontmatter, the per-kind required frontmatter, and a lead. |
| `standard` | `bare`, plus the full per-kind body sections each pack marks required, and a decision record for each design choice. |
| `strict` | `standard`, plus the profile-gated disciplines: term inclusion tests and Origins, typed term relations, constrained (EARS) requirement phrasing, verifications expected on current requirements (a current requirement with none is a reported finding, not an ill-formed artifact), and an independent-authority declaration on specifications. |

Adoption is monotonic: raising a profile may require adding sections, never invalidates an artifact valid under a lighter profile, and never changes identity or breaks a relation.
A profile is breadth of discipline; how far an artifact has matured is its `status`.

## The pack mechanism

A pack is a declarative selection of kinds ([Kind-agnostic substrate and kind packages](../../decisions/substrate-and-kind-packages.md){id=note:dec:w4awceq}).
A pack specification declares, for the pack it defines:

- the kinds it introduces, each with its id kind-segment;
- each kind's required and optional frontmatter fields, beyond the common envelope;
- each kind's required and optional body sections, in canonical order;
- the relation endpoint rows the pack contributes to the verb catalogue, with the endpoint kinds and the derived inverse.

A checker reads the enabled packs and validates kinds, fields, sections, and links from the files and the packs alone.

Enabling a pack is additive, the same monotonicity the profile axis carries: a pack contributes kinds and endpoint rows, and it may discipline the vocabulary it introduces, but it never invalidates an artifact or an edge that is legal without it.
A corpus that enables a pack keeps every substrate- and spine-legal edge; where a pack's richer path supersedes a bare edge, the overlap is surfaced by report, never made ill-formed ([Offering, fit, and the value proposition](../../decisions/offering-fit-and-value-proposition.md){id=note:dec:cjqwsxt}).

A pack normally introduces kinds; a pack may instead contribute only relation endpoint rows, riding the same declaration and closure rules, as the compliance pack does.

The method ships five built-in packs, the spine pack (the default), the discovery pack, the governance pack, the record pack, and the compliance pack, each fixed in its own specification; no adopter-authored pack mechanism is offered in this version.

## The manifest

A scope's manifest (`manifest.md` at the scope's layer root) is configuration, not intent, and is authoritative for everything that affects validation ([The corpus manifest](../../decisions/corpus-manifest.md){id=note:dec:mf3k9w2}).

A reader or tool finds the corpus by a two-step discovery: read `loom.md` at the repository root and follow its `root:` field where present, otherwise use `loom/`; a hidden `.loom/` with the same internal layout, and bare placement recognized wherever a layer's manifest sits, are the recognized fallbacks ([Adopter corpus placement](../../decisions/corpus-placement.md){id=note:dec:q2v7nk3}).

| Field | Value |
|---|---|
| `methodVersion` | The method version the corpus conforms to. Required. |
| `namespace` | The corpus's namespace: the identity-space prefix every artifact's id carries, declared once and the same across every repository the corpus spans. Required. |
| `opaqueLength` | The length of the opaque id segment minted in this corpus; optional, default seven. Set once on a multi-root corpus's root manifest, sized for the whole namespace ([The multi-root corpus](../../decisions/multi-root-corpus.md){id=note:dec:0n14gqx}). |
| `profile` | The corpus default conformance profile; any scope may override it. |
| `packs` | The enabled kind packages (the default is `[spine]`). |
| `vocabulary` | An optional map from a house term to a canonical token, unique both ways and never reusing one of the method's own canonical tokens as a house term, for statuses and verbs; display and input normalization only ([The manifest vocabulary map](../../decisions/vocabulary-map.md){id=note:dec:wn3xsjw}). |
| `scope` | The scope block (`id`, `parents`, optional `precedence`) declaring the scope's position in the cascade graph ([Scope and cascade](scope-and-cascade.md){id=note:spec:1r673tc}). |
| `roots` | Optional, on a multi-root corpus's root manifest: the member repositories that compose the corpus, each carrying its own manifest under the same namespace ([The multi-root corpus](../../decisions/multi-root-corpus.md){id=note:dec:0n14gqx}). |

A directory layout may mirror configuration for navigation, but the manifest, not the layout, is authoritative.

A corpus may span repositories: its root manifest declares `roots`, the members that compose it, each member carrying its own manifest under the same namespace; the assembled members are one corpus with one trace graph, one coverage closure, and one identity space ([The multi-root corpus](../../decisions/multi-root-corpus.md){id=note:dec:0n14gqx}).

## Rationale

Stating the substrate once, in the format it describes, makes a corpus self-describing and lets well-formedness be checked from the file alone, with no special tool.
Splitting the substrate from the packs is what lets one machinery carry a sharp trace spine and a product-discovery vocabulary without welding every kind into one document, and lets kind-legality be checked per enabled pack.
Splitting required-everywhere (the floor) from profile-gated rigor is what lets the same substrate serve a one-file prototype and a regulated corpus.

## Relations

- satisfies: [Checkable well-formedness and identity](../../requirements/system/checkable-well-formedness.md){id=note:req:sp8g0my}
- satisfies: [File-native capture](../../requirements/system/file-native-capture.md){id=note:req:mgdg9q0}
- satisfies: [Stable, location-independent identity](../../requirements/system/stable-identity.md){id=note:req:sfmkwmm}
- satisfies: [Legible lifecycle](../../requirements/system/legible-lifecycle.md){id=note:req:233g9mc}
- satisfies: [Typed, checkable relations](../../requirements/system/typed-relations.md){id=note:req:yb1xez2}
- satisfies: [Single authoritative representation per relationship](../../requirements/system/single-authoritative-relation.md){id=note:req:s5fh0e8}
- satisfies: [Stated-once, typed, checkable term-relations](../../requirements/system/typed-term-relations.md){id=note:req:n8w4k6m}
- satisfies: [Single authoritative term-relation](../../requirements/system/single-authoritative-term-relation.md){id=note:req:k4w7n9t}
- satisfies: [Tiered conformance](../../requirements/system/tiered-conformance.md){id=note:req:bth0rxp}
- satisfies: [Declarable kind packages](../../requirements/system/declarable-kind-packages.md){id=note:req:ekfkzzt}
- satisfies: [A provided default package](../../requirements/system/provided-default-package.md){id=note:req:rfdr0e7}
- satisfies: [In-code citation of intent](../../requirements/system/in-code-citation-of-intent.md){id=note:req:cffvvdz}
- satisfies: [Commit-message citation of intent](../../requirements/system/commit-message-citation-of-intent.md){id=note:req:cm7vq3x}
- decidedBy: [Kind-agnostic substrate and kind packages](../../decisions/substrate-and-kind-packages.md){id=note:dec:w4awceq}
- decidedBy: [Uniform opaque identity](../../decisions/identity-and-designations.md){id=note:dec:jhgkwja}
- decidedBy: [Typed decision edges](../../decisions/typed-decision-edges.md){id=note:dec:td3jw2y}
- decidedBy: [Conformance profiles as pure rigor bundles](../../decisions/conformance-profiles.md){id=note:dec:cf7n2wq}
- decidedBy: [The corpus manifest](../../decisions/corpus-manifest.md){id=note:dec:mf3k9w2}
- decidedBy: [Universal artifact lifecycle and its transitions](../../decisions/artifact-lifecycle.md){id=note:dec:gfwq0mv}
- decidedBy: [Archive and retention](../../decisions/archive-and-retention.md){id=note:dec:gh7mhc4}
- decidedBy: [The manifest vocabulary map](../../decisions/vocabulary-map.md){id=note:dec:wn3xsjw}
