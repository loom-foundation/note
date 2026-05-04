---
id: note:term:1q7g2py
name: Constraint
kind: term
status: current
---

A restriction on the *solution space*.

A Constraint may be solution-free (for example, an upper bound on resource use), or it may name a mechanism when an external force imposes it, in which case it must carry that force as its source.

## Inclusion test

Does it restrict the space of acceptable solutions rather than describe what the system does or what quality it exhibits?
If so it is a Constraint; if instead it names a mechanism with no stated external force imposing it, that is a leaked solution, not a Constraint.

## Relations

- *is a value of* [Type](type.md){id=note:term:mwwzghp}
- *contrasts with* [Functional](functional.md){id=note:term:5s5vpma} (states what the system does, a behavior or capability)
- *contrasts with* [Non-Functional](non-functional.md){id=note:term:a3gg1dj} (states a quality the system exhibits)

## Origin

The functional / non-functional split is standard in software requirements practice (ISO/IEC 25010 names the quality, non-functional, attributes).

The Constraint type follows INCOSE usage, where a constraint bounds the design rather than describing behavior.
