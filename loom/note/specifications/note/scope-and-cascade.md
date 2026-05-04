---
id: note:spec:1r673tc
name: Scope and cascade
kind: specification
status: current
authority: []
---

This specification fixes the grammar of scope and cascade: the frontmatter that declares a scope and its parent edges, the field by which an artifact records the scope it is load-bearing at, the authored syntax of the add, replace, and disinherit deviation operators and of a declared precedence, the deterministic procedure that resolves effective intent at a scope, and the validation rules a checker applies.

It fixes the representation proposed in [Scope and cascade representation](../../decisions/scope-and-cascade-representation.md){id=note:dec:e3v7s8q} and follows the file envelope, frontmatter schema, and relation grammar of [The substrate](substrate.md){id=note:spec:tkhd63e}.

Scope declaration is opt-in.
A sustained body of work that occupies a single scope, whether a software system, a hardware product, a process, or a methodology like this corpus, declares no scope block and writes no deviation: it inherits nothing and pays nothing.
The grammar below is earned only when intent must hold across more than one scope.

The cascade is general over kinds, not a feature of one.
Every kind carries the optional `scope` field as common frontmatter ([The substrate](substrate.md){id=note:spec:tkhd63e}), so every artifact records the scope at which its intent is load-bearing and is inherited below it.
The grammar fixed here therefore governs any kind that carries intent across scopes: a requirement, a governance policy, standard, or procedure, a convention, a term, a persona, a principle, or a Context.
"Obligation" and "Context" name the two representational *shapes* the cascade takes, not a restriction to a single kind.
An obligation, in this specification, means any discrete piece of intent an inner scope can strengthen, supersede, or drop, whatever its kind; a Context is the one holistic boundary statement a scope carries, deviated by re-authoring rather than by operators (see [Context narrowing](#context-narrowing)).
The one piece of intent that does not cascade is a record's opaque payload, which is carried for identity and provenance and is explicitly not diffed, cascaded, or read as obligations ([Record pack](../../decisions/record-pack.md){id=note:dec:hjv67df}).

## Scope declaration

A scope is a named position in the inheritance graph.
It is declared once, at the scope root, in a `scope` block on the scope's manifest (the `manifest.md` at the scope's layer root).
The manifest is the one host every scope shares: scope identity and parent edges are configuration, which the manifest already homes, not intent, and a cross-cutting scope has no Context to carry the block.
The block carries two fields:

| Field | Required | Value |
|---|---|---|
| `id` | required | The scope id: a stable, corpus-unique label for the scope, used as the unit the cascade graph is built from. It is independent of the directory the scope sits in, so a move never changes it. |
| `parents` | optional | A list of scope ids the scope inherits from. Absent or empty means a root scope with no parent. A single-scope corpus declares no scope block at all, which is the degenerate case of no parents. |

```yaml
scope:
  id: acme-payments
  parents: [acme, acme-privacy]
```

Where a scope has exactly one structural parent, directory containment may mirror that one edge: placing the scope's root inside the parent's tree records the same parent the spanning tree shows.
The `parents` list remains authoritative.
A cross-cutting or additional parent is never expressed by location; it is always named by id in `parents`.

A declared precedence, where one is authored, is a third entry of the scope block; its syntax is given under [Declared precedence](#declared-precedence) below.

## Recording an artifact's load-bearing scope

An artifact records the scope at which its intent first becomes load-bearing with an optional `scope` field in its own frontmatter, naming a scope id:

| Field | Required | Value |
|---|---|---|
| `scope` | optional | The scope id at which the artifact's intent first applies; below that scope the intent is inherited. Omitted, the artifact takes the scope of the scope root that encloses it; in a single-scope corpus the field is always omitted. |

The field is authored explicitly only where an artifact is load-bearing at a scope other than the one its location implies.
In the common single-parent, single-location case the field is omitted and the enclosing scope governs, so the default costs nothing.

## Deviation operators

An inner scope relates to an inherited obligation through one of three operators, authored on the inheriting artifact in a `## Deviation` section.
The section is a bullet list, one deviation per entry.
Each entry names the operator, names the inherited source by the relation-link form `[Title](path.md){id=...}` of [The substrate](substrate.md){id=note:spec:tkhd63e}, and names the scope the source came from; a `replace` or `disinherit` entry also carries a rationale line.

| Operator | Semantics |
|---|---|
| `add` | The inherited obligation stays in force; the local obligation applies alongside it. Both hold at this scope and below. The local obligation must genuinely co-hold with the inherited one, not conflict with it on the same point. |
| `replace` | The local obligation supersedes the inherited one at this scope and below; the inherited obligation no longer applies here. |
| `disinherit` | The inherited obligation is dropped at this scope and below, with no replacement. |

A `replace` or `disinherit` entry is written:

```markdown
## Deviation

- <operator> [Inherited title](relative/path.md){id=<namespace>:<kind>:<opaque>} from <source-scope-id>.
  Rationale: <why this scope deviates>.
```

An `add` entry omits the rationale, since a strengthening is the safe, silent case the cascade does not surface:

```markdown
## Deviation

- add [Inherited title](relative/path.md){id=<namespace>:<kind>:<opaque>} from <source-scope-id>.
```

The rationale is required on a `replace` and a `disinherit`, the loud cases, so a reviewer reads why an inherited obligation was superseded or dropped at the scope where it occurs.
No entry names its author: attribution is the artifact's own Git provenance (commit authorship and signature), the corpus's trust root, never a self-declared field, which any actor with file access could forge. Nothing in the entry grants or withholds permission to deviate.

Choose the operator by the actual relation to the named source.
An `add` records only an obligation that genuinely holds alongside the inherited one; an obligation that conflicts with the inherited one on the same point, a tighter threshold or a different value, is a `replace`, never an `add`, so the conflict is recorded with its rationale rather than silently layered as though both held.
A brand-new local obligation that relates to no inherited one carries no `## Deviation` entry at all: the operators exist to record a deliberate relation to a named inherited obligation, not to announce every new requirement.

### Context narrowing

A Context is not deviated with these operators.
A Context is a single holistic boundary statement, one per scope, so a subsystem re-authors its own Context, narrowed from the one it inherits, rather than authoring `## Deviation` entries against it.
The resolver detects the deviation by comparing the inherited effective boundary to the local one: narrowing (dropping an external entity, tightening what crosses) is the silent strengthening, and widening (admitting an external entity, loosening what crosses) is the loud, surfaced deviation, the inverse of the obligation rule where a removal is the loud direction.
A widening, being the loud direction, carries a rationale in the re-authored Context's body, the way a `replace` or a `disinherit` carries one; attribution is the Context's Git provenance, as for any deviation.

### Declared precedence

Where two parents are incomparable along the scope graph and their conflict on a named point recurs, an author may declare, once, that one parent precedes the other for that point.
The declaration is a `precedence` entry of the `scope` block at the scope root:

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

A declared precedence is a visible, attributable deviation: it carries its own `rationale`, is attributable through Git provenance like any operator entry, and converts a recurring surfaced tie into authored intent for the one point it names.
It orders only the pair and point it names; it invents no general distance metric.

## Effective-intent resolution

The effective intent at a scope is computed by walking the scope graph and applying the operators.
The procedure is deterministic and performable by an unaided human reader from the files alone; no step requires a tool.

To resolve the effective intent at a target scope:

1. **Gather the ancestor set.**
   From the target scope, follow `parents` edges transitively to collect every scope the target inherits from.
   The graph is acyclic (see [Validation rules](#validation-rules)), so this terminates.

2. **Collect the contributing sources.**
   For each point of intent, gather every authored obligation in force across the ancestor set and the target, together with each `## Deviation` entry that names it.

3. **Apply the operators.**
   An `add` keeps both the inherited obligation and the local one in force.
   A `replace` drops the inherited obligation at the target and keeps the local one.
   A `disinherit` drops the inherited obligation with no replacement.

4. **Order comparable conflicts by proximity.**
   Two conflicting sources are comparable when one lies on a parent chain above the other; the nearer source (fewer parent steps from the target) governs, silently, because it is authored intent.
   Where a source is reachable from the target by paths of different lengths, its distance is the shortest such path.
   Proximity is a partial order: nearer is defined only between comparable scopes.

5. **Surface incomparable ties.**
   Two conflicting sources at incomparable positions (neither reachable from the other by parent edges) are surfaced, naming every contributing source with its scope and owner.
   They are never auto-tiebroken, unless a declared precedence at the target names that exact pair and point, in which case the declared order resolves it and the resolution is recorded as authored intent.

6. **Surface every removal, loud.**
   A `disinherit` (and, for a Context, a widening) is always surfaced, attributable, and rationale-bearing, even when proximity would make its precedence unambiguous, so that an inherited obligation is never silently dropped.

The result is a derived view: the effective obligation at the target together with the trace of each contributing source and the operator applied.
It is never authored as a second artifact while the corpus is live; the one deliberate exception is materialization, which severs the link and records provenance ([The substrate](substrate.md){id=note:spec:tkhd63e}, the `materialized` frontmatter block).

## Validation rules

A checker applies the following rules; each is decidable from the files alone, with no tool required to read the corpus.

- **Acyclicity.**
  The `parents` edges form a directed acyclic graph: no scope reaches itself by following parent edges. A cycle is invalid, because resolution would not terminate.

- **Resolvability.**
  Every scope id named in a `parents` list, in a `scope` field, in a `## Deviation` source, or in a `precedence` entry resolves to a declared scope. A `parents` scope id may name a scope in another repository, resolving across the boundary per [Cross-repository resolution](../../requirements/system/cross-repository-resolution.md){id=note:req:dxxvabc} at the pinned upstream version; an upstream not currently resolvable is reported as unresolved rather than invalid, and the global properties below are asserted over the resolvable closure.

- **Deviation completeness.**
  Every `## Deviation` entry names an operator from the closed set (`add`, `replace`, `disinherit`), names an inherited source by resolvable id, and names the source scope; a `replace` or `disinherit` entry also carries a rationale. An entry missing any of these is invalid, so that no replacement or removal is unexplained. Attribution is not a field and is not checked here: it is the entry's Git provenance.

- **Deviation targets an inherited source.**
  The source a `## Deviation` entry names is in force at one of the target scope's ancestors. A deviation against a source the scope does not inherit is invalid.

- **Precedence well-formedness.**
  A `precedence` entry names two distinct parent scopes (`prefer`, `over`), both in the scope's ancestor set, a `on` point, and its own rationale. A precedence over scopes that are not both ancestors, or that are already comparable, is invalid.

- **Context narrows monotonically.**
  A re-authored Context may narrow the boundary it inherits silently; a widening (admitting an external entity the parent excluded, or loosening what crosses) is surfaced as loud and is invalid unless it carries a rationale in the Context body.

- **No stored effective intent.**
  No artifact is authored as a resolved effective-intent result while the corpus is live; only a `materialized` block carries a frozen copy, and it records provenance.

The checker reports; it decides nothing about who may deviate or whether a surfaced conflict is acceptable. Permission and resolution belong to the Orchestrating Authority ([Compute and Report](../../principles/compute-and-report.md){id=note:principle:6e7f28k}).

## Rationale

The scope graph lives in frontmatter so that resolution is location-independent: a move never breaks an inheritance edge, and a multi-parent or cross-cutting edge, which has no single location, is carried by id ([Scope and cascade representation](../../decisions/scope-and-cascade-representation.md){id=note:dec:e3v7s8q}).
Directory containment mirrors at most the single structural parent, so the tree stays a reading convenience and the frontmatter stays the single source of truth.

Three distinct operators rather than one keep a strengthening, a replacement, and a removal mechanically distinguishable, which is what lets a checker hold removal loud while letting a strengthening pass silently.
Carrying a rationale on every replacement and removal makes a dropped obligation legible at the scope where it occurs, rather than buried in a parent diff; attribution comes from Git provenance, not a forgeable field.

A partial order over proximity, with incomparable ties surfaced and every removal surfaced, is the resolution behavior decided for the cascade; representing it as a walk a human can perform keeps the corpus operable with no tool.
Obligations and Contexts share one cascade behavior, silent on a strengthening or a narrowing and loud on a removal or a widening, but use representations fit to their shapes: authored operators for a discrete obligation, boundary comparison for a holistic Context.

## Relations

- satisfies: [Scope and inheritance](../../requirements/system/scope-and-inheritance.md){id=note:req:96smmcv}
- satisfies: [Effective-intent resolution](../../requirements/system/effective-intent-resolution.md){id=note:req:5xnajsm}
- satisfies: [Deviation operators on inherited intent](../../requirements/system/deviation-from-inherited-intent.md){id=note:req:sd7ch4m}
- satisfies: [Visible, attributable deviation](../../requirements/system/visible-attributable-deviation.md){id=note:req:64eknb1}
- decidedBy: [Scope and cascade representation](../../decisions/scope-and-cascade-representation.md){id=note:dec:e3v7s8q}
