---
id: note:dec:ekpecn7
name: Proposable decisions
kind: decision
status: current
decided: 2026-07-02T00:00:00Z
---

A decision artifact may exist before it is ratified: context laid out, options weighed, recommendation made, but no timestamp yet set.
The `decided` field is required only when a decision reaches `current` or `obsolete`; it is omitted while the decision is `tbd`, `draft`, or `rejected`.

## Context

The propose-then-ratify loop is central to how Note is used collaboratively.
An author researches a question, names the forces, evaluates the alternatives, and sets a recommendation.
A second actor (a team, a reviewer, or a ratifying authority) reads the proposal, accepts or amends it, and ratifies it by moving `status` to `current`.

The file-format specification previously required `decided` on every decision artifact, unconditionally.
A decision drafted for ratification therefore could not validly exist: it either had to carry a false or placeholder timestamp, or it was malformed by the schema it was meant to conform to.
That contradiction blocked the propose-then-ratify loop at the format level.

The `decided` field is a timestamp; a timestamp records when an event occurred.
Before ratification, the ratification event has not occurred.
Carrying a false timestamp to satisfy a schema requirement is a form of data falsification the method should not invite.

## Decision

- **`decided` is required when `status` is `current` or `obsolete`, and omitted when `status` is `tbd`, `draft`, or `rejected`.**
  The field's presence is gated on lifecycle state rather than kind alone.
  A rejected decision never reached `current`, so it carries no ratification timestamp.
- **A proposal deliberately declined is recorded as `rejected`, not deleted.**
  Where a draft proposal is weighed and the conclusion to decline is worth keeping as a record, it moves to `rejected`; a proposal merely abandoned with no conclusion reached is deleted.
- **No sentinel value.**
  The field is absent (not present in frontmatter) for draft and tbd decisions; it is not set to a placeholder string such as `pending`.
  A timestamp field that holds a non-timestamp value is a type violation; a missing field is the correct representation of an event that has not occurred.
- **The ratification moment sets the timestamp.**
  When a decision is moved to `current`, the ratifying actor sets `decided` to the RFC 3339 UTC timestamp of that act.
  The wall-clock time may be `00:00:00` when only the date is recorded.

## Forces and trade-offs

Gating the field on lifecycle state adds a conditional to the schema.
The cost is a slight increase in schema complexity; the check becomes "if status is current or obsolete, decided must be present and well-formed" rather than "decided must be present and well-formed".
That conditionality is already present elsewhere in the schema: `last_reviewed` earns its place once an artifact reaches `current`, and `supersedes` / `superseded_by` are optional fields whose use is lifecycle-conditional in practice.
A conditional required field is not a novel shape for this format.

The benefit is correctness: a draft decision that lacks a ratification timestamp is not malformed; it is accurate.
Removing the false-timestamp pressure also removes an incentive to back-date or approximate, which would erode the reliability of the `decided` field across the corpus.

## Alternatives considered

- **Keep `decided` always required; a proposal carries a false or placeholder timestamp.**
  Rejected: a timestamp field exists to record when an event occurred.
  Requiring it before the event occurs either invites falsification or makes every draft decision technically malformed.
  Neither outcome serves the corpus's own Checkable well-formedness requirement.

- **A sentinel value such as `decided: pending`.**
  Rejected: the field is typed as an RFC 3339 UTC timestamp.
  Accepting a non-timestamp value in a timestamp field undermines the type contract, makes the field untrustworthy for tooling, and obscures rather than clarifies the lifecycle state.
  The `status` field already carries the lifecycle signal; `decided: pending` would duplicate it in a weaker, untyped form.

## Driven by

- groundedIn: [Universal artifact lifecycle and its transitions](artifact-lifecycle.md){id=note:dec:gfwq0mv}
- groundedIn: [Single Source of Truth](../principles/single-source-of-truth.md){id=note:principle:8691937}
- groundedIn: [Proportionality](../principles/proportionality.md){id=note:principle:es0vhzn}
