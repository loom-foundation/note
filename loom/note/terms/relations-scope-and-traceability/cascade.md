---
id: note:term:5b6cbtr
name: Cascade
kind: term
status: current
---

The composition of inherited intent across Scopes: an inner scope relates to intent from an outer scope by adding to it, replacing it, or disinheriting it.

The result at any scope is the effective intent.

## Inclusion test

Does the relationship compose the *same* intent across scopes, rather than refine it within a layer?
If so it is Cascade.

## Origin

General English (Oxford: "a process whereby something, typically information or knowledge, is successively passed on"), and the waterfall image of an outer source flowing down and being modified at each step.

The add / replace / disinherit composition follows the cascade in CSS, where a declared value is inherited from an outer context and an inner rule may augment, override, or unset it; the term is borrowed for the same shape over Scopes.
