---
id: note:req:46xm59a
name: Detectable staleness
kind: requirement
level: system
type: functional
status: current
---

Note shall ensure it is detectable, from the files, that the text of a referenced artifact has changed since a dependent relied on it, so the dependents pointing at it can be surfaced for re-check.

## Rationale

Staleness is about referenced text moving, not about behavior being wrong (see the Drift group under `terms/`).

Surfacing it lets a reader catch divergence by inspection rather than in an incident.

The mechanism is fixed in [Detect staleness from git provenance, not a stored digest](../../decisions/detect-staleness-from-git-not-a-stored-digest.md){id=note:dec:dvk7m2x}: detection is computed from git provenance against the citation graph (full where history is present, "can't tell" and never a false all-clear in history-stripped environments), with the cross-corpus computation deferred to the supporting tool.

## Relations

- derivedFrom: [Detectable drift](../stakeholder/detectable-drift.md){id=note:req:d6m4q7z}
- delivers: [Grounded in Stated Intent](../../offerings/right-sized-context/pr-grounded-in-stated-intent.md){id=note:pr:qj473b0}
- delivers: [Drift Surfaced Early](../../offerings/trust-by-inspection/pr-drift-surfaced-early.md){id=note:pr:cvarqvw}
