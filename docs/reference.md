# Adopter reference

A recorded decision plus a few commit trailers stop an agent from silently undoing a deliberate choice.
When you record *why* the code is the way it is, in a decision record an agent can read cold, and you cite that record from the commit that enacts it, an agent that later reviews the code finds the rationale instead of "cleaning up" what looks redundant.
That is the single sharpest thing Note buys you, and it costs four plain Markdown files and a habit.

Note is the intent layer of Loom: a way to capture what a system must be, why, and how you know it is met, as plain Markdown files that live beside your code.
Every artifact is a single file a human or an AI agent reads cold, with no special tool.
Note traces code to the obligation that prompted it, and it does so with files, identifiers, and typed links that a script can check from the files alone.

This reference is for an engineer, a product manager, or an AI agent who wants to author Note artifacts.
It uses a worked adopter namespace, `acme:`, throughout; the `acme:` ids in examples are illustrative and need not resolve.

**The note (state once).**
The note is the whole woven body of intent at a scope: the note layer holds the note.
An *artifact* is a single unit of the note (one need, one requirement, one decision): one file, one id.

The sections below cover, in order: a day-one quickstart, the directory convention, the stored artifact format, the id convention, the lifecycle, every kind, the layer model, the kind packs, the verb catalogue, and the three citation surfaces (corpus, code, commit).

---

## Day one

You need three things to start: a manifest, four starting kinds, and a commit-trailer habit.

**1. The manifest.** Create `loom/note/manifest.md`. This is the smallest manifest that validates:

```markdown
---
methodVersion: 0.5.0
profile: standard
packs: [spine]
---

# Manifest

The corpus manifest for acme: the method version, the conformance profile, and the enabled packs.
```

`profile` is `standard` for most teams (`bare` for a throwaway prototype, `strict` for a regulated corpus; see section 3).
Profiles set rigor, packs set kinds: see [profiles.md](profiles.md) for a per-value walkthrough and guidance on choosing.
`packs` defaults to `[spine]`; add `discovery` only when you want the Value Proposition Canvas kinds (section 7).

**2. The four starting kinds.** Most corpora begin with `need`, `requirement`, `decision`, and `term`:

- a **need** records a want in the persona's terms;
- a **requirement** records the obligation that addresses it;
- a **decision** records a choice and its why, so an agent does not undo it;
- a **term** pins a word the corpus uses with one specific meaning.

A first need is one file:

```markdown
---
id: acme:need:7k2m9q0
name: Fast Checkout
kind: need
status: current
persona: "[Shopper](../personas/shopper.md){id=acme:persona:3xq8r0t}"
---

Shoppers abandon the cart when checkout takes more than a few seconds, and every abandoned cart is lost revenue.
```

**3. The commit-trailer habit.** When a commit serves an artifact, cite it in a trailer at the foot of the message:

```
feat(checkout): cache the cart pricing read

Refs: acme:dec:pxnjmcd
```

Default to `Refs:` unless you can name a verifiable structural role (`Satisfies:`, `Verifies:`, `Enacts:`).
The durable id is the only load-bearing part (section 9).

---

## 1. The directory convention and layers

### Discovery (the two-step algorithm)

A tool finds an adopter's Loom corpus by a fixed two-step algorithm:

1. Read `loom.md` at the repository root if it is present, and follow its `root:` field to the corpus location.
2. Otherwise use `loom/` at the repository root.

The recommended placement is the `loom/` umbrella at the repository root, so the second step resolves with no override file.
The `root:` field appears in exactly one place: the repo-root `loom.md` override, used when `loom/` collides with an existing directory or when a monorepo hosts several independent Loom instances:

```yaml
---
root: tools/acme-intent/loom
---
```

Two fallbacks are recognized.
A hidden `.loom/` directory (same internal layout as `loom/`) is recognized for a brownfield repository that prefers to keep the corpus out of the way.
A bare placement (a layer's manifest sitting at some other path) is recognized via the **layer-root rule**: a layer root is wherever a layer's `manifest.md` sits, whatever the surrounding path.

This meta-repository is a worked instance of the `loom.md` override: a `loom.md` at the repository root carries `root: corpus/note/loom`, pointing discovery at the umbrella inside the Note package, whose note-layer root is `corpus/note/loom/note/`.
The override keeps the whole Note method (corpus, docs, and licensing) self-contained in one subtree of a repository that hosts more than one Loom instance; identity is location-independent (section 3), the authoritative scope lives in the manifest, and a tool indexes any placement identically.

### The layers

Note rides a **substrate** (section 6) shared by a family of layers, each a coherent body of artifacts for one concern. Layer enablement is the manifest, mirrored by folder presence.

- **note** (live): the intent layer. Why the system exists, what it must do, why it was built that way, and how you know it is met. This is the trace spine and the rule, boundary, and vocabulary kinds. The note layer holds the note.
- **plan** (deferred): a planning layer for work and its order. Designed, not available in this version.
- **guild** (reserved): a layer for disciplines, roles, and skills. Named only; not specified in this version.

For an intent-only corpus, `loom/note/` is the only layer present.

### Scopes nest inside the note layer

A *scope* is the unit at which intent is load-bearing (a whole product, a subsystem, a package).
Scope declaration is opt-in: a body of work that occupies a single scope declares no scope block, inherits nothing, and pays nothing.
Each declared scope is rooted by two files in the note layer:

- `manifest.md` carries configuration (`methodVersion`, `profile`, `packs`, `vocabulary`, and the `scope` block: id and parents), authoritative for validation.
- `context.md` is the one-per-bounded-scope boundary statement: what is inside, outside, and crossing.

Both stay inside the note layer, because the context is intent and the manifest is the scope's configuration host.

### A worked tree

A single-scope adopter on the spine pack:

```
acme-repo/
├── src/ (the product code)
└── loom/
    └── note/
        ├── manifest.md (methodVersion, profile, packs, scope block)
        ├── context.md (the system boundary)
        ├── needs/
        │   └── fast-checkout.md
        ├── requirements/
        │   └── system/
        │       └── checkout-latency.md
        ├── decisions/
        │   └── cache-strategy.md
        ├── acceptance-criteria/
        │   └── checkout-on-saved-card.md
        ├── verifications/
        │   └── checkout-latency-load-test.md
        ├── terms/
        │   └── tenant.md
        └── archive/ (terminal artifacts, mirroring the kind tree)
            └── decisions/
                └── early-cache-stub.md
```

A multi-scope adopter nests scopes, each with its own `manifest.md` and `context.md`:

```
loom/
└── note/
    ├── manifest.md (root scope)
    ├── context.md
    ├── requirements/
    └── payments/ (a child scope)
        ├── manifest.md (declares scope acme-payments, parents: [acme])
        ├── context.md
        └── requirements/
```

### The archive

Terminal artifacts (`status: obsolete` or `status: rejected`) are placed under a single visible `archive/` directory at the layer root, mirroring the kind tree beneath it (`archive/decisions/...`, `archive/requirements/system/...`).
Status stays authoritative; placement is the derived mirror a tool keeps in sync.
On a filename clash inside `archive/<kind>/`, the opaque id is suffixed.
The archive is part of the record and is never hidden.

### A corpus across repositories (multi-root)

One corpus, one namespace, may span several repositories.
The root manifest declares the member repositories as `roots`; each member carries its own manifest under the same namespace.
Together they form one corpus with one trace graph, one coverage closure, and one identity space.

The root manifest sits where the workspace is already anchored: in the manifest or spine repository a workspace tool such as West or the repo tool uses, or in the parent directory that holds sibling repositories when they are checked out by hand.
A `loom.md` at the workspace root may point discovery at it.

References between members are ordinary in-corpus references, resolved on disk in the assembled workspace with no tool.
A different system, under a different namespace, is a cross-repository reference, not a member root.

A worked example: a system kept as three sibling repositories assembled in one workspace.

```
acme-workspace/
├── loom.md                 # points discovery at the root manifest
├── manifest.md             # root: namespace acme; opaqueLength 9; roots: [gateway, billing, catalog]
├── gateway/
│   └── note/
│       ├── manifest.md     # namespace acme
│       └── requirements/system/auth.md          (acme:req:7k2m9q0)
├── billing/
│   └── note/
│       ├── manifest.md     # namespace acme
│       └── requirements/system/invoicing.md     (acme:req:3xq8r0t)
└── catalog/
    └── note/
        └── manifest.md     # namespace acme
```

A requirement in `billing/` refers to one in `gateway/` as an ordinary in-corpus reference:

```
- derivedFrom: [Auth](../../gateway/note/requirements/system/auth.md){id=acme:req:7k2m9q0}
```

A second system, `vendor`, lives under a different namespace; `billing/` refers to it as a cross-repository reference, not as a member root.

---

## 2. The stored artifact format

A Note artifact is a single UTF-8 Markdown file: YAML frontmatter delimited by `---`, then a Markdown body.
One artifact per file.

The body carries no level-1 heading; the designation lives in frontmatter (`name`).
The body opens with an unheaded **lead**: a single statement of the artifact's substance (the want for a need, the obligation for a requirement, the definition for a term), with no heading above it.
Further sections are level-2 headings in the canonical order the kind fixes (section 5).
Prose is wrapped with semantic line breaks (one sentence per source line within a paragraph, a blank line between paragraphs), which keeps diffs legible.

A frontmatter value is a YAML scalar; a value containing a colon followed by a space is quoted, because an unquoted `: ` parses as a nested mapping.

### The conformance floor

Whatever the profile, an artifact is well-formed only with a well-formed envelope, the common required frontmatter (`id`, `name`, `kind`, `status`), the per-kind required frontmatter its pack declares, and a lead.
The four-line minimum, for a need:

```markdown
---
id: acme:need:7k2m9q0
name: Fast Checkout
kind: need
status: current
persona: "[Shopper](../personas/shopper.md){id=acme:persona:3xq8r0t}"
---

Shoppers abandon the cart when checkout takes more than a few seconds, and every abandoned cart is lost revenue.
```

(`persona` is the need's per-kind required frontmatter; a kind with no per-kind requirements floors at the four common fields plus a lead.)

The `kind` field is authoritative for the artifact's kind, and the id's kind-segment agrees with it: a checker asserts the two match.

At `standard` an artifact carries more: the per-kind sections described in section 5.
A fuller version of the same need:

```markdown
---
id: acme:need:7k2m9q0
name: Fast Checkout
kind: need
status: current
persona: "[Shopper](../personas/shopper.md){id=acme:persona:3xq8r0t}"
validation: observed
---

Shoppers abandon the cart when checkout takes more than a few seconds, and every abandoned cart is lost revenue.

## Illustrative situations

A returning shopper with a saved card expects to complete purchase in one tap; a multi-second spinner reads as a failure and they leave.
```

Stating the format in the format it describes is deliberate: it makes a corpus self-describing and lets well-formedness be checked from the file alone, with no server and no database.

### The common envelope

Every artifact carries these frontmatter fields:

| Field | Required | Value |
|---|---|---|
| `id` | required | `<namespace>:<kind-segment>:<opaque>`, immutable (section 3); the kind-segment agrees with `kind`. |
| `name` | required | The designation: a concise label, not a summary of the body. |
| `kind` | required | The kind token (one of the kinds in section 5), drawn from an enabled pack; authoritative for the kind-segment. |
| `status` | required | One of `tbd, draft, current, obsolete, rejected` (section 4). |
| `aliases` | optional | A list of additional designations of the same concept (a synonym in transition, an abbreviation, a prior name). A reference never targets an alias; an alias is for lookup and display only. |
| `scope` | optional | The scope id at which the artifact is load-bearing; omitted, it takes the scope of its enclosing scope root. Earns its place only where the artifact is load-bearing at a scope other than its location implies. |
| `supersedes` / `superseded_by` | optional | A citation of the replacing or replaced artifact in the standard citation form (name label, relative path, id), authored as a pair when one artifact replaces another: `supersedes` on the successor, `superseded_by` on the retired artifact. Where the retired artifact is a read-only frozen mirror, only the successor's `supersedes` is authored and the retired side's view is derived. |
| `last_reviewed` | optional | An ISO date; earns its place once an artifact is `current`. |
| `obsoleted` | optional | An ISO date recording retirement; earns its place at `status: obsolete`. |

There is no `title` field.

---

## 3. The id convention and profiles

### Identity

Every artifact carries an immutable id of three colon-separated segments:

```
<namespace>:<kind-segment>:<opaque>
```

- **`<namespace>`** is the corpus's namespace, declared once in its manifest; it is the identity-space boundary every artifact's id carries, the same across every repository the corpus spans.
  For Acme it is `acme:`; this meta-repo's corpus uses `note:`.
  An opaque is unique within its namespace, so distinct namespaces never collide and one namespace may span several repositories.
- **`<kind-segment>`** abbreviates the kind; a pack fixes the segment for each kind it declares (section 5 and section 7 list them: `req`, `dec`, `spec`, `ver`, `ac`, `conv`, `ctx`, and so on).
- **`<opaque>`** is a Crockford Base32 string: the digits `0-9` and the letters `A-Z` minus `I`, `L`, `O`, and `U` (dropped to avoid visual confusion). It is written lowercase and compared case-insensitively, and it must be unique within its namespace; a tool mints it from a cryptographically secure source and checks it against the corpus, and you may also mint it by hand (see "Minting an opaque" below).

```
acme:req:sp8g0my
acme:dec:pxnjmcd
acme:ver:4w9k2t1
```

**The opaque grammar is uniform across every kind, with no exception.**
A term and a persona carry the same opaque id as any other kind; neither uses a slug.
The designation lives in `name`, and further designations in `aliases`; a term is referenced and resolved by designation, not by a readable id.

```
acme:term:k4w7n9t       a term: opaque id, name "Tenant"
acme:persona:3xq8r0t    a persona: opaque id, name "Shopper"
acme:principle:eym5t5g  a principle: opaque id, name "Plain Naming"
```

### The opaque length

The opaque length is configurable per corpus, set in the manifest.
The default is **7 characters**: an adopter who configures nothing gets a 7-character opaque, as in every id above.
A very large corpus may configure a longer opaque; a small one may shorten it.
The configured length applies to newly minted ids and never forces a re-mint of an existing one.

### Minting an opaque (no tool required)

The format requires only that the opaque is unique within its namespace; nothing checks how you produced it, so neither way below needs the Note tool.

- **Random, no registry (recommended).** Take a random value from any source you have, your operating system (`uuidgen`, `openssl rand`), an online generator, or even dice or the tail of a git hash, and keep the leading Crockford characters. Randomness is what keeps independent authors, in different repositories of one namespace, from colliding without coordinating; a one-line script or your tool draws from a cryptographically secure source when one is at hand.
- **Sequential, with a registry.** A sole author may instead keep a small file of allocated opaques and increment them (`000`, `001`, and so on). This is simplest for one person in one repository, at the cost of maintaining the list, and it stops being collision-free once several authors mint in parallel under one shared namespace, which is the coordination the random approach avoids.

Either way, a collision check (a grep over the corpus, your tool, or your own eye against the registry) catches a clash before it lands.

### Immutability

The id is minted once and never re-minted; a move or a rename never changes it.
Every reference carries the target's id, so identity survives any reorganization of the tree.
A reference's visible text is the target's current `name`, refreshed after a rename; if it drifts, nothing breaks, because the id is the citation.
The file name is a navigation convenience (descriptive kebab-case), never the identity.

### Profiles (pure rigor bundles)

The conformance profile is a pure rigor bundle, set in the manifest.
It carries no kind availability: which kinds exist lives only in packs (section 7).

| Profile | Requires |
|---|---|
| `bare` | The floor: a well-formed envelope, the common required frontmatter, the per-kind required frontmatter, and a lead. |
| `standard` | `bare`, plus the full per-kind body sections each pack marks required, and a decision record for each design choice. |
| `strict` | `standard`, plus the profile-gated disciplines: term inclusion tests and Origins, typed term relations, constrained (EARS) requirement phrasing, verifications expected on current requirements (a current requirement with none is a reported finding, not an ill-formed artifact), and an independent-authority declaration on specifications. |

Adoption is monotonic: raising a profile may require adding sections, never invalidates an artifact valid under a lighter profile, and never changes identity or breaks a relation.
A profile is breadth of discipline; how far an artifact has matured is its `status`.

For an adopter-facing walkthrough of each profile value and guidance on choosing, see [profiles.md](profiles.md).

---

## 4. The artifact lifecycle

Every artifact carries a `status` from one universal set, the same for every kind:

| Status | Meaning |
|---|---|
| `tbd` | A scaffolded placeholder: named, no authored substance yet. |
| `draft` | Authored substance present, not yet confirmed operative. A decision in `draft` is a provisional proposal: context, options, and a recommendation, not yet ratified. |
| `current` | The confirmed operative source. The live, honored version. |
| `obsolete` | Retired content, once operative, kept for history. A terminal state. |
| `rejected` | An authored proposal deliberately declined, kept as a record. A terminal state. |

### The legal transitions

Motion is monotonic toward settled, then terminal. No transition runs backward.

| From | To | Meaning |
|---|---|---|
| `tbd` | `draft` | A placeholder gains authored substance. |
| `tbd` | `current` | Authored and confirmed operative in one act. |
| `draft` | `current` | The content is confirmed operative. For a decision this is ratification, and it sets the `decided` timestamp. |
| `draft` | `rejected` | An authored proposal is deliberately declined and kept. |
| `current` | `obsolete` | Operative content is retired and kept for history. |

`obsolete` follows only `current`; `rejected` follows only `draft`.
A `current` artifact is never returned to `draft` or `tbd`, and a terminal artifact is never reinstated in place.
Reopening a settled question is a *new* artifact that may supersede the old one (`supersedes` on the successor, `superseded_by` on the retired artifact), never a rewrite of the original's lifecycle.

Deletion is not a transition: an unauthored `tbd` placeholder, or a `draft` abandoned with no conclusion, may simply be deleted.
The discriminator between deleting a draft and marking it `rejected` is whether a deliberate conclusion to decline was reached and is worth keeping.

Note defines which transitions are well-formed.
Who may perform one, and when a pipeline gates on a status, belongs to the Orchestrating Authority, not to the format.
Who performed a transition is carried by Git history, not a frontmatter field.

Stage names may be surfaced as house terms through the manifest `vocabulary` map (section 7), but a committed file carries the canonical token.

**Intent is living.**
What becomes of a specification once the build ships falls into three families: *flow-forward*, where the document is scaffolding filed away after implementation; *flow-back*, where the code is the truth and changes are ported back into the document; and *living intent*, where the artifact remains the authoritative source and divergence from it is drift to be surfaced.
Note is living intent by construction: a `current` artifact stays the operative source for as long as it is honored, retirement is an explicit lifecycle act (`obsolete`, with `supersedes` on a successor), and nothing is archived merely because it was built.
The `archive/` tree holds terminal artifacts only, never shipped-and-filed specs.
Work-planning artifacts, which may legitimately be ephemeral, are the deferred plan layer's concern, not the note layer's.

---

## 5. The kinds

This section describes every kind: what it is, the frontmatter it adds beyond the common envelope, the body sections it carries, and what each field and section means.
The spine-pack kinds come first, grouped by role; the discovery-pack kinds follow in a clearly-marked opt-in section.
Section bodies are level-2 headings in the canonical order shown.
At `bare` the lead alone is required; the sections marked required are what `standard` expects.

The spine pack declares eleven kinds:

| Kind | Segment | Role on or around the spine |
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

---

### The trace spine: need → requirement → specification → verification

#### need

**What it is.** The originating want, in the persona's terms, before a solution is fixed.
The top anchor of the trace spine and the unit of prioritization.
With the discovery pack enabled, a need is a *profile* over its Job, Pain, and Gain facets, which are member files, not body sections.

**Frontmatter it adds.**

| Field | Req/Opt | Meaning |
|---|---|---|
| `persona` | required | A citation, or a list of citations, of the persona artifacts the need is wanted by; each entry is the standard citation form (name label, relative path, id) written as a quoted YAML string; by reference rather than free text. |
| `validation` | optional | One of `assumed, inferred, observed, established, invalidated`: how validated the underlying claim is. |

**Body sections.**

| Section | Req/Opt | Content |
|---|---|---|
| *(lead)* | required | The want, in the persona's terms, including the stakes if it goes unmet. |
| `## Source` | optional | External citations grounding the need (a standard, policy, paper, URL). |
| `## Illustrative situations` | optional | Concrete scenarios that shaped the need. |

A need names its persona by the `persona` frontmatter field, not by a body relation.

#### requirement

**What it is.** A binding obligation on the system, stated solution-free where possible.
The backbone node of the spine.

**Frontmatter it adds.**

| Field | Req/Opt | Meaning |
|---|---|---|
| `level` | optional | `stakeholder` or `system`. A stakeholder requirement states an obligation in the stakeholder's terms; a system requirement states an obligation on the system. A profile may require it. |
| `type` | optional | `functional`, `non-functional`, or `constraint`. A profile may require it where the solution-free check is enforced. `constraint` requirements bind the solution space (security, performance, compatibility, regulatory) and need not be solution-free. |

**Body sections.**

| Section | Req/Opt | Content |
|---|---|---|
| *(lead)* | required | The obligation, stated solution-free (unless `type: constraint`). |
| `## Source` | optional | External citations, where an authority grounds the obligation (stakeholder level). |
| `## Rationale` | recommended | Why the obligation holds; what is left to lower levels. |
| `## Acceptance criteria` | optional on-ramp | One or more solution-free conditions authored inline, a blessed lightweight on-ramp until a criterion earns its own file. See the on-ramp note under acceptance-criterion. |
| `## Relations` | required | The traceability links (section 8). |

A stakeholder requirement `addresses` the need (or, in the discovery pack, `relieves` a pain / `creates` a gain / `delivers` a reliever or creator).
A system requirement is `derivedFrom` a stakeholder or coarser requirement.
Either may `enacts` a principle.

```markdown
---
id: acme:req:sp8g0my
name: Checkout Latency Budget
kind: requirement
status: current
level: system
type: non-functional
---

The checkout flow completes within 800 milliseconds at the 95th percentile under expected load.

## Rationale

The 800ms budget is the point below which the spinner is not perceived as a failure; it is derived from the Fast Checkout need's observed abandonment threshold.

## Relations

- addresses: [Fast Checkout](../../needs/fast-checkout.md){id=acme:need:7k2m9q0}
- decidedBy: [Cache strategy](../../decisions/cache-strategy.md){id=acme:dec:pxnjmcd}
```

#### specification

**What it is.** The committed design solution for one or more requirements: the schema, format, structure, or mechanism.
The engineer's contract with the rest of the system.
Kept light and earned: authored for the non-trivial case, not heavyweight per change.

**Frontmatter it adds.**

| Field | Req/Opt | Meaning |
|---|---|---|
| `authority` | required at `strict` | A list of repository-relative paths to the external authority documents the design answers to (an OpenAPI document, a JSON Schema), or an empty list when the specification answers to none. The source of truth for the spec's independent authority; the optional `## Authority` section is its commentary. |

**Body sections.**

| Section | Req/Opt | Content |
|---|---|---|
| *(lead)* | required | The design commitment this fixes. |
| *(design sections)* | required | One or more `##` sections giving the schema, format, interface, or mechanism. |
| `## Authority` | optional | Commentary on the `authority` field: which standard governs, the rule that the external document governs on divergence, the human-readable names. The counterpart to a need's or requirement's `## Source`; the field is the source of truth. |
| `## Rationale` | recommended | Why this design, where the requirement and the authority leave a choice open; a weighed choice is a decision record cited by `decidedBy`. |
| `## Relations` | required | `satisfies` the requirement(s) it designs for, and `derivedFrom` a coarser requirement where it refines one. |

A specification carries no `enacts`: it reaches a principle transitively through the requirement it satisfies (section 8).

#### verification

**What it is.** The executed check, under a named method, that an obligation is met, plus where its run-evidence lives.
The bottom of the spine: code → verification → obligation.
For an agent it is the only confidence anchor and an executable teacher of invariants.
Note captures the check; running it and owning the verdict belong to the Orchestrating Authority.

**Frontmatter it adds.**

| Field | Req/Opt | Meaning |
|---|---|---|
| `method` | required | One of `test`, `analysis`, `inspection`, `demonstration`, `formal-proof`. |

**Body sections.**

| Section | Req/Opt | Content |
|---|---|---|
| *(lead)* | required | What is verified and to what standard of passing. |
| `## Criteria` | required | What constitutes a pass. |
| `## Procedure` | required | How the check is made under the named method. |
| `## Evidence` | optional | A pointer to where a run's evidence lives, kept by the Orchestrating Authority. Never the verdict. |
| `## Relations` | required | `verifies` the requirement, specification, convention, or acceptance-criterion the check directly establishes. |

---

### The rule and quality kinds: decision, convention, acceptance-criterion

#### decision

**What it is.** A recorded choice among alternatives, with context and consequences, so future humans and agents recover the *why-this-way*. ADR-shaped.
For an AI agent this is the single most load-bearing artifact: without the recorded rationale, an agent will "clean up" code that looks redundant and silently undo a deliberate choice.

**Frontmatter it adds.**

| Field | Req/Opt | Meaning |
|---|---|---|
| `decided` | required at `current` and `obsolete`; omitted at `tbd`, `draft`, `rejected` | An RFC 3339 UTC timestamp ending in `Z`. Set when the decision is ratified to `current`. A rejected decision never reached `current`, so it carries no `decided`. |

**Body sections.**

| Section | Req/Opt | Content |
|---|---|---|
| *(lead)* | required | A one-paragraph summary of what was decided. |
| `## Context` | required | The situation and the forces in play. |
| `## Decision` | required | The choice, as bullets where it has parts. |
| `## Forces and trade-offs` | required | What the choice costs and why it is accepted. |
| `## Alternatives considered` | required | What was rejected and why. |
| `## Driven by` | required | The typed `groundedIn` and `amends` list, one relationship per line (section 8); not free prose. |
| `## Worked example` | optional | A concrete illustration. |

A decision's `## Driven by` carries only `groundedIn` and `amends`; the reverse, that a decision determined an artifact's content, is authored as `decidedBy` on that artifact (section 8).
Decision records are living documents: a small correction is made in place on the still-current decision (the old choice moves to `## Alternatives considered`), while a modification that is itself decision-worthy is a new decision that authors `amends` toward the one it modifies (section 8).
A wholesale replacement uses the `supersedes`/`superseded_by` frontmatter instead.

#### convention

**What it is.** An agreed authoring or coordination practice that binds the *making* of artifacts by agreement, not the system by obligation.
It uses no *shall*.
A convention is where a Definition of Done lives: a standing, shared, team-authored quality agreement that applies to all artifacts at a level is a convention (scoped by the `scope` mechanism), not an acceptance-criterion (which is per-item) and not a verification (which is the executed check).
For an AI agent, a convention's worth is proportional to how *enforceable* it is, so a convention is best authored to be checkable, ideally with a `verifies`-linked check.

**Body sections.**

| Section | Req/Opt | Content |
|---|---|---|
| *(lead)* | required | The agreed practice, stated declaratively in one or two sentences. It may name the mechanism, format, or style it fixes. |
| `## Rationale` | optional | Why this option was agreed, where the weighing is not already a decision record; the coordination value. |
| `## Relations` | optional | `enacts` the principle the convention serves, where one grounds it. |

A convention is exempt from the solution-free rule by kind; where alternatives were genuinely weighed, a decision record carries the why and the convention names it through its own `decidedBy`.

#### acceptance-criterion

**What it is.** A solution-free condition, authored at commit time (with its requirement), that defines what "acceptable" means for a requirement or need.
The product owner's sign-off instrument and the engineer's definition-of-done at the item level.
It is *declarative* (the what-acceptable), distinct from a verification, which is the *executable* check.
It is authored solution-free, before build, often in Given-When-Then form, and it is the natural home for the explicit out-of-scope an agent most needs.

An acceptance-criterion is a distinct kind, not a section on a requirement, because it has a distinct author (the PO), a distinct lifecycle (authored solution-free, before build, per item), and a distinct audience.

**Frontmatter it adds.** None beyond the common envelope.

**Body sections.**

| Section | Req/Opt | Content |
|---|---|---|
| *(lead)* | required | The condition that must hold for acceptance, stated solution-free. |
| `## Out of scope` | recommended | What this criterion explicitly does *not* cover, stated negatively on purpose. Recommended at `standard`. |
| `## Relations` | required | `qualifies` exactly one requirement or need (section 8). |

```markdown
---
id: acme:ac:m3hpn1c
name: Checkout completes within budget on saved card
kind: acceptance-criterion
status: current
---

Given a returning shopper with a saved card, when they confirm the order, the confirmation screen appears within the latency budget without an intermediate spinner.

## Out of scope

Guest checkout and new-card entry are covered by separate criteria.

## Relations

- qualifies: [Checkout Latency Budget](../requirements/system/checkout-latency.md){id=acme:req:sp8g0my}
```

**The section on-ramp.** A `## Acceptance criteria` section authored on a requirement is a permitted authoring on-ramp, so an author need not mint a separate file for every criterion from the first draft.
The standalone acceptance-criterion kind is the canonical, promoted form: where a criterion is traced to, referenced, or verified, it earns its own file, and a tool promotes a bundled section into its own acceptance-criterion artifacts.

---

### The boundary and vocabulary kinds: context, term, persona

#### context

**What it is.** The system boundary: what is inside, outside, and crossing.
One per bounded scope, kept in the note layer as `context.md`.

**Body sections.**

| Section | Req/Opt | Content |
|---|---|---|
| *(lead)* | required | The boundary statement: what is inside, outside, and crossing. |
| `## External entities` | required | The actors and systems the system interacts with. |
| `## What crosses the boundary` | required | The ports: what passes in and out. |
| `## What is out of scope` | required | Stated negatively, on purpose. |

#### term

**What it is.** A defined word (genus and differentia), so every other artifact and every agent reads the corpus unambiguously.
A term carries the uniform opaque id, with the designation in `name` (Title Case, so a defined term reads as one in prose) and any further designations in `aliases`.
A term is invoked in prose by capitalization and resolved by closed-vocabulary lookup against the terms and personas in force at the reading scope.

**Body sections.**

| Section | Req/Opt | Content |
|---|---|---|
| *(lead)* | required | The genus-and-differentia definition. |
| `## Inclusion test` | profile | A decision question that classifies a candidate as in or out. |
| `## Relations` | optional | Typed links from the closed term-relation set (section 8), one per line, each authored once on the end shown. |
| `## Origin` | profile | The grounding: the relevant general-English (Oxford) sense in quotation marks, then the standards or professional lineage. A one-line note for a pure coinage. |
| `## Examples` / `## See also` | optional | Concrete cases; navigation pointers that are not typed relations. |

#### persona

**What it is.** The named actor or segment a need serves.
The holder of the need.
A persona carries the uniform opaque id, with no slug; its designation is in `name`.

**Body sections.**

| Section | Req/Opt | Content |
|---|---|---|
| *(lead)* | required | A one-paragraph role description: who the actor is. No headed sections. |

A persona participates through a frontmatter field, not a verb: a need names its personas by citation in its `persona` list, each entry the standard citation form (name label, relative path, id) written as a quoted YAML string.
There is no authored persona relation and no computed inverse; a "needs served by this persona" view is computed from the field.

---

### The transverse anchor: principle

#### principle

**What it is.** A transverse, weighted normative commitment that obligations enact.
Not a node on the need-to-requirement spine but an anchor that a requirement or convention names.
A principle is adopted to mitigate a risk or realize a gain the corpus cares about.
Its coverage is advisory and asymmetric: a principle enacted by nothing is a pruning candidate; an obligation that enacts no principle is information, not a defect.

**Body sections.**

| Section | Req/Opt | Content |
|---|---|---|
| *(lead)* | required | The named, weighted commitment, in one or two sentences. |
| `## Why this matters` | required | The rationale, and the risk it mitigates or the gain it realizes. |
| `## How to apply` | required | The litmus for when the principle bears, and how to honor it. |
| `## Considered alternative` | recommended | The rejected opposite, and why it was not taken. |
| `## Relations` | optional | Authored links to other principles or terms. The `enactedBy` inverse (the obligations that enact it) is a derived view, never authored. |
| `## Origin` | profile | The grounding: the relevant Oxford sense, plus the standards or professional lineage. |

A principle authors no `enacts`: a requirement or convention names the principle it `enacts`, pointing at the principle, while the principle itself authors none.

---

### Opt-in pack: the discovery pack (Value Proposition Canvas)

These eight kinds are enabled by opting into the discovery pack (section 7): add `discovery` to `packs` in the manifest.
A spine-only corpus holds none of them.
With the pack enabled, a need becomes a *profile* over its Job, Pain, and Gain facets; an offering is a *value map* over its Pain Reliever and Gain Creator facets.
Each facet is its own file: one job, pain, gain, reliever, or creator per file.

| Kind | Segment | Reading |
|---|---|---|
| offering | `offering` | A value map over its Pain Reliever and Gain Creator facets. |
| value-proposition | `vp` | The authored, customer-facing pitch of an offering. |
| system | `system` | The system-of-interest that provides the value; authored only when more than one must be told apart. |
| job | `job` | A single job a need's persona is trying to get done. |
| pain | `pain` | A single pain the persona endures or fears. |
| gain | `gain` | A single gain the persona wants. |
| pain-reliever | `pr` | A single relief an offering provides for a pain. |
| gain-creator | `gc` | A single gain an offering creates. |

A need or an offering keeps its profile file *beside* its facet folder, never inside it: a need's profile is `needs/<slug>.md`, next to `needs/<slug>/`; an offering's profile is `offerings/<slug>.md`, beside `offerings/<slug>/`.
Within a facet folder, a facet file's name is prefixed with its id kind-segment (`job-`, `pain-`, `gain-`, `pr-`, `gc-`) so the kinds read as distinct.

#### offering

| Section | Req/Opt | Content |
|---|---|---|
| *(lead)* | required | The value offered, benefit-led, in the persona's terms. Not solution-free, no *shall*. |
| `## Relations` | required | `addresses` the need. |

#### value-proposition

| Section | Req/Opt | Content |
|---|---|---|
| *(lead)* | required | The authored value-claim, the customer-facing pitch of an offering, in the persona's terms. Benefit-led, no *shall*. Optional as an artifact; where present, the single source product copy, marketing, and sales restate. |
| `## The case` | required at `standard` | The story in the persona's terms and the fit essence; the longer argument that follows the pitch. |
| `## Relations` | required | `expresses` the offering it pitches. |

The value-proposition's only required relation, `expresses`, targets an offering, which is why it lives in the discovery pack and not the spine.

#### job / pain / gain (need facets)

| Section | Req/Opt | Content |
|---|---|---|
| *(lead)* | required | A single job, pain, or gain in the persona's terms, one per file. |
| `## Relations` | required | `partOf` the need. |

A **pain** may add `subkind` (optional): `problem` (an undesired outcome already endured), `obstacle` (in the way of a job), or `risk` (a feared, not-yet-realized outcome).
A **gain** may add `expectation` (optional): `required`, `expected`, `desired`, or `unexpected` (the Kano ladder).
A **pain** or **gain** may also add `validation` (optional), the same five-tier grading a need carries.
All are optional at every profile.

#### pain-reliever / gain-creator (offering facets)

| Section | Req/Opt | Content |
|---|---|---|
| *(lead)* | required | A single offering element that relieves a pain or creates a gain, one per file, benefit-led. |
| `## Relations` | required | `partOf` the offering, and `relieves` a pain (reliever) or `creates` a gain (creator). |

The **fit** (the set of `relieves` and `creates` edges between an offering's map and a need's profile) is a derived view, never authored.

#### system

**What it is.** The system-of-interest that provides an offering's value: a product, a service, a piece of hardware, or any arrangement that achieves a purpose.
A corpus with one system-of-interest keeps it implicit in its single Context; a `system` artifact is authored only when more than one must be told apart.
Its versions are tagged snapshots of the corpus, not a kind of their own.

| Section | Req/Opt | Content |
|---|---|---|
| *(lead)* | required | The system-of-interest that provides the value, in plain terms. |
| `## Relations` | optional | `provides` the offerings, value-propositions, pain-relievers, or gain-creators it delivers. |

The `provides` claim is substantiated by the as-built evidence a tool resolves from the `@intent` citations (section 9); a divergence between what a system claims to provide and what its code cites is a reportable finding, never an authored correction.

> **Deferred, designed.** The **risk** kind and the **plan** pack (a `task` kind and its `dependsOn` dependency graph) are designed but not available in this version.
> They are not enableable kinds in this version; they are noted here so an adopter does not author against them yet.

---

## 6. The substrate

Note and its sibling layers ride one **substrate**: the universal machinery the kinds are supplied onto.
The substrate is the file envelope, the immutable opaque identity scheme, the conformance floor, the universal lifecycle, the typed-relation mechanism (authored once, inverse derived, graph acyclic), the decision edges and term relations, scope and cascade, the three citation surfaces, the conformance profiles, the pack mechanism, and the manifest schema.
The substrate knows no kind: the kinds, their fields, and their legal links are supplied by packs (section 7), each fixed in its own specification.

Splitting the substrate from the packs is what lets one machinery carry a sharp trace spine and a product-discovery vocabulary without welding every kind into one document, and lets kind-legality be checked per enabled pack.
Splitting the required-everywhere floor from profile-gated rigor is what lets the same substrate serve a one-file prototype and a regulated corpus.

---

## 7. The kind packs and the manifest

### Packs

A pack is a declarative selection of kinds: which kinds exist, each kind's id segment, its required and optional frontmatter and body sections, and the relation endpoint rows it contributes to the verb catalogue.
One substrate carries many packs; a corpus names its packs in the manifest, and a checker reads the enabled packs and validates kinds, fields, sections, and links from the files alone.

The method ships **five built-in packs**:

- **The spine pack** (the default). The sharp, V-model-shaped trace spine `need → requirement → specification → verification`, with `decision` and `acceptance-criterion` attached, `term`, `persona`, and `context` underpinning it, `convention` binding the making, and `principle` anchoring it transversely. A corpus that names no pack is on the spine pack.
- **The discovery pack** (opt-in). Adds `offering`, `value-proposition`, `system`, and the facet kinds (`job`, `pain`, `gain`, `pain-reliever`, `gain-creator`). A need becomes a profile over its jobs, pains, and gains; an offering a value map over its relievers and creators; the fit the derived set of `relieves` and `creates` edges. Off by default, because the trace spine is the universal floor and the Canvas is the most methodology-specific layer.
- **The governance pack** (opt-in). Adds `policy`, `standard`, and `procedure`, the instruments an organization states once and its units adopt and adapt, traced by `implements`.
- **The record pack** (opt-in). Adds `record`, the side-car that gives an opaque file a durable id, a lifecycle, and a hash-checked payload.
- **The compliance pack** (opt-in). Adds no kind: it contributes the typed crosswalk relations (`equivalentTo`, `subsetOf`, `intersectsWith`) by which a requirement or convention (and, with governance, a policy or standard) records its correspondence to a control in an external framework, held as read-only artifacts under the framework's namespace. Coverage is derived, tailoring is the cascade's, and carry-forward across a framework version rides `supersedes`.

Packs are **built-in only** in this version: an open or adopter-authored pack mechanism is a named non-goal.

### The manifest

The manifest (`manifest.md` at a scope root) is **configuration, not intent**, and is authoritative for everything that affects validation.
A directory layout may mirror configuration for navigation, but the manifest, not the layout, decides.

| Field | Value |
|---|---|
| `methodVersion` | The method version the corpus conforms to. Required. |
| `namespace` | The corpus's namespace: the identity-space prefix every artifact's id carries, declared once and the same across every repository the corpus spans. Required. |
| `opaqueLength` | The length of the opaque id segment minted in this corpus; optional, default seven. For a multi-root corpus it is set once on the root manifest, sized for the whole namespace ([The multi-root corpus](../loom/note/decisions/multi-root-corpus.md){id=note:dec:0n14gqx}). |
| `profile` | The corpus default conformance profile (`bare`, `standard`, `strict`); any scope may override it. |
| `packs` | The enabled built-in packs; the default is `[spine]`. |
| `vocabulary` | An optional map from a house term to a canonical token, unique both ways, for statuses and verbs; display and input normalization only. A committed file always carries the canonical token. |
| `scope` | The scope block (`id`, `parents`, optional `precedence`) declaring the scope's position in the cascade graph. |
| `roots` | Optional, on a multi-root corpus's root manifest: the member repositories that compose the corpus, each carrying its own manifest under the same namespace ([The multi-root corpus](../loom/note/decisions/multi-root-corpus.md){id=note:dec:0n14gqx}). |

---

## 8. The verb catalogue

A relationship is authored **once, on the dependent (downstream) end**, as a typed, directional link pointing at the artifact it depends on.
The inverse is a **derived view**, computed, never hand-authored.
Every edge reads as a true English sentence: `<dependent> <verb> <governing>`.
You author `satisfies` on a specification pointing at its requirement; the requirement's `satisfiedBy` is computed.
The hierarchical edges are kept acyclic.

A reference is a Markdown link carrying the target's durable id:

```
[visible text](relative/path.md){id=acme:req:sp8g0my}
```

The `{id=...}` is authoritative; the relative path is a navigation convenience a move may stale and a tool restores.

### The catalogue

| Verb | Meaning | From → To (endpoint constraint) | Computed inverse |
|---|---|---|---|
| `addresses` | The obligation or offering deals with the want. | requirement → need \| job; offering → need | `addressedBy` |
| `derivedFrom` | A finer requirement refines a coarser one. | requirement \| specification → requirement | `refinedBy` |
| `satisfies` | A specification commits the design solution a requirement obliges (an assertion, not proof). | specification → requirement | `satisfiedBy` |
| `verifies` | An executed check establishes that an obligation holds. | verification → requirement \| specification \| convention \| acceptance-criterion | `verifiedBy` |
| `enacts` | An obligation puts a transverse principle into practice. | requirement \| convention → principle | `enactedBy` |
| `qualifies` | A solution-free condition the obligation must meet to be accepted. | acceptance-criterion → requirement \| need | `qualifiedBy` |
| `groundedIn` | A decision rests on an artifact as its justification. | decision → need \| requirement \| decision \| principle | `grounds` |
| `amends` | A decision modifies a still-current prior decision in place. | decision → decision | `amendedBy` |
| `decidedBy` | An artifact's content was determined by a decision. | requirement \| specification \| convention → decision | `decides` |
| `expresses` | A value-proposition gives voice to an offering's fit. | value-proposition → offering | `expressedBy` |
| `partOf` | A facet is a constituent of its need or offering. | job \| pain \| gain → need; pain-reliever \| gain-creator → offering | `composedOf` |
| `relieves` | A reliever (or requirement) eases a pain. | pain-reliever \| requirement → pain | `relievedBy` |
| `creates` | A creator (or requirement) brings about a gain. | gain-creator \| requirement → gain | `createdBy` |
| `delivers` | A requirement provides a reliever or creator. | requirement → pain-reliever \| gain-creator | `deliveredBy` |
| `framedBy` | A pain or gain names the job it is felt against, within its own need. | pain \| gain → job | `frames` |
| `provides` | A system claims the value it delivers. | system → offering \| value-proposition \| pain-reliever \| gain-creator | `providedBy` |

**Notes on the spine.** `enacts` is sourced from a requirement or a convention only; a specification reaches a principle transitively through the requirement it satisfies, so a specification never carries `enacts`.
A decision's `## Driven by` is the typed `groundedIn` / `amends` list; the reverse, that a decision determined an artifact's content, is authored as `decidedBy` on that artifact.
A requirement `addresses` the need it serves on every need, whatever packs are enabled; the spine never bends to a pack.
A requirement links straight to a need-facet with that facet's polarity verb (`relieves` a pain, `creates` a gain, `addresses` a job) wherever no offering facet covers that facet; once an offering's reliever or creator covers it, the fit edge for that facet is the offering's, and requirements `delivers` the relievers and creators instead.
The delivers chain is what makes a pitched value proposition an inspectable claim, traced through the offering's facets and the delivering requirements to specifications and verifications; a direct need edge beside a complete delivers chain is redundant and reported, never an error.
A persona is carried by a frontmatter field, not a verb.
`framedBy` is optional and repeatable, authored on the facet, and its target job is `partOf` the same need; its absence carries no completeness claim.
`provides` is authored on the system, optional and repeatable; a coarse claim naming a whole offering expands to that offering's facets in the derived provision view.

### Term-to-term relations (a separate closed set)

Relations between terms are a parallel, closed, ISO-704-grounded associative set, authored once on the end shown, the hierarchical ones acyclic.
They are written as `## Relations` bullets (`- *verb* [Term](path){id=acme:term:k4w7n9t}`), with the subject term implicit:

| Verb | Family | Authored on | Inverse |
|---|---|---|---|
| `is a` | generic | the subordinate concept | `subsumes` |
| `is a value of` | generic | the value | `ranges over` |
| `is part of` | partitive | the part | `is composed of` |
| `carries` | associative | the holder | `is carried by` |
| `scopes` | associative | the Context | `is scoped by` |
| `contrasts with` | associative, symmetric | the alphabetically-earlier term | (symmetric) |
| `relates to` | associative | either end, gloss required | (per gloss) |

The structural verbs above are reused verbatim when a term participates in a structural edge.

### The verb set is fixed

The verb set, its endpoints, and its inverses are a **closed catalogue**; an adopter does not redefine verb semantics, invent a verb meaning, change an endpoint, or alter a computed inverse.
Letting adopters redefine relationship semantics would break interoperability between corpora.

The **only** accommodation is the manifest `vocabulary` map (section 7): a house term may map to a canonical token for display and input only.
If Acme's engineers say "fulfills," the manifest maps `fulfills → satisfies`; the canonical verb, its endpoints, and its inverse are unchanged, and a committed file carries the canonical token `satisfies` only.
A house term never reuses one of the method's own canonical tokens: mapping `implements`, a governance verb, onto `satisfies` would make one token mean two things, so such a map is refused.
The map is display and input normalization, never an authoring vocabulary.

---

## 9. Linking and citation: corpus, code, and commit

Note has three citation surfaces.
Across all three, **the durable id is the only load-bearing part of any citation.**

### In-artifact (within the corpus): the reference-link form

A citation from one artifact to another uses the Markdown reference-link form, with the target's durable id in the `{id=...}` attribute:

```markdown
## Relations

- satisfies: [Checkout Latency Budget](../requirements/system/checkout-latency.md){id=acme:req:sp8g0my}
- enacts: [Plain Naming](../../principles/plain-naming.md){id=acme:principle:eym5t5g}
```

The `{id=...}` is authoritative; the relative path is a convenience a tool restores after a move.
The verb is the relationship verb from section 8, authored on the dependent end.

### Across repositories (a co-located workspace)

A reference may target an artifact in another repository, in the same reference-link form: the target's full durable id (the namespace included) is the authoritative part, and the relative path is the navigation convenience.

```markdown
- derivedFrom: [Retention Standard](../../platform/loom/note/requirements/system/retention.md){id=platform:req:k7w2n9p}
```

In a co-located workspace, sibling repositories checked out together (for example under West or the repo tool), that relative path resolves on disk and the link reads cold with no tool, exactly as an in-corpus reference does.
Laid out differently, the path may not resolve; the id still names the target, so the path is repaired, by hand or by a tool, rather than the reference being lost.
A reference whose repository is not currently present is reported unresolved, not invalid, and whole-graph properties are computed over the reachable closure.

The full id carries the namespace, so a reference is unambiguous across repositories that use distinct namespaces; keeping ids unique within a namespace that several repositories share is an identity concern (section 3), not a property of the reference form.
This is a live, files-alone reference; pinning it to an upstream version, freezing a copy, and the rest of cross-repository inheritance are the heavier disciplines a tool adds when a corpus depends on another's intent.

### In-code (from a file outside the corpus): a durable id behind a fixed marker

Source code is outside the corpus, so it cannot use a relative-path reference link.
Instead a code comment carries the durable id behind a fixed marker, with a human-readable label that is expected by convention but never checked:

```javascript
// @intent Satisfies: acme:req:sp8g0my (checkout latency budget)
function settleCheckout(cart) { ... }
```

A tool resolves the id; the parenthetical label is for the human reader and a tool ignores it.
If the label drifts from the artifact's name, nothing breaks, because the label is never the citation.

### In-commit: a durable id in a trailer

A citation from a Git commit lives in a trailer at the foot of the message, in the `Signed-off-by:`-style block, behind a key.
The id never appears in the subject or the prose.
The trailer keys are the relationship verbs as Title-Case tokens, with `Refs:` the neutral fallback when the author asserts a link without claiming a specific structural role:

```
feat(checkout): cache the cart pricing read

Satisfies: acme:req:sp8g0my
Enacts: acme:principle:eym5t5g
Refs: acme:dec:pxnjmcd
```

### The convention is expected, never checked

The Title-Case verb keys (`Satisfies:`, `Verifies:`, `Enacts:`, `Refs:`) are an **expected, never-checked convention**.
A tool may raise an advisory, non-blocking plausibility warning on an unknown key or an implausible target kind, but it never blocks: a commit has no source kind for a checker to validate against, so only the resolvability of the id is load-bearing.

**Agent guidance.** Default to `Refs:` unless the structural claim is verifiable; reach for `Satisfies:`, `Verifies:`, or `Enacts:` only when you can name the structural role with confidence.
Committed files, code comments, and commit trailers carry **canonical tokens only**; the vocabulary map (section 7) is display and input normalization, never an authoring vocabulary.

### Citation, not command (the boundary)

These are **citation** keys.
They state a relationship; they never transition state.
Note deliberately excludes the imperative state-change family (`Closes`, `Fixes`, `Resolves`, and Jira's `#done` / `#close`), because those keywords *command* a state change: on most platforms they auto-close the referenced item on merge.
A citation in a commit must never, by itself, mark a requirement done or accepted.
Whether an obligation is met is a verdict owned by the Orchestrating Authority and established by a verification's evidence, not by a word in a commit footer.
A citation states a relationship; it never transitions state.

---

## Agent guidance (at a glance)

- **Discover the corpus** by the two-step algorithm: read root `loom.md` and follow its `root:` if present; otherwise use `loom/` (section 1).
- **Read the nearest manifest** before authoring: it fixes the profile, the enabled packs, and the scope (sections 1, 7).
- **A draft decision is provisional.** A decision in `status: draft` is a proposal, not yet ratified; do not treat it as the operative source (section 4).
- **`## Out of scope` is recommended at standard** on an acceptance-criterion: state negatively what the criterion does not cover (section 5).
- **Default to `Refs:`** in commit trailers and code comments unless the structural claim is verifiable; use canonical tokens only (section 9).

---

## Patterns for a regulated Adopter

Note buys cheap documentation wins for a regulated corpus with no new machinery:

- **A baseline is a Git tag.** A released, frozen state of the corpus is a tag, not a stored kind; the corpus at that tag is the baseline.
- **Change control is the supersede pattern.** A controlled change is a new artifact that supersedes the old (`supersedes` on the successor, `superseded_by` on the retired artifact), with the retired one archived (section 1), so the prior obligation stays legible.
- **The verification `method` enum maps to the standards.** The enum (`test`, `analysis`, `inspection`, `demonstration`, `formal-proof`) maps to ISO 26262 table 9 and to ASPICE, so a verification's method reads directly against the assessment framework.
