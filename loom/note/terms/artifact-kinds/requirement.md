---
id: note:term:tr9zna6
name: Requirement
kind: term
status: current
---

A statement, in obligation form (*shall*), of what must be true of the solution.

A Requirement traces to a Need, or to a Pain it relieves, a Gain it creates, or a Job it addresses, directly or through a coarser Requirement, and constrains the solution *without prescribing it*.

A Requirement is satisfiable by more than one design; choosing among them is design work, not the Requirement's.

## Inclusion test

Is it stated as an obligation, traceable to a Need, and satisfied by the solution rather than describing how the solution works?

If it describes a mechanism, it is a Specification, or it is a Requirement with a leaked solution (a defect), unless it is a Constraint with a stated external source.

## Relations

- *addresses* [Need](need.md){id=note:term:x4vqdj1}
- *addresses* [Job](job.md){id=note:term:41qzg6f}
- *relieves* [Pain](pain.md){id=note:term:hb74nmn}
- *creates* [Gain](gain.md){id=note:term:7e4f92v}
- *delivers* [Pain Reliever](pain-reliever.md){id=note:term:7qrdxnp}
- *delivers* [Gain Creator](gain-creator.md){id=note:term:g9fxrs5}
- *carries* [Type](../requirement-typing/type.md){id=note:term:mwwzghp}
- *carries* [Level](../requirement-levels/level.md){id=note:term:60yb5qr}
- *contrasts with* [Specification](specification.md){id=note:term:9xd6ejd} (obligation versus design)

## Origin

General English (Oxford: "a thing that is needed or wanted; a condition which must be complied with").

Standardized as an artifact kind in ISO/IEC/IEEE 29148:2018 and the INCOSE Guide for Writing Requirements, which mandate *shall* language and the rule that a requirement constrains without specifying the solution.
