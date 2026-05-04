---
id: note:req:peh9g30
name: Non-breaking evolution with a guaranteed forward path
kind: requirement
level: stakeholder
type: constraint
status: current
---

Evolution of the method and of its reference tool shall preserve a defined forward path for every conformant corpus.

No released version shall leave an existing conformant corpus with no supported way to move forward.

## Source

See the Source of [Adopt without being stranded by the method's own evolution](../../needs/adopt-without-being-stranded.md){id=note:need:x4zqfws}.

## Rationale

Adopting a method and its format is a long-lived commitment.

If a later version can render an existing corpus unreadable with no migration, the commitment becomes a trap, and the fear of that trap discourages adoption.

The detailed rules (version declaration, within-major backward compatibility, a defined migration across majors, a deprecation window, and independent versioning of method and tool) are the system requirements derived from this one;
this requirement states the guarantee they serve.

Tier (how much a project has adopted) and version (how the method has evolved) are orthogonal;
this requirement is about the version axis.

## Relations

- addresses: [Adopt without being stranded by the method's own evolution](../../needs/adopt-without-being-stranded.md){id=note:need:x4zqfws}
