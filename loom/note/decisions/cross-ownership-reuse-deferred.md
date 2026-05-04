---
id: note:dec:xq0wn7d
name: Cross-ownership reuse is deferred to tooling
kind: decision
status: current
decided: 2026-07-02T10:25:48Z
---

Drawing intent in from a source outside the corpus's line of ownership, or offering it out to one, is tool work: the method adds no subscription surface now.
What the files must carry already exists in the method's constructs; the workflow itself (publishing, pinning, drawing in, re-checking) belongs to tooling built on the method, the reference tool Sett first among them.

## Context

[Share and reuse intent across ownership lines](../needs/share-and-reuse-intent-across-ownership-lines.md){id=note:need:mqzq97r} asks for supply-chain reuse of intent: depend on a peer's published requirements at a pinned version, with provenance and drift visibility, where no inheritance line exists.
The need is inferred from the package-dependency and lateral-reuse patterns and marked so; the method has not met an adopter exercising it, and its facets name workflow moments (choose a version, draw in, confirm the source, stay current) more than file shapes.

What the files must carry is largely settled elsewhere.
An id names its corpus wherever the file travels ([Declared namespace identity](../requirements/stakeholder/declared-namespace-identity.md){id=note:req:78hqr3n}), a reference into an absent corpus degrades to unresolved rather than invalid ([Cross-repository resolution](../requirements/system/cross-repository-resolution.md){id=note:req:dxxvabc}), and a copied-in block carries its provenance ([Materialization of inherited intent](../requirements/system/materialization-of-inherited-intent.md){id=note:req:dssf1pp}).
What remains is operation: discovering a source, choosing and pinning a version, fetching a self-contained closure, and re-checking the upstream, none of which is representation.

## Decision

- **No new method surface now.**
  No kind, verb, field, or manifest block is added for cross-ownership sharing in 0.x.
- **The workflow is tool work.**
  Publishing an intent package, subscribing at a pinned version, drawing in a self-contained closure, and reporting upstream movement belong to tooling built on the method; the method confines itself to what the files carry.
- **A drawn-in copy rides the materialization shape.**
  The provenance block materialization fixes for inherited intent (source, scope, version or commit, date) is read by its fields, not by the relationship that motivated the copy, so a cross-ownership copy carries the same shape with a foreign namespace in its source.
- **Reopening.**
  Taken up as method surface when tool practice shows the files must carry something no construct carries (a subscription manifest, say), or when a real adopter exercises the need.
  Until then the coverage view keeps listing the need, and this record is the deliberate answer.

## Forces and trade-offs

Adding subscription constructs now would be unearned: the need is inferred, never observed, and every speculative kind or field is a new home for drift; the common adopter would pay for surface only supply-chain reuse uses.

Deferring costs visibility.
A strict coverage view reports a current need with no addressing obligation, which reads as a gap until this record is found.
That cost is accepted: the honest state is a real need consciously routed to tooling, and a decision is the method's instrument for recording exactly that.

Participation stays universal either way.
A drawn-in copy is plain files a reader needs no tool to read; the tool accelerates the subscription workflow, it never gates reading.

## Alternatives considered

- **Author the method surface now: a dependencies block in the manifest, a subscription construct, or both.**
  Rejected: speculative surface for an unobserved need, against Earned Substance and Proportionality, and the wrong moment to freeze a shape tooling has not yet exercised.
- **Route the need through existing constructs: promotion, federation, or fork.**
  Rejected: the need's own distinctions rule each out; promotion and federation act inside one ownership line, and a fork detaches from a former parent, while this source was never inside the line.
- **Silence: no record.**
  Rejected: the coverage view would keep reporting an unanswered need with nothing to find; a one-page record is the proportionate fix.

## Driven by

- groundedIn: [Share and reuse intent across ownership lines](../needs/share-and-reuse-intent-across-ownership-lines.md){id=note:need:mqzq97r}
- groundedIn: [Proportionality](../principles/proportionality.md){id=note:principle:es0vhzn}
- groundedIn: [Earned Substance](../principles/earned-substance.md){id=note:principle:yecemfe}
