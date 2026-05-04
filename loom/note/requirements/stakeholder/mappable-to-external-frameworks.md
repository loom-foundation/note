---
id: note:req:ddh4kfx
name: Intent mappable to external frameworks
kind: requirement
level: stakeholder
type: functional
status: current
---

An author shall be able to express, as part of the intent and on the obligation it concerns, the correspondence between an obligation and a control in an external framework, including which kind of correspondence it is, so the mapping is captured once, kept with the obligation, and read as the obligation is read.

## Source

See the Source of [Crosswalk intent to the frameworks it answers to](../../needs/crosswalk-to-external-frameworks.md){id=note:need:5mmrydr}.

## Rationale

An obligation that answers to an external framework carries that correspondence as real intent, and a mapping held apart from the obligation drifts from it.

The obligation here is only that the correspondence be expressible as intent and stay with the obligation; whether a framework's controls are referenced live or captured as a local copy, and how the correspondence is typed, are left to the system requirement and to specification.

How a framework's catalog is brought in, and how coverage is computed and reported, are a tool's concern, carried by Sett.

## Relations

- addresses: [Crosswalk intent to the frameworks it answers to](../../needs/crosswalk-to-external-frameworks.md){id=note:need:5mmrydr}
- decidedBy: [The compliance crosswalk pack](../../decisions/compliance-crosswalk-pack.md){id=note:dec:ve053yf}
- delivers: [Mapping Authored Beside the Obligation](../../offerings/framework-crosswalk/pr-mapping-authored-beside-the-obligation.md){id=note:pr:84wcxrm}
