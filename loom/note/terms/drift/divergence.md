---
id: note:term:47bcgvy
name: Divergence
kind: term
status: current
---

The condition where an implementation no longer honors the contract a specification describes.

Divergence is about behavior, not text.

## Inclusion test

Has the running behavior parted from the contract, independent of whether any text changed?
If so, it is divergence; if instead the text of a relied-upon artifact moved but the behavior still honors the contract, that is staleness.

## Relations

- *contrasts with* [Staleness](staleness.md){id=note:term:psh3vcg} (the text of a referenced artifact moved; divergence is the behavior parting from the contract)

## Origin

General English (Oxford: "the process or state of diverging", from Latin *divergere*, to bend or move apart).

The corpus narrows the everyday sense of two things drifting apart to a specific parting: running behavior pulling away from the contract its specification states, whether or not any text was touched.

The behavior-versus-conformance framing is standard in software assurance, where a system is said to diverge from its specification when its observed behavior no longer satisfies the stated contract.
