---
id: note:pr:cvarqvw
name: Drift Surfaced Early
kind: pain-reliever
status: current
---

Staleness and divergence are detectable from the files, so a contract that moved, or behavior that parted from it, surfaces for re-check before it ships. This holds even when the contract was revised under an unchanged id: a dependent that relied on the older text is surfaced as stale rather than left to rest silently on wording it no longer matches.

## Relations

- partOf: [Trust by inspection](../trust-by-inspection.md){id=note:offering:53tjnhp}
- relieves: [Divergence Surfaces at Failure](../../needs/trust-intent-is-honored/pain-divergence-surfaces-at-failure.md){id=note:pain:1e0h3d0}
- relieves: [Informal Contracts Diverge Silently](../../needs/trust-intent-is-honored/pain-informal-contracts-diverge-silently.md){id=note:pain:dxstn0f}
- relieves: [Relied-Upon Artifact Revised Under a Stable Id](../../needs/trust-intent-is-honored/pain-relied-upon-artifact-revised-under-stable-id.md){id=note:pain:3x7k2vp}
