---
id: note:term:80049zb
name: Orchestrating Authority
kind: term
status: current
---

The external authority that holds actor identity and decides permission: who an actor is, what authority a role carries, who may make a transition, and who may approve a deviation.

Note does not provide this: it defines the representations and checks an Orchestrating Authority consumes; Sett computes and reports over them, likewise deciding nothing.

The role can be played by a full orchestration system such as Loom, or by a continuous-integration pipeline with code-owners and protected branches, or by a human reviewer.

## Inclusion test

Does the statement reach into *who* may act or whether an action is *permitted*?
If yes, it belongs to the Orchestrating Authority, not to Note or Sett;
if instead it concerns *what* a well-formed artifact looks like or whether a check holds, that is Note or Sett.
(See `context.md`.)

## Origin

General English: "orchestrating" in the sense of arranging and coordinating the parts of an undertaking to a desired effect (Oxford: "arrange or direct the elements of (a situation) to produce a desired effect"), paired with "authority" as the right to decide and to permit.

The term is a coinage of this corpus: it names the external authority that Note and Sett presuppose but deliberately do not provide, the seam at which representation hands off to permission.
