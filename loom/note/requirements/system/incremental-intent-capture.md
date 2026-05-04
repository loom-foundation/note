---
id: note:req:m2x8k5p
name: Incremental capture of recovered intent
kind: requirement
level: system
type: functional
status: current
---

Note shall ensure that intent recovered from an existing system can be captured incrementally and partially, with each artifact's maturity and the confidence of each claim marked honestly, so a corpus may faithfully describe a real system without first being complete.

## Rationale

Brownfield adoption requires that a corpus be valid while still partial and while holding low-confidence, recovered claims.

The method already carries the vocabulary for this: an artifact's maturity is legible in its status, and a claim may carry a validation tier.

This requirement names the obligation that those let a corpus grow from an existing system rather than demanding completeness or overstated confidence, and that recovered intent is distinguished from forward-authored intent by its tier and status rather than by a new field.

The mechanisms are specification.

## Relations

- derivedFrom: [Incremental adoption of an existing system](../stakeholder/incremental-adoption.md){id=note:req:h7n4k2w}
- delivers: [Honest Confidence Marking](../../offerings/start-where-you-are/pr-honest-confidence-marking.md){id=note:pr:04xvzk6}
- delivers: [Confidence Carried on Every Claim](../../offerings/start-where-you-are/gc-confidence-carried-on-every-claim.md){id=note:gc:gch0nst}
