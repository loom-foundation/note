---
id: note:dec:t3rmvrb
name: Pack verbs are authorable between terms
kind: decision
status: current
decided: 2026-07-02T10:44:22Z
---

A pack verb may be authored between two terms wherever the owning pack defines an endpoint row for the kinds those terms name.
Such an edge documents the kind model; it adds no new endpoint legality and no instance-level obligation.

## Context

Twelve terms author pack verbs (addresses, satisfies, verifies, relieves, creates, delivers, expresses) in their Relations sections, describing how the kinds they define relate: the Pain Reliever term relieves the Pain term as the kinds' instances do each other.
The substrate carried the practice in a single sentence, that structural verbs are reused verbatim, which left the readiness review unable to tell sanctioned reuse from de facto extension.

## Decision

- A pack verb is authorable between terms exactly where the owning pack defines an endpoint row for the kinds the two terms name; the verb keeps its pack meaning, read at the kind level.
- The edge is documentation of the kind model: it creates no endpoint legality the pack does not already define, and it obligates no instance.
- The closed term-relation set (is a, is part of, and the rest) remains the vocabulary for everything that is not a kind-level reading of a pack verb.
- The substrate's term-relations section states the rule explicitly, replacing the single sentence.

## Forces and trade-offs

Letting terms reuse pack verbs risks a reader mistaking a kind-level note for an instance-level edge.
Accepted: the endpoint-row condition means the reading is always the one the pack already fixed, and the alternative (a parallel described-by vocabulary for terms) would restate every pack verb under a second name, pure drift surface.

## Alternatives considered

- **Forbid pack verbs between terms and rewrite the twelve.**
  Rejected: the kind model would lose its most precise statement, and the rewrite would land on prose that says the same thing less checkably.
- **Coin term-level twins for each pack verb.**
  Rejected: a duplicated vocabulary with a per-verb mapping to maintain, against Single Source of Truth for no reader gain.

## Driven by

- groundedIn: [Terms and personas as first-class, scoped kinds](terms-and-personas-as-kinds.md){id=note:dec:t4w8k2n}
- groundedIn: [Kind-agnostic substrate and kind packages](substrate-and-kind-packages.md){id=note:dec:w4awceq}
