---
id: note:term:a5pxcwk
name: System Level
kind: term
status: current
---

The Level value that marks a requirement as an obligation on the system itself, verified against what is built rather than validated against stakeholder needs.

System Level is a value of Level (the level axis of a Requirement), not to be conflated with the System boundary concept: "System" names the boundary of what is under construction, while "System Level" names the refinement depth at which an obligation is expressed as a constraint on that boundary.
A system-level requirement is derived from a stakeholder-level requirement and answered by a specification; it is checked by verification against the built system.

## Inclusion test

Is the obligation placed on the system itself and verified against what is built, rather than stated in the terms of whoever holds the need and validated against the needs?
If so, it is at the System Level.
If instead the obligation answers to the stakeholders' needs and is validated against them, it is at the Stakeholder Level.

## Relations

- *is a value of* [Level](level.md){id=note:term:60yb5qr}
- *relates to* [System](../system-and-boundary/system.md){id=note:term:0jbwfkm} (verified against; a system-level obligation is confirmed against what is built)

## Origin

Oxford: "a set of things working together as parts of a mechanism or an interconnecting network", via Late Latin systema and Greek sustēma, "an organized whole".

In requirements engineering the system level names obligations on the solution itself; ISO/IEC/IEEE 29148 derives the system requirements specification from the stakeholder requirements and verifies it against the built system.
The level label "System Level" is kept distinct from the boundary term "System" so that the two readings of the word do not collapse into one another in the corpus vocabulary.
