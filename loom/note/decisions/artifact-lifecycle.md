---
id: note:dec:gfwq0mv
name: Universal artifact lifecycle and its transitions
kind: decision
status: current
decided: 2026-06-12T00:00:00Z
---

Every artifact's `status` moves through one universal set of well-formed transitions, the same for every kind: a maturity ladder of `tbd`, `draft`, and `current`, then one of two terminal states, `obsolete` for content that was operative and is retired, and `rejected` for an authored proposal that was deliberately declined and kept as a record.
Motion is monotonic toward the settled state and then terminal; a terminal artifact is placed under the layer-root archive tree, with status authoritative and placement the derived mirror.

## Context

Status records an artifact's lifecycle state, and a reader's trust in an artifact depends on which state changes are meaningful at all ([Legible lifecycle](../requirements/system/legible-lifecycle.md){id=note:req:233g9mc}).
A bare maturity ladder of `tbd`, `draft`, and `current` answers the question of how settled an artifact is, but it has a gap on the terminal end.

`obsolete` is the terminal state of content that was operative and is now retired.
It does not fit an authored proposal that was weighed and declined before it ever became operative: such a proposal was never `current`, so it cannot be `obsolete`, yet the conclusion to decline is often worth keeping as a record rather than erasing from the live corpus.
Validation already names the analogous case for claims: an off-ladder terminal tier for a claim that testing disproved, kept as a record rather than deleted.
The lifecycle ladder needs its analogue, and `rejected` is it.

A terminal artifact also needs a home that keeps it out of the live reader's path without erasing it.
Status alone tells a reader an artifact is retired or declined, but a corpus that leaves terminal artifacts interleaved with current ones makes the live set harder to read.
The archive convention answers this by placing terminal artifacts under a single visible archive tree, leaving status the authority and placement its mirror.

## Decision

- **One universal transition table.** The well-formed transitions of `status` are the same for every kind:

  | From | To | Well-formed | Meaning |
  |---|---|---|---|
  | `tbd` | `draft` | yes | A scaffolded placeholder gains authored substance. |
  | `tbd` | `current` | yes | Authored and confirmed operative in one act, never held as a separate draft. |
  | `draft` | `current` | yes | The content is confirmed as the operative source; for a decision this is ratification, and it sets `decided`. |
  | `draft` | `rejected` | yes | An authored proposal is deliberately declined and kept as a record. |
  | `current` | `obsolete` | yes | The content is retired; it was operative and is kept only for history. |

- **Two terminal states.** `obsolete` follows `current` (was operative, now retired); `rejected` follows `draft` (an authored proposal, declined).
  `rejected` is the lifecycle analogue of Validation's off-ladder disproved tier: kept as a record rather than deleted.
  The transitions `tbd -> obsolete`, `draft -> obsolete`, `tbd -> rejected`, and `current -> rejected` are ill-formed.

- **Motion is monotonic, never backward.** A `current` artifact is not returned to `draft` or `tbd`, and a terminal artifact is not reinstated in place.
  Reopening a settled question is a new artifact that may supersede the old one (`supersedes` on the successor, `superseded_by` on the retired artifact), never a rewrite of the original's lifecycle.

- **Deletion is not a transition.** An unauthored `tbd` placeholder, or a `draft` proposal abandoned with no conclusion reached, may be deleted (the file removed).
  The discriminator between deleting a draft and marking it `rejected` is whether a deliberate conclusion to decline was reached and is worth keeping as a record: if so, `rejected`; if merely abandoned, delete.

- **A terminal artifact is placed under the layer-root archive.** A terminal artifact, `obsolete` or `rejected`, is placed under the layer root's visible `archive/` tree, mirroring the kind tree, per the archive convention ([Archive and retention](archive-and-retention.md){id=note:dec:gh7mhc4}).
  Status stays authoritative: it is the field that records the artifact is terminal, and the placement is the derived mirror a checker keeps in sync, never the authority.

- **Optional `obsoleted` field.** An ISO date recording when an artifact was retired earns its place at `status: obsolete`, especially where no `superseded_by` is present; a superseding successor's `decided` already times the retirement.

- **Note defines well-formed transitions, not who may perform them.** Who may move an artifact between states belongs to the Orchestrating Authority, and who performed a transition is carried by Git history and signatures, not a frontmatter field ([System context](../context.md){id=note:ctx:rzbtzq9}).

## Forces and trade-offs

A fifth status value, a new optional field, and a derived placement widen the schema surface.
The cost is low and bounded: `rejected` is a value an existing field already ranges over, the `obsoleted` field is optional, the archive placement is computed from status rather than authored, and a small corpus that never retires or declines anything pays nothing.

Keeping `rejected` as an explicit terminal state, rather than deleting a declined proposal, leaves an artifact in the tree that a reader must recognize as off the ladder.
That is the same cost `obsolete` already carries, and the benefit is the same: the corpus remembers what was proposed and turned down, discoverable by inspection rather than by archaeology in Git history.
Placing the terminal artifact under the archive tree keeps that record discoverable without leaving it in the live reader's path.

## Alternatives considered

- **Record a decision-to-decline as a `current` decision rather than marking the proposal `rejected`.**
  Rejected in favor of an explicit terminal state on the proposal itself.
  A separate `current` decision reframes the declination as a new operative choice and scatters the record across two artifacts; marking the proposal `rejected` keeps the declination's own record in place, discoverable by inspecting the artifact that was declined.
- **Delete every declined proposal and rely on Git history.**
  Rejected: a deleted artifact is not legible or discoverable in the live corpus, which is exactly what an auditor reading the tree needs ([Legible lifecycle](../requirements/system/legible-lifecycle.md){id=note:req:233g9mc}).
  Git history reconstructs what was removed only for a reader who already knows to look and where.
  Deletion remains correct for a draft abandoned with no conclusion reached; the discriminator above separates the two cases.
- **Make placement the authority and derive status from the directory.**
  Rejected: a folder mirrors state but never overrides the authoritative field, so status is the authority and placement the mirror, not the reverse.
  Deriving terminal state from the directory would let a misfiled artifact misstate its own lifecycle.
- **Rely on the Git commit alone to time a retirement.**
  Rejected for the no-successor case: where nothing supersedes a retired artifact, the retirement moment is not legible from the artifact, only from history.
  The optional `obsoleted` field records it in the artifact for that case, and is unneeded where a superseding successor's `decided` already times it.

## Driven by

- groundedIn: [Legible lifecycle](../requirements/system/legible-lifecycle.md){id=note:req:233g9mc}
- groundedIn: [Know an artifact's maturity before relying on it](../needs/know-artifact-maturity.md){id=note:need:6pxykex}
- groundedIn: [Single Source of Truth](../principles/single-source-of-truth.md){id=note:principle:8691937}
- groundedIn: [Compute and Report](../principles/compute-and-report.md){id=note:principle:6e7f28k}
