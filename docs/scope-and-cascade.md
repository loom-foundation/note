# Scope and cascade

How to state an obligation once and let it inherit, deviate, and resolve across many scopes.
This is orientation and applied guidance, not normative text; the binding grammar and resolution procedure live in [Scope and cascade](../loom/note/specifications/note/scope-and-cascade.md){id=note:spec:1r673tc}, and the model it fixes lives in [Scope and cascade representation](../loom/note/decisions/scope-and-cascade-representation.md){id=note:dec:e3v7s8q}.
The substrate specification ([The substrate](../loom/note/specifications/note/substrate.md){id=note:spec:tkhd63e}) fixes the manifest schema, the file envelope, and the identity scheme that the examples below rely on.
The first six worked examples below are the situations from [State a shared obligation once](../loom/note/needs/state-obligation-once.md){id=note:need:257yf29}; a seventh shows a non-obligation kind (a persona) cascading the same way.

## What scope and cascade are for

A Scope is the position at which intent becomes load-bearing and below which it is inherited ([Scope](../loom/note/terms/relations-scope-and-traceability/scope.md){id=note:term:rqbkaxn}).
The Cascade composes that inherited intent down the graph: an inner scope adds to it, replaces it, or disinherits it, and the result at any position is the Effective Intent ([Cascade](../loom/note/terms/relations-scope-and-traceability/cascade.md){id=note:term:5b6cbtr}, [Effective Intent](../loom/note/terms/relations-scope-and-traceability/effective-intent.md){id=note:term:b0f7xzp}).
The point is to state a shared obligation once, inherit it everywhere it holds, and deviate loudly where it does not, so policies are not copy-pasted and silently drift apart.

Scope is opt-in, and the on-ramp is free.
A sustained body of work that occupies a single Scope, whether a software system, a hardware product, a process, or a methodology like this corpus, declares no scope block at all and writes no deviation: it inherits nothing and pays nothing.
The grammar below is earned only when intent must hold across more than one Scope.

Cascade is not just for requirements.
Every kind carries the same optional `scope` field, so anything that holds across scopes inherits the same way: a governance policy, standard, or procedure; a convention; a term; a persona; a principle; or a Context.
The worked examples below lead with requirements because they are the easiest to read, but the operators (`add`, `replace`, `disinherit`) apply unchanged to any of these kinds, and a non-requirement example (a cascading persona) is shown alongside them.
The single thing that does not cascade is a Record's opaque payload, which is carried for identity and provenance, never read as intent.

## The building blocks

### The scope block

A Scope is declared once, at its scope root, in a `scope` block on that scope's `manifest.md`.
The block carries the scope id and the parent edges; a root scope has no parents.

```yaml
scope:
  id: acme
```

```yaml
scope:
  id: acme-payments
  parents: [acme]
```

The `manifest.md` at the scope root is configuration, not intent, and is authoritative for everything that affects validation.
Beyond the `scope` block, it carries:

| Field | Purpose |
|---|---|
| `methodVersion` | The method version the corpus conforms to. Required. |
| `namespace` | The corpus's namespace: the identity-space prefix every artifact's id carries. Required. |
| `profile` | The corpus default conformance profile (`bare`, `standard`, or `strict`). |
| `packs` | The enabled kind packages (default: `[spine]`). List `[spine, discovery]` to enable the discovery pack. |
| `vocabulary` | An optional map from a house term to a canonical token, for statuses and verbs; display and input normalization only. |
| `scope` | The scope block (`id`, `parents`, optional `precedence`) declaring the scope's position in the cascade graph. |

The manifest hosts the scope block because scope identity and parent edges are configuration, not intent, and a cross-cutting scope (a security or privacy domain) has no Context to carry it.
Where a scope has exactly one structural parent, placing its root inside the parent's tree mirrors that one edge as a reading convenience, but the `parents` list is authoritative and a cross-cutting or additional parent is always named by id.
See [Adopter corpus placement](../loom/note/decisions/corpus-placement.md){id=note:dec:q2v7nk3} for why the directory tree is only the spanning tree of the Scope graph.

### The artifact scope field

An artifact carries an optional `scope` field naming the scope id at which its intent first becomes load-bearing; below that scope the intent is inherited.

```yaml
---
id: acme:req:...
name: Data retention
kind: requirement
scope: acme
---
```

Omitted, the field takes the scope of the enclosing scope root, so the common case pays nothing.
It is authored explicitly only where an artifact is load-bearing at a scope other than the one its location implies.

### The deviation operators

An inner scope relates to an inherited obligation in a `## Deviation` section on the inheriting artifact, one bullet per deviation.
There are three operators; the spec fixes their exact semantics, summarized here only to teach.

- `add`: the local obligation genuinely co-holds with the inherited one; both apply.
- `replace`: the local obligation supersedes a conflicting inherited one at this scope and below.
- `disinherit`: the inherited obligation is dropped here, with no replacement.

A `replace` or a `disinherit` carries a `Rationale:` line, because it is the loud direction the cascade surfaces; an `add` carries none, because a strengthening is the safe, silent case.

```markdown
## Deviation

- replace [Data retention](../../acme/requirements/retention.md){id=acme:req:...} from acme.
  Rationale: SOX obliges seven-year retention for this subsidiary.
```

Two rules decide the operator, and they are easy to get wrong.
A tighter or conflicting threshold (a different value on the same point) is a `replace`, never an `add`: layering it as an `add` would record both as holding when they cannot.
A brand-new local obligation that relates to no inherited one carries no `## Deviation` entry at all; it is just a new requirement.
No entry names its author: attribution is the artifact's Git provenance, never a self-declared field.

### Declared precedence

Where two incomparable parents conflict on the same point and the conflict recurs, an author may settle it once with a `precedence` entry in the scope block, naming the pair, the point, and a rationale.

```yaml
scope:
  id: acme-checkout
  parents: [acme-payments, acme-privacy, acme-security]
  precedence:
    - prefer: acme-privacy
      over: acme-security
      on: "access-log retention"
      rationale: "data minimization governs PII in access logs here"
```

It orders only the pair and point it names; it invents no general distance metric.

### Context narrowing

A Context is not deviated with operators.
A subsystem re-authors its own Context, narrowed from the one it inherits, and the cascade detects the change by comparing boundaries: narrowing (dropping an external entity, tightening what crosses) is silent, and widening (admitting an entity the parent excluded) is loud and carries its rationale in the Context body ([Context model](../loom/note/decisions/context-model.md){id=note:dec:b7w3k9n}).
Obligations and Contexts share one cascade behavior, silent on a strengthening or a narrowing and loud on a removal or a widening; only the representation differs.

## How resolution works

Effective intent is a derived view, never stored (the one exception is materialization).
A reader resolves it at a target scope by walking the `parents` edges to gather every ancestor, applying each `## Deviation` operator, ordering comparable conflicts by proximity (the nearer source governs, silently), and surfacing every incomparable tie and every removal.
The walk is performable by an unaided human from the files alone; the spec fixes the exact procedure and the validation rules a checker applies.

## The seven scenarios

Each scenario below shows the files an author would write, then a sentence on how the cascade resolves them.
Ids in the snippets are elided as `acme:req:...`; real ids are the opaque seven-character form.

### 1. Regulated subsidiary (strengthen, then opt out)

A holding company sets data retention once organization-wide; an audit subsidiary under SOX tightens it, and an ephemeral-sandbox app opts out entirely.

The organization states retention once at the root scope:

```yaml
# acme/loom/note/manifest.md
scope:
  id: acme
```

```markdown
<!-- acme/loom/note/requirements/data-retention.md -->
Acme shall retain customer records for at least two years.
```

The audit subsidiary has a conflicting, tighter threshold on the same point, so it is a `replace`:

```yaml
# acme-audit/loom/note/manifest.md
scope:
  id: acme-audit
  parents: [acme]
```

```markdown
<!-- acme-audit/loom/note/requirements/data-retention.md -->
The audit subsidiary shall retain customer records for at least seven years.

## Deviation

- replace [Data retention](../../acme/requirements/data-retention.md){id=acme:req:...} from acme.
  Rationale: SOX obliges seven-year retention for an entity in scope for audit.
```

The sandbox app drops the obligation, so it is a `disinherit`:

```markdown
<!-- acme-sandbox/loom/note/requirements/data-retention.md -->
## Deviation

- disinherit [Data retention](../../acme/requirements/data-retention.md){id=acme:req:...} from acme.
  Rationale: the sandbox handles only throwaway session data; retention is a category error here.
```

Resolution: at `acme-audit` the nearer seven-year obligation governs and surfaces as a recorded replacement; at `acme-sandbox` the removal surfaces loud and routes to the retention owner; everywhere else the two-year obligation holds unchanged.

### 2. Mono-repo with a shared baseline (replace and extend per product)

A security and data-handling baseline applies to every service in the repo; a payments service layers PCI obligations on top, and a marketing site opts out of rules that do not apply.

The baseline is authored once at the root, and each app is a child scope by containment:

```yaml
# monorepo/loom/note/manifest.md
scope:
  id: acme
```

```yaml
# monorepo/packages/payments/loom/note/manifest.md
scope:
  id: acme-payments
  parents: [acme]
```

The PCI obligations are genuinely additive new requirements that relate to no single inherited rule, so they carry no `## Deviation` entry; they are simply new requirements at `acme-payments`.
Where a PCI rule tightens a specific baseline rule (say a shorter key-rotation interval), that one is a `replace`:

```markdown
<!-- payments/loom/note/requirements/key-rotation.md -->
The payments service shall rotate encryption keys every ninety days.

## Deviation

- replace [Key rotation](../../../loom/note/requirements/key-rotation.md){id=acme:req:...} from acme.
  Rationale: PCI DSS requires a ninety-day rotation, tighter than the annual baseline.
```

The marketing site opts out of an inapplicable rule with a `disinherit`:

```markdown
<!-- marketing-site/loom/note/decisions/baseline-opt-out.md -->
## Deviation

- disinherit [Cardholder-data handling](../../../loom/note/requirements/cardholder-data.md){id=acme:req:...} from acme.
  Rationale: the public marketing site processes no cardholder data.
```

Resolution: the baseline holds for every service; the payments key-rotation `replace` resolves by proximity and is recorded; the marketing opt-out surfaces loud.

### 3. Platform standards inherited by app teams

A platform team defines auth, logging, and observability standards inherited by every application team; an app overrides a standard only where it has a recorded, justified exception.

The standards live in the platform scope (often its own repository), and an app declares it as a parent by id, resolving across the repo boundary:

```yaml
# acme-platform/loom/note/manifest.md
scope:
  id: acme-platform
```

```yaml
# acme-checkout/loom/note/manifest.md
scope:
  id: acme-checkout
  parents: [acme-platform]
```

An app that conforms writes nothing: it inherits the standards as effective intent.
An app with a justified exception that supersedes one standard writes a `replace`:

```markdown
<!-- acme-checkout/loom/note/decisions/logging-exception.md -->
## Deviation

- replace [Structured-logging standard](.../requirements/logging-standard.md){id=acme:req:...} from acme-platform.
  Rationale: this service ships to an air-gapped customer whose SIEM ingests only syslog.
```

Resolution: the standards hold for every app by inheritance; the one recorded exception resolves by proximity and stays visible at the app where it occurs.

### 4. Cross-cutting concern across divisions (multi-parent)

A privacy / GDPR requirement applies to products that live under different divisions, so a product inherits both from its structural parent (its division) and from the cross-cutting privacy concern owned elsewhere.

The privacy concern is its own named scope with no Context (a cross-cutting scope carries obligations but has no boundary):

```yaml
# acme/loom/note/privacy/manifest.md
scope:
  id: acme-privacy
  parents: [acme]
```

```markdown
<!-- acme/loom/note/privacy/requirements/gdpr-erasure.md -->
A system holding personal data shall erase it on a verified right-to-be-forgotten request.
```

A wallet product under the payments division and a newsletter product under the marketing division each carry two parents.
The structural parent is mirrored by containment; the cross-cutting privacy edge is always carried by id:

```yaml
# acme/divisions/payments/products/wallet/loom/note/manifest.md
scope:
  id: acme-wallet
  parents: [acme-payments-div, acme-privacy]
```

```yaml
# acme/divisions/marketing/products/newsletter/loom/note/manifest.md
scope:
  id: acme-newsletter
  parents: [acme-marketing-div, acme-privacy]
```

Each product then authors its own erasure design as new local intent (a specification that satisfies the inherited requirement), with no `## Deviation` entry, because it relates to the inherited obligation by satisfying it, not by adding, replacing, or removing it.
Resolution: both products inherit `gdpr-erasure` from `acme-privacy` regardless of their division, the privacy owner states the rule once, and each product's effective intent shows it sourced from the cross-cutting parent.
If the division and the privacy parent ever conflicted on the same point, they sit at incomparable positions, so the conflict would surface for explicit resolution rather than be auto-tiebroken, and a recurring tie could be settled with a `precedence` entry naming the two parents and the point.

### 5. Incubator with many entities and apps

An incubator defines common policies once at the root (Privacy, GDPR, data-lifecycle management, right-to-be-forgotten), reused by most entities and their apps; each entity can opt out, change parameters, or extend further.

The common policies are authored once at the incubator root, and each entity is a child scope:

```yaml
# incubator/loom/note/manifest.md
scope:
  id: incubator
```

```yaml
# incubator/entities/acme/loom/note/manifest.md
scope:
  id: incubator-acme
  parents: [incubator]
```

The three deviation shapes all appear here, each picked by its actual relation to an inherited policy:

```markdown
<!-- an entity that changes a parameter: a conflicting value on the same point -->
## Deviation

- replace [Data-lifecycle retention](../../../loom/note/requirements/data-lifecycle.md){id=acme:req:...} from incubator.
  Rationale: this entity's regulator mandates a five-year minimum, not the default eighteen months.
```

```markdown
<!-- an entity that drops an inapplicable policy -->
## Deviation

- disinherit [Right to be forgotten](../../../loom/note/requirements/rtbf.md){id=acme:req:...} from incubator.
  Rationale: this entity is a B2B analytics tool that holds no personal data subject to erasure.
```

An entity that extends the policies further authors new requirements with no `## Deviation` entry (new local intent that relates to no inherited obligation), or, where a stricter rule co-holds with an inherited one rather than conflicting, an `add`.
Resolution: most entities inherit the common policies untouched; each replace and disinherit surfaces at the entity where it occurs and the policy owner states each baseline once.
When an entity is funded and spun out, the intent it inherited must travel with it, which is captured separately by [Self-contained extraction of inherited intent](../loom/note/requirements/stakeholder/self-contained-extraction.md){id=note:req:qq6eywy}.

### 6. Nested organizations

A parent organization with child organizations, which in turn have departments and multiple systems, needs the same state-once / inherit / deviate flexibility cascading down the whole chain.

Each level is a scope whose single structural parent is mirrored by containment, so the chain reads straight off the tree:

```yaml
# group/loom/note/manifest.md
scope:
  id: group
```

```yaml
# group/orgs/retail/loom/note/manifest.md
scope:
  id: group-retail
  parents: [group]
```

```yaml
# group/orgs/retail/departments/fulfillment/loom/note/manifest.md
scope:
  id: group-retail-fulfillment
  parents: [group-retail]
```

```yaml
# group/orgs/retail/departments/fulfillment/systems/wms/loom/note/manifest.md
scope:
  id: group-retail-wms
  parents: [group-retail-fulfillment]
```

A group-wide obligation stated once at `group` is in force at every level beneath it.
A deviation at any level uses the same three operators against the source it inherits, naming the source scope it came from:

```markdown
<!-- the warehouse system tightens a group access-control floor -->
## Deviation

- replace [Access-control floor](../../../../../../loom/note/requirements/access-control.md){id=acme:req:...} from group.
  Rationale: the warehouse handles regulated pharmaceutical stock and requires two-person authorization.
```

Resolution: the obligation cascades the full depth of the chain; the warehouse `replace` resolves by proximity because `group` and `group-retail-wms` are comparable (they lie on one parent chain), and the nearer warehouse obligation governs silently as recorded intent.
Because each level adds exactly one parent edge, every scope's effective intent is the walk up its own chain, and a deviation at a middle level (a department) is itself inherited by the systems beneath it.

### 7. A persona cascading (a non-obligation example)

The cascade is not requirement-only; any kind that carries the `scope` field inherits the same way. A persona, the named actor a body of work serves, cascades like any intent: a high scope defines it once, and a descendant inherits it as-is, adapts it locally, or disinherits it with a reason.

The organization defines its `Field technician` persona once at the root scope:

```yaml
# acme/loom/note/manifest.md
scope:
  id: acme
```

```markdown
<!-- acme/loom/note/personas/field-technician.md -->
The Field Technician services installed equipment on-site, often offline, and needs every procedure usable from a phone in a low-connectivity environment.
```

A descendant that serves the same actor unchanged writes nothing: it inherits the persona as effective intent, exactly as an inherited requirement is inherited.

A regulated subsidiary whose technicians work under a stricter certification regime adapts the persona locally. The local definition supersedes the inherited one on the same actor, so it is a `replace` carrying its rationale:

```markdown
<!-- acme-medical/loom/note/personas/field-technician.md -->
The Field Technician services installed equipment on-site and holds a current biomedical-equipment certification, so a procedure may assume credentialed handling of regulated devices.

## Deviation

- replace [Field technician](../../acme/personas/field-technician.md){id=acme:persona:...} from acme.
  Rationale: this subsidiary's technicians are certified for regulated medical devices, which the org-wide persona does not assume.
```

A purely cloud subsidiary that serves no on-site actor at all disinherits the persona, with a reason:

```markdown
<!-- acme-saas/loom/note/personas/field-technician-opt-out.md -->
## Deviation

- disinherit [Field technician](../../acme/personas/field-technician.md){id=acme:persona:...} from acme.
  Rationale: this subsidiary ships only hosted software; it has no field technician among the actors it serves.
```

Resolution: most descendants inherit the org-wide persona untouched; the medical subsidiary's `replace` resolves by proximity and stays recorded at the scope where it occurs; the SaaS subsidiary's `disinherit` surfaces loud and routes to the persona's owner. The mechanics are identical to the obligation scenarios above; only the kind being cascaded differs.

## Picking the operator, in one line

A genuinely additive obligation that co-holds is an `add` (or, if it relates to no inherited rule, just a new requirement with no `## Deviation` entry).
A tighter or conflicting threshold on the same point is a `replace`.
An opt-out is a `disinherit`.
A `replace` or a `disinherit` always carries its `Rationale:`; an `add` never does.
