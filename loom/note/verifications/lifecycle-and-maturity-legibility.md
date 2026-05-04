---
id: note:ver:m4t9xzc
name: Lifecycle and maturity legibility
kind: verification
status: current
method: analysis
---

This verification confirms that maturity and confidence are legible from every artifact without reading its body: the `status` field carries the universal lifecycle, status changes stay within the well-formed transition set, recovered or untested claims are distinguishable through their `validation` tier, and a change of intent carries its rationale in the record.
The check is a static pass over the files, with transitions read from history where history is present; it computes and reports findings only, and the verdict belongs to the Orchestrating Authority.

## Criteria

A pass requires that:

- every artifact carries a `status` from the universal set, so a reader triages placeholder, in-progress, settled, and retired without opening a body;
- between any two revisions where history is present, each status change is a well-formed transition (`tbd` to `draft` or `current`, `draft` to `current` or `rejected`, `current` to `obsolete`), with no backward motion and no reinstated terminal artifact;
- a decision at `current` or `obsolete` carries its `decided` timestamp, so ratification is dated on the record;
- every `validation` field carries a tier from the closed set, so a recovered or untested claim is marked at honest confidence rather than dressed as confirmed, and a corpus may be valid while partial;
- every current decision carries its `## Context`, `## Forces and trade-offs`, and `## Alternatives considered`, so why intent changed is recoverable beside what changed.

A pass is zero failures across the corpus; where history is absent, the transition check honestly reports can't-tell rather than a silent pass.

## Procedure

By analysis.
A static reader collects every artifact's `status`, `decided`, and `validation` fields and validates them against the universal set, the decided-gating rule, and the closed tier set; it validates the decision kind's required sections corpus-wide.
Where git history is present, it diffs each artifact's frontmatter across revisions and classifies every status change against the transition table; where history is stripped, it emits can't-tell for the transition criterion.
The reader only reads; it executes nothing, so the check is reproducible by anyone with the repository.

## Evidence

A run produces a report: the status census, any transition, gating, tier, or section failure, and the can't-tell set where history was unavailable.
The report is kept with the run by the Orchestrating Authority; it is not stored in this artifact.

## Relations

- verifies: [Legible lifecycle](../requirements/system/legible-lifecycle.md){id=note:req:233g9mc}
- verifies: [Legible artifact maturity](../requirements/stakeholder/legible-maturity.md){id=note:req:b3h47g8}
- verifies: [Incremental capture of recovered intent](../requirements/system/incremental-intent-capture.md){id=note:req:m2x8k5p}
- verifies: [Incremental adoption of an existing system](../requirements/stakeholder/incremental-adoption.md){id=note:req:h7n4k2w}
- verifies: [Evolving intent with rationale](../requirements/stakeholder/evolving-intent-rationale.md){id=note:req:6swdxb0}
