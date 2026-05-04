---
id: note:ver:dg5xq2m
name: Drift signals are detectable from the files
kind: verification
status: current
method: analysis
---

This verification confirms that the drift signals the method promises are computable from a committed corpus: text-staleness (a referenced artifact's text moved since a dependent relied on it), lifecycle-staleness (a citation resolves to an artifact that is no longer `current`), and the structural suspect-citation signals, each surfaced for re-check and never reported as a false all-clear.
The check computes and reports findings only; the verdict on any surfaced item belongs to the Orchestrating Authority.

## Criteria

A pass requires, across every citation in the corpus, that:

- text-staleness is computable where history is present: comparing when the target's content last changed against when the citing relationship was established classifies the citation fresh or stale, per the git-provenance mechanism ([Detect staleness from git provenance, not a stored digest](../decisions/detect-staleness-from-git-not-a-stored-digest.md){id=note:dec:dvk7m2x});
- the signal is three-valued and never false-clears: where the reference point cannot be established (a shallow clone, a squashed history, a plain-file export), the output is can't-tell, never a silent fresh;
- lifecycle-staleness is computable from the files alone: every citation whose target's `status` is not `current` is surfaced, as a signal distinct from text-staleness;
- the structural suspect-citation signals are computable from the citation graph alone and surfaced for review, asserting nothing about whether the citing unit honors the cited intent.

A pass is each signal computable as specified, with no path that returns a silent all-clear where its reference point is unavailable.

## Procedure

By analysis.
A static reader parses every artifact's frontmatter and citations, joins each citation to its target's `status` for the lifecycle signal, and computes the structural suspect signals from the citation graph.
Where git history is present, it reads, for each citation, the commit that established the citing relationship and the target's last content-changing commit, and classifies the pair fresh or stale; where history is absent or stripped, it emits can't-tell for exactly those citations.
The reader only reads; it executes nothing and writes nothing, so the check is reproducible by anyone with the repository.

## Evidence

A run produces a report per signal: the citations checked, each classification (fresh, stale, can't-tell, or surfaced), and the findings raised.
The report is kept with the run by the Orchestrating Authority; it is not stored in this artifact.

## Relations

- verifies: [Detectable drift](../requirements/stakeholder/detectable-drift.md){id=note:req:d6m4q7z}
- verifies: [Detectable staleness](../requirements/system/detectable-staleness.md){id=note:req:46xm59a}
- verifies: [Detectable lifecycle staleness](../requirements/system/detectable-lifecycle-staleness.md){id=note:req:s9xq4r2}
- verifies: [Surfaceable suspect-citation signals](../requirements/system/surfaceable-suspect-citation.md){id=note:req:v3k7m1n}
