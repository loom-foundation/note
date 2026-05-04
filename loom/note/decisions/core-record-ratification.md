---
id: note:dec:rt7sw3k
name: Core record ratification
kind: decision
status: current
decided: 2026-07-02T00:00:00Z
---

The corpus ratifies its record in full: every term, the system context, every requirement, every verification, the validation-evidence convention, and the value layer's offerings and facets move to current, so everything the corpus relies on reads as the operative source it is.
Claim confidence stays honest through the validation tiers rather than through draft statuses, and the verification gaps the strict profile surfaces over the current requirements are the corpus's own open work queue, reported and worked through rather than hidden by status.

## Context

The corpus's maturity ladder had inverted: every specification and decision was current while 80 of 81 terms, 61 of 67 requirements, the system context, one convention, both verifications, and the whole value layer were draft.
Draft means content a reader cites with caution, yet the reference closure structurally pulls the terms in force into every slice, and the current specifications were ratified against those very terms and requirements.
Left as it was, the posture read as either dishonest statuses or an unfinished core, and it suppressed the strict profile's verification findings by keeping requirements below the status the findings key on.

The value layer posed the one genuine question: its pitches are graded `validation: assumed`, so a draft status looked like a second honesty signal.
With the validation field declared ([The validation field](validation-field.md){id=note:dec:vf2m8qe}), that duplication resolves: the tier carries how tested a claim is, and status returns to its one job, how settled the artifact's content is.
An offering whose prose is settled and whose claim is untested is exactly `status: current` with `validation: assumed`.

## Decision

- **The vocabulary is ratified.**
  Every term moves to current; the stale pre-split instantiation examples on the Namespace, Component, and Subsystem terms were corrected before ratification, so nothing false was confirmed operative.

- **The context is ratified.**
  The system boundary is relied on throughout the corpus and now reads current, under its canonical section headings.

- **The requirements are ratified.**
  Every requirement's obligation is settled through ratified decisions, so all move to current; four leads were brought to the shall-form the strict profile expects before the flip.

- **The verifications are ratified.**
  The identity-and-reference-integrity and specification-authority checks move to current, joined by two new checks over the drift family, so every requirement that was already current now carries at least one verification.

- **The evidence convention is ratified.**
  [Validation evidence in the Source](../conventions/validation-evidence-in-source.md){id=note:conv:8wafpx1} becomes operative alongside the declared validation field.

- **The value layer is ratified, with its claims graded rather than overstated.**
  The offerings, their relievers and creators, and the remaining draft pains move to current: their prose is the settled statement of the value and the problems it answers.
  How far each claim has been tested stays on the record where it belongs, in the `validation` tier the pitches carry, not in a draft status doing a second job.

- **Verification gaps are surfaced, never suppressed.**
  At strict, a current requirement without a verification is a reported finding; the newly current requirements make that queue honest and visible, and the owner works through it rather than clearing it by demoting statuses.

## Forces and trade-offs

Ratifying the requirement set ahead of full verification coverage makes the strict report longer, not shorter: the corpus chooses visible debt over a green dashboard.
That is the method's own coverage philosophy applied to itself, gaps surfaced and decidable, and the alternative, keeping settled obligations draft so the findings stay quiet, misuses the maturity ladder as a suppression switch.

Ratifying the value layer trades the caution a draft status broadcast for a single, sharper signal: a reader who wants to know whether a pitch is proven reads its validation tier, and a reader who wants to know whether the artifact is settled reads its status.
Two axes, each doing one job, is the model the corpus already fixes; the draft statuses were the residue of the time before the field was declared.

A sweep this size rests on the review that ratifies it: the statuses flip in attributable changes, and any artifact wrongly confirmed is corrected by an ordinary follow-up rather than a lifecycle rollback.

## Alternatives considered

- **Drop the manifest to `standard` until verifications catch up.**
  Rejected: the corpus dogfoods the method at its most demanding configuration, and the strict findings are the point, not a blemish; hiding them would trade honesty for appearance.

- **Ratify only the requirements that already carry verifications.**
  Rejected: it gates an obligation's settledness on verification supply, misreading the ladder; a requirement is current when its content is confirmed operative, and the missing check is exactly what the strict report exists to say.

- **Leave the terms draft as a standing caution.**
  Rejected: the closure pulls the vocabulary into every slice, so a draft vocabulary tells every reader and agent to hesitate over words the specifications already rely on.

- **Leave the value layer draft while its claims await validation evidence.**
  Rejected by the owner, on the grounds the validation field makes sound: the tier already grades the claim, a draft status restated that grade in a weaker form, and caution about untested claims belongs on the validation axis, not the maturity axis.

## Driven by

- groundedIn: [Know an artifact's maturity before relying on it](../needs/know-artifact-maturity.md){id=note:need:6pxykex}
- groundedIn: [Legible lifecycle](../requirements/system/legible-lifecycle.md){id=note:req:233g9mc}
- groundedIn: [See and decide on coverage gaps](../needs/see-and-decide-on-coverage-gaps.md){id=note:need:7kp2v9d}
- groundedIn: [The validation field](validation-field.md){id=note:dec:vf2m8qe}
- groundedIn: [Compute and Report](../principles/compute-and-report.md){id=note:principle:6e7f28k}
