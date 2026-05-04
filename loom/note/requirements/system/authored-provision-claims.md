---
id: note:req:pr0vc74
name: Authored provision claims with derived coverage
kind: requirement
level: system
type: functional
status: current
---

Note shall represent provision as a typed edge authored on the providing system-of-interest, pointing at the offering, value-proposition, pain-reliever, or gain-creator it provides, and authored on no other end.

The effective provision of an offering shall be derivable from the authored claims by expanding a coarse claim to the facets the offering is composed of and taking the union across systems, with overlapping claims surfaced as shared provision and never reconciled silently.

A provision claim shall remain an authored claim distinct from its evidence: the as-built state substantiates or contradicts it, and a divergence is a reportable finding, never a stored verdict or an authored downward edge.

## Rationale

The provider carries the edge so the value an offering states stays clean of its provider; the inverse view is derived, per [Single authoritative representation per relationship](single-authoritative-relation.md){id=note:req:s5fh0e8}.

Expansion to facet granularity lets a coarse claim naming a whole offering and a fine claim naming one reliever compose in one derived view, so an offering built across several systems reads as the union of what each provides.

The claim-and-evidence split mirrors the value proposition and its fit, and versions are tagged snapshots of the corpus, so what a version claims is read at its marker; the choices are recorded in [The system-of-interest provides the value](../../decisions/system-of-interest-provides-value.md){id=note:dec:swar6np}.

## Relations

- derivedFrom: [Attributable, versioned provision](../stakeholder/attributable-versioned-provision.md){id=note:req:atr7vpn}
- decidedBy: [The system-of-interest provides the value](../../decisions/system-of-interest-provides-value.md){id=note:dec:swar6np}
