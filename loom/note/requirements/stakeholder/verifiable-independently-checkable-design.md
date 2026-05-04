---
id: note:req:vh3k82n
name: Verifiable, independently checkable design
kind: requirement
level: stakeholder
type: functional
status: current
---

The design committed in a specification shall be checkable against an authority independent of the method's own assertions, so that what a specification claims is falsifiable by something other than the method, and so that a reader or verifier can confirm a design holds without taking the method's word for it.

## Source

See the Source of [Trust and drift visibility](../../needs/trust-intent-is-honored.md){id=note:need:46tkxcn}.

## Rationale

Tracing intent and detecting drift confirm that relationships are legible and current, but they do not confirm that what a specification asserts is itself sound;
a specification typed only by a label can be internally consistent and still wrong.

The trust this Need asks for therefore has a facet distinct from coverage and drift: a specification's content must be falsifiable against something outside the method, so confidence does not rest on the method's own say-so.

How content is checked, and against which independent authorities, is left to the system requirements.

## Relations

- addresses: [Trust and drift visibility](../../needs/trust-intent-is-honored.md){id=note:need:46tkxcn}
