---
id: note:dec:0n14gqx
name: The multi-root corpus
kind: decision
status: current
decided: 2026-06-28T00:00:00Z
---

One corpus may span several repositories under a single namespace: a root manifest declares the member roots, each member carries the shared namespace, and the assembled members are one corpus with one trace graph, one coverage closure, and one identity space.
A namespace is declared once in the manifest and is the identity-space boundary; an opaque is unique within a namespace, so repositories that share a namespace share one id space and repositories that choose distinct namespaces never collide.
References between members are ordinary in-corpus references; a reference to another system, under another namespace, is a cross-repository reference, not a membership.

## Context

A system is often built as several repositories, for ownership, team-boundary, or release-cadence reasons, yet its intent is one connected body ([Operate one corpus across many repositories](../needs/operate-corpus-across-repositories.md){id=note:need:03gs33j}).
The method already resolves references and inheritance across repository boundaries ([Cross-repository inheritance and materialization](cross-repository-inheritance.md){id=note:dec:h4w9k2t}) and already treats a layer root as wherever a manifest sits ([Adopter corpus placement](corpus-placement.md){id=note:dec:q2v7nk3}).
What it lacks is a way to say that several repositories are *one* corpus rather than several that merely reference each other.

Two gaps make that need bite.
A repository does not declare which namespace it mints into, so a tool or an agent cannot tell the identity-space boundary or check that the repository mints only within it ([Undeclared Identity-Space Boundary](../needs/operate-corpus-across-repositories/pain-undeclared-id-space.md){id=note:pain:86y9pke}).
And when sub-systems share one namespace across repositories, parallel offline minting can draw the same identifier, a collision that surfaces only at assembly ([Shared Namespace Collides Under Parallel Minting](../needs/operate-corpus-across-repositories/pain-shared-namespace-collision.md){id=note:pain:ntyth85}).
A deliberation against this design, with a systems engineer and an adversary, settled its shape: model the shared identity as one corpus, not as separate corpora sharing a prefix, and keep uniqueness probabilistic rather than coordinated.

## Decision

- **A namespace is declared in the manifest.**
  A corpus declares its `namespace` once, in its manifest, realizing what the Namespace term already asks for ([Namespace](../terms/identity-and-references/namespace.md){id=note:term:x494sn0}).
  The declaration is the identity-space boundary a tool reads to know which namespace the repository mints into; a checker asserts every artifact's id carries it.

- **An opaque is unique within its namespace, not within one repository.**
  Uniqueness is scoped to the namespace, so one namespace may span repositories without an id meaning two things, and distinct namespaces partition the id space so independent corpora never collide.
  Within a namespace, uniqueness is probabilistic, not coordinated: the opaque is drawn from a cryptographically secure source at a length the manifest sets for the whole namespace, so parallel offline minting across members stays collision-free with no shared registry; the per-repository collision check is a local backstop, and a workspace-assembly check reports the rare collision rather than preventing it.

- **A corpus may span repositories as member roots.**
  A corpus's root manifest may declare `roots`, the member repositories that compose it; each member carries its own manifest declaring the same namespace.
  The members are located by relative path in a co-located workspace, or by URL when they are not, the same way a cross-repository reference resolves; the assembled corpus is the union of the root and its members, sharing one namespace, one trace graph, and one coverage closure.

- **Same system, same namespace; different system, different namespace.**
  Members of one corpus reference each other as ordinary in-corpus references, under the one namespace.
  A reference to another system, under another namespace, is a cross-repository reference or an inheritance, not a membership, and its reproducibility is pinned as that decision fixes ([Cross-repository inheritance and materialization](cross-repository-inheritance.md){id=note:dec:h4w9k2t}).

- **Placement rides where the workspace is anchored.**
  The root manifest sits where the workspace is already anchored: in the manifest or spine repository a workspace tool uses, or, pulling repositories by hand, in the parent directory that holds the siblings; a `loom.md` may point discovery at it, extending the placement algorithm ([Adopter corpus placement](corpus-placement.md){id=note:dec:q2v7nk3}).

- **Represented and checked, never coordinated at the mint.**
  The method declares the namespace, sizes the opaque, and reports collisions and unresolved members at assembly; it runs no central mint and no lock.
  Keeping uniqueness probabilistic and assembly-checked rather than coordinated is what lets a contributor or an agent mint offline in one member with no online service ([Compute and Report](../principles/compute-and-report.md){id=note:principle:6e7f28k}).

## Forces and trade-offs

Spanning a corpus across repositories adds a root manifest and a per-member namespace declaration, against Earned Substance.
It is accepted because the alternative, separate corpora sharing a namespace prefix by convention, has no declared boundary and no single place to size the opaque for the whole, so its uniqueness rests on each repository guessing a length in isolation, the shortest of which sets the real safety.
Binding the members into one declared corpus gives the namespace one home for its length and its membership, and makes the shared id space a checkable fact rather than a hopeful convention.

Probabilistic uniqueness, sized once for the namespace, is weighed against a coordinated mint.
A coordinated mint (a shared registry or a lock) removes the residual birthday risk but requires every member to reach a service to mint, breaking offline, files-alone authoring.
The residual risk is made small by sizing the opaque to the namespace's scale, and is caught, not prevented, by the assembly check: the method reports the collision, the authority resolves it.

Whole-graph properties across members, acyclicity, coverage, and the inbound view a member cannot see alone, are computed only when the workspace is assembled.
A member read in isolation has durable ids and its own local checks, but the cross-member view is an assembly-time computation, not a files-alone one; this is named rather than hidden.

## Alternatives considered

- **Separate corpora that share a namespace prefix by convention.**
  Rejected: nothing declares the shared boundary, no single place sizes the opaque for the whole, and offline minting safety becomes the shortest length any participating repository happened to choose; the shared id space is a hope, not a checkable fact.

- **Mandate one namespace per repository, distinct everywhere.**
  Rejected: it forbids the common, legitimate case of sub-systems of one system sharing one identity space, and forces a system's intent to read as many corpora that merely cross-reference; distinct namespaces stay available and are right for genuinely independent corpora, but they are not the only choice.

- **A coordinated mint, a central registry or lock, for a shared namespace.**
  Rejected: it removes the residual collision risk at the cost of an online service at mint time, breaking the offline, files-alone authoring the method requires; probabilistic uniqueness sized for the namespace, with an assembly-time check, keeps minting local.

- **Treat each repository's contribution as inheritance rather than membership.**
  Rejected: inheritance pins a version and freezes or severs the link, which is right for depending on another system's intent but wrong for the parts of one system, which co-evolve and must read as one live body, not as pinned snapshots of each other.

## Driven by

- groundedIn: [Operate one corpus across many repositories](../needs/operate-corpus-across-repositories.md){id=note:need:03gs33j}
- groundedIn: [Cross-repository inheritance and materialization](cross-repository-inheritance.md){id=note:dec:h4w9k2t}
- groundedIn: [Adopter corpus placement](corpus-placement.md){id=note:dec:q2v7nk3}
- groundedIn: [Single Source of Truth](../principles/single-source-of-truth.md){id=note:principle:8691937}
- groundedIn: [Earned Substance](../principles/earned-substance.md){id=note:principle:yecemfe}
- groundedIn: [Proportionality](../principles/proportionality.md){id=note:principle:es0vhzn}
- groundedIn: [Compute and Report](../principles/compute-and-report.md){id=note:principle:6e7f28k}

## Worked example

A system kept as three sibling repositories, assembled in one workspace:

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

A requirement in `billing/` refers to one in `gateway/` as an ordinary in-corpus reference, resolved on disk in the workspace with no tool:

```
- derivedFrom: [Auth](../../gateway/note/requirements/system/auth.md){id=acme:req:7k2m9q0}
```

An engineer or an agent in `billing/` mints `acme:` ids at the declared length and commits offline; the ids are unique across the members by construction, and a workspace-assembly check confirms it and reports any unresolved member.
A second system, `vendor`, is a different namespace: `billing/` refers to it as a cross-repository reference, pinned per the cross-repository decision, not as a member root.
