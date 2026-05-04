---
id: note:dec:e3v7s8q
name: Scope and cascade representation
kind: decision
status: current
decided: 2026-06-11T03:55:44Z
---

A scope is a named position in the inheritance graph, identified by a stable scope id and declaring its parent edges and any author-declared precedence in frontmatter, with directory containment permitted to mirror the single structural parent as a reading convenience only.
An artifact records which scope it is load-bearing at, and an inner scope relates to inherited intent through three authored operators (add, replace, disinherit), each recorded explicitly and the loud ones (replace, disinherit) carrying a rationale, so that the cascade and its deviations are represented in the files and checkable from them alone.

This decision fixes the representation model.
A sustained body of work that lives in a single scope declares nothing and pays nothing; the machinery is earned only when intent must hold across more than one scope, whether the work is a software system, a hardware product, a process, or a methodology like this corpus.

## Context

The requirements for scope and cascade are settled but representation-absent.
[Scope and inheritance](../requirements/system/scope-and-inheritance.md){id=note:req:96smmcv} requires that intent can be expressed at the scope where it becomes load-bearing, inherited by the scopes beneath it, sourced from more than one parent, and kept acyclic.
[Deviation operators on inherited intent](../requirements/system/deviation-from-inherited-intent.md){id=note:req:sd7ch4m} requires three defined ways for an inner scope to relate to inherited intent, each recorded explicitly on the inheriting artifact.
[Visible, attributable deviation](../requirements/system/visible-attributable-deviation.md){id=note:req:64eknb1} requires every replacement or removal to be visible at the deviating scope, to carry a rationale, and to be attributable.
[Effective-intent resolution](../requirements/system/effective-intent-resolution.md){id=note:req:5xnajsm} requires the effective intent at any scope to be deterministically computable, with comparable conflicts resolved by proximity and incomparable conflicts and removals surfaced.

Two prior decisions constrain the representation.
[Adopter corpus placement](corpus-placement.md){id=note:dec:q2v7nk3} settled that the authoritative scope lives in frontmatter, that directory containment may mirror at most the single structural parent as a convenience, and that cross-cutting and multi-parent edges are always carried by id in frontmatter; the directory tree is the spanning tree of the Scope DAG, never the whole DAG.
[Cascade conflict resolution](cascade-conflict-resolution.md){id=note:dec:9c4tk2n} settled the resolution behavior: proximity resolves comparable conflicts silently, genuine ties surface, any removal is always loud, and an author may declare a precedence once among otherwise-incomparable parents.

What is missing is the syntax: no scope field exists, the three operators have no authored form, the declared precedence has no shape, and the effective-intent walk has no representation a reader can perform.
[Context model](context-model.md){id=note:dec:b7w3k9n} settled that a Context narrows monotonically and that a widening is a loud deviation treated like a removal; the representation must let Context ride the same mechanism rather than introduce a second one.

The principles bind the shape of the answer.
Universal participation and file-native capture mean the walk must be performable by an unaided human reader from the files, with no step requiring a tool.
[Compute and Report](../principles/compute-and-report.md){id=note:principle:6e7f28k} means the representation represents and is checkable but enforces nothing: permission stays with the Orchestrating Authority.
[Proportionality](../principles/proportionality.md){id=note:principle:es0vhzn} means a single-scope corpus declares nothing.
[Single Source of Truth](../principles/single-source-of-truth.md){id=note:principle:8691937} means the scope and parent fact has one home in frontmatter, mirrored at most by the spanning tree.

## Decision

- **A scope is identified by a stable scope id, declared once at the scope root.**
  A scope is named by a `scope` block on the scope's manifest at the scope root, carrying a scope id and the scope's parent edges.
  The manifest, the corpus's configuration home, is the one host every scope shares: scope identity and parent edges are configuration, not intent, and a cross-cutting scope (a security or privacy domain) has no Context to carry the block, so the boundary statement cannot be the host.
  The scope id is the unit the cascade graph is built from; an artifact names the scope it belongs to rather than re-declaring the graph.
  A corpus that occupies a single scope declares no scope block at all: the absence of any declared parent is the default single-scope case, and it costs nothing.

- **Parent edges live in frontmatter, by id; containment mirrors at most one of them.**
  A scope declares its parents as a list of scope ids in the scope block.
  Where a scope has a single structural parent, directory containment may mirror that one edge as a reading convenience, but the frontmatter list is authoritative and a move never changes the graph.
  Cross-cutting and multi-parent edges are never expressed by location; they are always carried by id, consistent with [Adopter corpus placement](corpus-placement.md){id=note:dec:q2v7nk3}.
  The parent relation is acyclic: a scope may not reach itself by following parent edges, so resolution terminates.

- **An artifact records the scope it is load-bearing at.**
  An artifact carries an optional `scope` field naming the scope id at which its intent first applies; below that scope the intent is inherited.
  An artifact in a single-scope corpus omits the field and is load-bearing at the lone implicit scope.
  An artifact whose scope is unambiguous from the scope root it sits under may omit the field and take the enclosing scope; the field is authored explicitly only where an artifact is load-bearing at a scope other than the one its location implies, which keeps the common case free of ceremony.

- **Three authored deviation operators; the loud ones carry a rationale.**
  An inner scope relates to an inherited obligation through one of three operators, authored on the inheriting artifact in a `## Deviation` section, each naming the inherited source by id:
  - **add** (strengthen): the inherited obligation stays in force and the local one applies alongside it; both hold.
  - **replace**: the local obligation supersedes the inherited one at this scope and below; the inherited one no longer applies here.
  - **disinherit** (remove): the inherited obligation is dropped at this scope and below, with no replacement.
  A **replace** or a **disinherit** carries a rationale (the why), satisfying [Visible, attributable deviation](../requirements/system/visible-attributable-deviation.md){id=note:req:64eknb1}; an **add** is the safe, silent strengthening the cascade does not surface, so it records only the operator and the source and pays no rationale tax.
  No entry names its author: attribution is the artifact's own Git provenance (commit authorship and signature), the corpus's trust root, never a self-declared field, which any actor with file access could forge, consistent with [Compute and Report](../principles/compute-and-report.md){id=note:principle:6e7f28k}.

- **A declared precedence is a fourth, optional authored entry of the same family.**
  Where two parents are incomparable and their conflict recurs, an author may declare, once, that one parent precedes the other for a named point of intent, in a `precedence` entry of the scope block carrying its own rationale.
  A declared precedence is itself a visible, attributable deviation, auditable like any operator, and it converts a recurring surfaced tie into authored intent ([Cascade conflict resolution](cascade-conflict-resolution.md){id=note:dec:9c4tk2n}).

- **A Context is re-authored and compared, not deviated with operators.**
  A Context is a single holistic boundary statement, one per scope, not a set of discrete inherited obligations, so it carries no `## Deviation` operators.
  A subsystem re-authors its own Context, narrowed from the one it inherits, and the cascade detects the deviation by comparing the inherited effective boundary to the local one ([Context model](context-model.md){id=note:dec:b7w3k9n}).
  Narrowing (dropping an external entity, tightening what crosses) is the safe, silent strengthening; widening is the loud, surfaced deviation, the inverse of the obligation rule where a removal is loud, and it carries its rationale in the re-authored Context's body.
  The cascade behavior is shared with obligations, silent on a strengthening or a narrowing and loud on a removal or a widening; only the representation differs, authored operators for a discrete obligation and boundary comparison for a holistic Context.

- **The effective-intent walk is a derived view, never stored.**
  The effective intent at a scope is computed by walking the parent edges and applying the operators; it is never authored as a second artifact while the corpus is live, the one deliberate exception being materialization ([Effective-intent resolution](../requirements/system/effective-intent-resolution.md){id=note:req:5xnajsm}).
  The grammar and the deterministic procedure are fixed in the companion specification.

## Forces and trade-offs

- Putting the scope graph in frontmatter, with containment as a mere mirror, keeps location non-normative so a move never breaks resolution, at the cost that the directory tree shows only the spanning tree and the full DAG must be read from frontmatter or reconstructed by a tool.
  Accepted: location-independence is a settled commitment, and the spanning tree still gives a human a legible cascade for the common single-parent case.

- Making every replacement and removal carry a rationale costs the author a sentence on each loud opt-out.
  Accepted: a silently dropped cross-cutting obligation is the precise audit surprise the machinery exists to prevent, while an **add** pays nothing, so the silent strengthening stays silent and the cost falls only where intent is genuinely replaced or removed.

- Representing an obligation deviation with authored operators but a Context deviation by boundary comparison is two representations rather than one, at the cost that a reader learns both.
  Accepted under Earned Substance: an obligation is a discrete inherited item and a Context is a holistic boundary, genuinely different shapes, so one operator vocabulary forced over both would strain the Context; the cascade behavior, silent on a strengthening or a narrowing and loud on a removal or a widening, stays the one shared model.

- An optional `scope` field on artifacts, defaulting to the enclosing scope, keeps the single-scope and single-parent cases free of ceremony, at the cost that a reader cannot always tell an artifact's scope from the field alone and may need the enclosing scope root.
  Accepted under Proportionality: the field is earned only where an artifact's scope differs from its location, and the common case pays nothing.

## Alternatives considered

- **Express scope by directory location, normatively (path determines scope).**
  Rejected: it trades away location-independence, the same rejection [Adopter corpus placement](corpus-placement.md){id=note:dec:q2v7nk3} already made, and it cannot express a multi-parent or cross-cutting edge, which has no single location.

- **A single combined override operator instead of three.**
  Rejected: it collapses add, replace, and disinherit into one verb whose meaning depends on unstated intent, which is exactly the implied-rather-than-explicit deviation [Deviation operators on inherited intent](../requirements/system/deviation-from-inherited-intent.md){id=note:req:sd7ch4m} forbids; a checker could not tell a strengthening from a removal, and removal must be distinguishable to stay loud.

- **A standalone deviation artifact per opt-out, referencing the inheriting artifact.**
  Rejected against Earned Substance and visibility: a separate file makes the deviation invisible at the scope where it occurs, forcing a reviewer to find it, which is the opposite of the visibility [Visible, attributable deviation](../requirements/system/visible-attributable-deviation.md){id=note:req:64eknb1} requires; the deviation belongs on the inheriting artifact.

- **Force the three obligation operators onto a Context (an add, replace, or disinherit per external entity).**
  Rejected: a Context is a holistic boundary, not a set of discrete inherited items, so per-entity operators strain it, and the operator-to-loudness mapping inverts confusingly, the `disinherit` that is loud for an obligation being the silent narrowing for a Context. Re-authoring the boundary and detecting narrowing from widening by comparison fits the holistic shape and keeps one shared cascade behavior without a second operator vocabulary, while still honoring that Context shares the cascade mechanism ([Context model](context-model.md){id=note:dec:b7w3k9n}).

- **Store the resolved effective intent as its own artifact for fast reads.**
  Rejected: a stored result is a second source that drifts; the walk is cheap enough to recompute, and the one deliberate freeze is materialization, which severs the link and records provenance ([Effective-intent resolution](../requirements/system/effective-intent-resolution.md){id=note:req:5xnajsm}).

- **A total order over parents (nearest wins, ties broken by declaration order), as CSS does.**
  Rejected: it silently resolves a genuine equal-distance conflict by an arbitrary rule, the silent wrong-pick [Cascade conflict resolution](cascade-conflict-resolution.md){id=note:dec:9c4tk2n} already rejected; proximity stays a partial order and genuine ties surface.

- **Host the scope block on the Context (`context.md`) rather than the manifest.**
  Rejected: a cross-cutting scope has no Context by the [Context model](context-model.md){id=note:dec:b7w3k9n}, yet cross-cutting scopes are the multi-parent sources the cascade most needs to declare; only the manifest, present at every scope root, hosts them all. Scope identity and parents are configuration, not intent, so the manifest, not the boundary statement, is their home.

- **Record the deviating author in a frontmatter or entry field.**
  Rejected: any actor with file access could write a false author, so a self-declared attribution is advisory dressed as structural, the failure [Compute and Report](../principles/compute-and-report.md){id=note:principle:6e7f28k} rejects, and it duplicates the authoritative Git record it would drift from. Attribution rests on Git provenance, the corpus's trust root.

- **Require a rationale on every operator, including `add`.**
  Rejected: strengthening is the silent, auto-resolved case ([Cascade conflict resolution](cascade-conflict-resolution.md){id=note:dec:9c4tk2n}), and [Visible, attributable deviation](../requirements/system/visible-attributable-deviation.md){id=note:req:64eknb1} obliges a rationale only for a replacement or a removal; taxing `add` with a rationale it does not need is ceremony against Proportionality.

## Driven by

- groundedIn: [Scope and inheritance](../requirements/system/scope-and-inheritance.md){id=note:req:96smmcv}
- groundedIn: [Deviation operators on inherited intent](../requirements/system/deviation-from-inherited-intent.md){id=note:req:sd7ch4m}
- groundedIn: [Visible, attributable deviation](../requirements/system/visible-attributable-deviation.md){id=note:req:64eknb1}
- groundedIn: [Effective-intent resolution](../requirements/system/effective-intent-resolution.md){id=note:req:5xnajsm}
- groundedIn: [Adopter corpus placement](corpus-placement.md){id=note:dec:q2v7nk3}
- groundedIn: [The corpus manifest](corpus-manifest.md){id=note:dec:mf3k9w2}
- groundedIn: [Cascade conflict resolution](cascade-conflict-resolution.md){id=note:dec:9c4tk2n}
- groundedIn: [Context model](context-model.md){id=note:dec:b7w3k9n}

## Worked example

A division scope `acme-payments` inherits from the organization scope `acme` and a cross-cutting `acme-privacy` scope.
Its scope block, at the scope root, declares the graph:

```yaml
scope:
  id: acme-payments
  parents: [acme, acme-privacy]
```

A service scope `acme-checkout` under `acme-payments` sits in a directory contained by it, so it mirrors that one structural parent by location and need only name its cross-cutting parent by id:

```yaml
scope:
  id: acme-checkout
  parents: [acme-payments, acme-privacy]
```

A retention requirement at `acme-checkout` disinherits an inherited Security obligation it cannot meet:

```markdown
## Deviation

- disinherit [Service-to-service mTLS](.../mtls.md){id=note:req:...} from acme-security.
  Rationale: a legacy dependency cannot perform mTLS; compensating controls are recorded in ...
```

A reader resolving the effective intent at `acme-checkout` walks the parent edges, applies each operator, and stops because the parent graph is acyclic.
The disinherit surfaces as loud regardless of proximity; nothing in the files enforces the opt-out, which the Orchestrating Authority routes to the Security scope's owner.
