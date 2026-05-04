---
id: note:dec:h4w9k2t
name: Cross-repository inheritance and materialization
kind: decision
status: current
decided: 2026-06-10T05:50:48Z
---

A corpus may inherit intent maintained in another repository, referencing it by durable id and resolving it across the repository boundary at an explicitly pinned version, so the inheritance is reproducible.

A corpus may instead materialize an upstream: freeze a local copy at a chosen version, sever the live link, and depend on no external repository thereafter.

Materialized copies live under `materialized/<namespace>/<version>/` at the layer root, each carrying its own provenance, which is the single record of the capture.

Inheriting and materializing are per upstream: a corpus can keep some sources live and freeze others.

## Context

Note already lets a relation reference an artifact in another repository by stable id and resolve scope inheritance across repository boundaries ([Cross-repository resolution](../requirements/system/cross-repository-resolution.md){id=note:req:dxxvabc}), and lets a scope capture inherited intent locally with provenance, severing the live link ([Materialization of inherited intent](../requirements/system/materialization-of-inherited-intent.md){id=note:req:dssf1pp}; [Self-contained extraction of inherited intent](../requirements/stakeholder/self-contained-extraction.md){id=note:req:qq6eywy}).

What was unsettled was the operational shape: the version at which a live reference resolves, where frozen copies sit on disk, how their provenance is recorded, and whether a central index of frozen sources is kept.

These converged through worked scenarios (a note repository and a sett repository under one foundation; an incubator spinning out an entity).

## Decision

- **Live inheritance is referenced by id and pinned to a version.**
  A corpus that inherits from another repository references the upstream artifacts by durable id, so the link stays live and the upstream is not copied, and it resolves them at an explicitly identified upstream version, so the inheritance is reproducible and does not shift unless the version is deliberately changed.
  The upstream repository is located by a remote URL or a local filesystem path, so two repositories cloned side by side can inherit from each other with no online service.
  How the version is declared and recorded is the tool's configuration concern, settled on the tool side by Sett's own configuration decision.
- **Materialization freezes a copy and severs the link.**
  A corpus may capture an inherited upstream as local standalone artifacts at a chosen version and stop depending on the upstream repository ([Materialization of inherited intent](../requirements/system/materialization-of-inherited-intent.md){id=note:req:dssf1pp}).
  This is per upstream: a corpus can keep some sources live and materialize others.
- **Materialized copies live under a dedicated, named location.**
  Frozen copies sit at `materialized/<namespace>/<version>/` at the layer root: inside the corpus, because they are part of the now self-contained corpus, but clearly separated from authored intent.
  The name is `materialized` so that "inherited" stays reserved for intent still live-linked to its upstream; conflating the two would mislead.
  The per-upstream subdirectory nests `<namespace>/<version>/` rather than encoding the version in the directory name, so a namespace containing hyphens needs no escaping and no separator character is required.
- **Per-artifact provenance is the single record.**
  Each materialized artifact carries, in its own frontmatter, a `materialized` block recording the source repository, the version, the resolved commit, and the date it was captured; its `status` still records lifecycle, so a frozen copy still honored is `current` and a retired one is `obsolete`, and the block's presence rather than the status marks it as materialized.
  This provenance travels with the file and is the authoritative record of the capture.
  No separate index of materialized sources is kept: a central ledger would duplicate the per-artifact provenance and risk drifting from it.
  On materialization, the upstream simply stops being listed as a live inherited source.
- **A frozen mirror keeps its id; an adopted copy is re-homed.**
  A faithful frozen mirror keeps the upstream's durable id, so existing references resolve unchanged and the content stays identical to the upstream at that version.
  If a corpus instead takes ownership to evolve a copy, it re-homes the artifact to its own namespace, with the provenance recorded as lineage; that is a deliberate fork, not a mirror.
- **Generated path segments are portable.**
  Because namespaces and versions become directory names, Sett lowercases them and rejects reserved device names when generating materialized paths, so a corpus authored on one operating system resolves identically on Linux, macOS, and Windows.
  The portability of human-authored filenames is a separate, advisory convention that Sett reports on rather than enforces, consistent with the Compute and Report principle ([Compute and Report](../principles/compute-and-report.md){id=note:principle:6e7f28k}).
  The portability obligations themselves live on the tool side, as Sett's own portable-generated-paths and reported-path-hazards requirements.

## Worked example

A corpus that keeps one upstream live (`acme-shared`) and has materialized another (`note`):

```
my-app/
├── .sett/
│   ├── config.toml             # lists acme-shared as live; note is no longer listed
│   └── lock
└── loom/note/
    ├── requirements/
    │   └── my-thing.md      # derivedFrom acme-shared:req:... (live) + note:req:k7w2n9p (frozen)
    └── materialized/
        └── note/
            └── v0.4.0/
                └── requirements/
                    └── data-retention.md
```

The frozen artifact is self-describing; its provenance is the only record of the capture (the id below is illustrative):

```markdown
---
id: note:req:k7w2n9p
status: current
materialized:
  from: git+https://github.com/loom-foundation/note.git
  at: v0.4.0
  commit: 9f2c1ab
  on: 2026-06-02
---
```

## Forces and trade-offs

- Pinning a version makes inheritance reproducible at the cost that picking up upstream fixes is a deliberate bump rather than automatic.
  Accepted: a corpus that silently shifts under its owner is worse than one that updates on purpose, and the bump is exactly where change review belongs.
- Per-artifact provenance with no central ledger keeps a single source of truth and cannot drift, at the cost that auditing "everything this corpus froze" means scanning the `materialized/` tree rather than reading one list.
  Accepted: the tree and the frontmatter are that audit, and a ledger that restates them is the drift risk the methodology exists to avoid.
- Placing frozen copies inside the layer root makes them part of the self-contained corpus, at the cost of mixing authored and inherited material under one root.
  Mitigated by the dedicated `materialized/` subtree, which marks them as not hand-authored.

## Alternatives considered

- **Name the directory `inherited/`.**
  Rejected: "inherited" reads as intent still live-linked to its upstream, so using it for frozen copies misleads.
  `materialized` names the state.
- **Name the directory `vendor/`.**
  Rejected: `vendor/` connotes third-party code dependencies; the corpus inherits intent, not libraries, so the term is off-domain.
- **Encode the version as `namespace@version` in one directory name.**
  Rejected: `@` carries URL and git-revision friction, and a single-name encoding forces escaping when a namespace contains hyphens.
  Nested `namespace/version/` lets the path separator do the work with no escaping.
- **Keep a central index of materialized sources in configuration.**
  Rejected: it duplicates the per-artifact provenance and can drift from it.
  The artifacts are the record.
- **Resolve cross-repository references at a floating reference by default.**
  Rejected: a floating reference is not reproducible; the inheritance would shift without a deliberate change.

## Driven by

- groundedIn: [Cross-repository resolution](../requirements/system/cross-repository-resolution.md){id=note:req:dxxvabc}
- groundedIn: [Materialization of inherited intent](../requirements/system/materialization-of-inherited-intent.md){id=note:req:dssf1pp}
- groundedIn: [Self-contained extraction of inherited intent](../requirements/stakeholder/self-contained-extraction.md){id=note:req:qq6eywy}
- groundedIn: [Scope and inheritance](../requirements/system/scope-and-inheritance.md){id=note:req:96smmcv}
- groundedIn: [Requirement levels](requirement-levels-and-identity.md){id=note:dec:nc2yrf4}
- groundedIn: [Adopter corpus placement](corpus-placement.md){id=note:dec:q2v7nk3}
