# Meta

This directory holds Note's Meta compartment: the rules and disciplines by which *this repository* authors and maintains the Note corpus.

It is not part of the Note method.
It is project-state of the Note repository, the way a team's own contributor guide is project-state and not part of the product the team ships.

## Three compartments

This repository authors Note in Note's own format.
Because the thing being authored is itself a methodology, three compartments blur together easily; this section names them so they stay apart.

**Meta, the how.**
The authoring discipline this repository applies to produce the corpus.
Its subject is our own working process, and its audience is whoever maintains Note, human or AI.
It lives here, under `meta/`.

**Method, the what.**
Note itself: the universal method for capturing intent, applicable to any sustained body of work, whether a software system, a hardware product, a process, or a methodology like this corpus.
Its subject is Note, defined for every adopter, and its audience reads it as the definition of the method.
It lives under `loom/note/`, and it is *Note's own* loom/note/.

**Adopter, the why.**
Note applied to a concrete system in someone else's repository: their needs, their requirements, their design.
Its subject is that system, and its audience is that adopter's team.
It is *a Note user's* loom/note/, and it never lives in this repository.

## Note's loom/note/ is not a Note user's loom/note/

The Method compartment and the Adopter compartment both live at a layer root called `loom/note/`, and that shared name is the source of the most common authoring error here.

`loom/note/` in *this* repository is the Method: the generic definition of Note.
`loom/note/` in an *adopter's* repository is the Adopter compartment: one concrete instantiation of Note on a system.

A construct defined in Note's loom/note/, a Term, a Principle, or a Requirement kind, is therefore defined for *any* body of work, not for the one this repository happens to be, which is a methodology.
Writing such a definition as though it belonged only to methodologies collapses the Method compartment into the Meta compartment.
That collapse is the recurring defect [compartmentalization.md](compartmentalization.md) exists to prevent.

## What lives here

- [compartmentalization.md](compartmentalization.md): the discipline that keeps the three compartments apart, including the read protocol to follow before authoring and the rule that routes a piece of content to its correct compartment. Read it before working on `note/`.
- [prose-conventions.md](prose-conventions.md): the prose conventions the corpus's artifacts and meta are written in.
