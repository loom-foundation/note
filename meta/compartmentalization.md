# Compartmentalization

This repository authors Note in Note's own format.
Because the thing being authored is itself a methodology, the three compartments named in [README.md](README.md), Meta, Method, and Adopter, blur together under the hand, and the blur produces a recurring defect: the Meta fact that *we are authoring a methodology* leaks into a Method definition that should hold for any adopter.

This document is the discipline that keeps the compartments apart.
Read it before working anywhere under `note/`.

## Which compartment are you touching?

Ask what the subject of the change is.

If you are changing *how this repository works*, a prose convention or this discipline itself, you are in the Meta compartment.
It lives under `meta/`.

If you are changing *what Note is*, a Term, a Principle, a Need, a Requirement, or a Specification of the method, you are in the Method compartment.
It lives under `loom/note/`.
Its subject is any sustained body of work, never this repository in particular.

If you find yourself describing *a concrete system's* needs or requirements as the subject of a Method artifact, stop.
That is the Adopter compartment, and it belongs in an adopter's repository, not here.
Use it only as a cited example, clearly flagged as one.

## The read protocol

Before authoring in the Method compartment, read two things, in this order.

First, read `meta/` to learn *how* to work: the prose conventions and this discipline.
This is the how.

Second, read the current `loom/note/` files that neighbor your change to learn the *format to match*.
The corpus dogfoods Note, so the existing artifacts are the live template: their body structure, their relations, their register.
Match them rather than inventing a shape.
This is the what.

Doing the first without the second produces well-disciplined prose in the wrong format; doing the second without the first copies a shape without understanding the rule it serves.

## The universal-subject rule

A Method-compartment artifact defines a construct for every adopter of Note.
Its subject is therefore a sustained body of work, not a methodology, even though the one body of work being authored in this repository is, by coincidence, a methodology.

Two moves keep a definition universal.

Generalize the subject.
Write "a sustained body of work", or the appropriate general subject, not "a methodology" or "this corpus".

Cite the spectrum.
Name the range of things the construct applies to, a software system, a hardware product, a process, a methodology, so the universal scope is unmistakable.

### Worked example: the defect and its fix

The defect comes from the [decision that introduced the Principle kind](../loom/note/decisions/principles-first-class.md){id=note:dec:eym5t5g}.
Its Context originally opened:

> A methodology accumulates a small set of foundational commitments that guide judgment where no specific rule yet bears, and that a class of obligations follows from.

This defines a universal construct, the Principle, through the single thing this repository uses Note for.
A Principle applies to any sustained effort, so opening with "A methodology accumulates" bakes the Meta context into a Method definition.

The fix generalized the subject and cited the spectrum:

> A sustained body of work accumulates a small set of foundational commitments that guide judgment where no specific rule yet bears, and from which a class of obligations follows.
> The work may be a software system, a hardware product, a process, or a methodology like this corpus, and a Principle plays the same role in each.

### Naming this project is allowed when it is flagged as the instantiation

The rule forbids an instantiation *masquerading as* the definition.
It does not forbid naming this project's instantiation when that naming is explicit.

The Origin of [Compute and Report](../loom/note/principles/compute-and-report.md){id=note:principle:6e7f28k} does this correctly:

> The application to a methodology and its tool is this project's; the access-control and mechanism-policy lineage is the established part, the framing here is ours.

"Is this project's" labels the sentence as the instantiation, so the universal definition is not narrowed.
An instantiation labeled as such is allowed; an instantiation passing for the definition is the defect.

## The routing rule

When a piece of content needs a home, route it by its subject.

A normative property of the Note method, something every adopter must follow, belongs in `loom/note/`, as a Requirement, a Specification, or a Principle.

Expository how-to guidance for an adopter, orientation, worked walkthroughs, background, belongs in `docs/`.

A rule about how *this repository* authors its corpus belongs in `meta/`.

The test is the subject, not the phrasing.
"How to write a Requirement well" reads like authoring guidance, but if it states a property every adopter's requirements must have, it is a Method rule and belongs in `loom/note/`; only the part specific to authoring *this* corpus stays in `meta/`.

## Checklist

Before a Method-compartment change lands:

- The subject is a sustained body of work, not a methodology or this corpus.
- The spectrum is cited where the scope could otherwise be read as narrow.
- Any mention of this project is flagged as the instantiation, not written as the definition.
- The content sits in the compartment its subject dictates, `meta/`, `loom/note/`, or `docs/`, not the compartment it was first drafted in.
