---
id: note:req:s9xq4r2
name: Detectable lifecycle staleness
kind: requirement
level: system
type: functional
status: current
---

Note shall ensure it is detectable, from the files, that a citation resolves to an artifact whose lifecycle state is no longer `current`, so the citations relying on a superseded, rejected, or obsolete artifact can be surfaced for re-check, as a signal distinct from a referenced text moving.

## Rationale

A citation can resolve cleanly and still mislead: the artifact it names may have been superseded, rejected, or retired, so the reliance points at an obligation the corpus no longer holds ([Legible lifecycle](legible-lifecycle.md){id=note:req:233g9mc} fixes the state set this keys on).

Text-staleness does not catch this: the referenced text need not have moved at all for the artifact to have left `current`, and an artifact may be marked obsolete without its body changing ([Detectable staleness](detectable-staleness.md){id=note:req:46xm59a}).

The two signals are therefore distinct and both belong under the obligation that drift surface by inspection: text-staleness reports that what a dependent relied on has changed, lifecycle-staleness reports that what it relied on is no longer authoritative.

This requirement states the property, that a citation onto a non-`current` artifact be detectable and surfaced, and leaves how the state is read and the signal raised to specification.

Whether such a check runs, and by whom, belongs to the Orchestrating Authority; Note represents the citation and the lifecycle state and computes over them, and reaches no further.

## Relations

- derivedFrom: [Detectable drift](../stakeholder/detectable-drift.md){id=note:req:d6m4q7z}
