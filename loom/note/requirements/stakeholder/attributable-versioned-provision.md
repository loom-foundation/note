---
id: note:req:atr7vpn
name: Attributable, versioned provision
kind: requirement
level: stakeholder
type: functional
status: current
---

A reader shall be able to attribute an offering's value to the system-of-interest that provides it, and to read a version's claimed value from the corpus at that version's marker, so that who provides this value and what a version delivers are answerable from the files without recomputing coverage from the code.

## Source

The provider-attribution and per-version situations of [Know the real product behind the intent](../../needs/know-the-real-product.md){id=note:need:m0h1ncg}: a product delivered by several services with responsibility scattered across prose, shipped features reading identically to planned ones, and a capability whose availability depends on which product version actually carries it.

## Rationale

Which system is responsible for which value, and whether a version has it, otherwise lives in prose and tribal memory, exactly the state the need records.

The method's answer is decided: an authored provision claim carried by the provider, versions as tagged snapshots of the corpus, and computed as-built evidence auditing the claim ([The system-of-interest provides the value](../../decisions/system-of-interest-provides-value.md){id=note:dec:swar6np}).
This requirement states the reader-facing property and leaves the representation to the system requirement derived from it.

## Relations

- addresses: [Know the real product behind the intent](../../needs/know-the-real-product.md){id=note:need:m0h1ncg}
- decidedBy: [The system-of-interest provides the value](../../decisions/system-of-interest-provides-value.md){id=note:dec:swar6np}
