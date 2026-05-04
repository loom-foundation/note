---
id: note:dec:nc2yrf4
name: Requirement levels
kind: decision
status: current
decided: 2026-06-12T00:00:00Z
---

A requirement carries a `level` that names the abstraction it sits on, with two default values, `stakeholder` and `system`.
The field is authoritative and the directory layout is a derived convenience.
The vocabulary is a per-corpus choice with this two-value default: the conformance floor requires no level, so a single-level prototype omits it and pays nothing.
Identity is the uniform opaque grammar that every kind shares, defined once in identity-and-designations, and the level is deliberately no part of it.

## Context

A requirement may sit on more than one abstraction level, and a method needs both a vocabulary for those levels and a place to record one.

Two levels carry the common case.
A stakeholder requirement is an obligation as the holder of a need states it; a system requirement is an obligation on the system that answers it.
The pairing is the dominant systems-engineering cut and reads clearly to any practitioner.
"Stakeholder" names whoever holds the need, which is broader than "user": a board that never touches the system can still impose an obligation on it, a right-to-be-forgotten obligation to meet a privacy regulation, for example.

The level is a classification, not a structural element.
The refinement that connects a system requirement to the stakeholder requirement it answers is carried by the derivation relation, so the level adds no structure the relation graph does not already hold; it is a readable label on a node.
A classification of that sort must stay free to change without disturbing anything that points at the requirement, which makes the level's relationship to identity the second question this decision settles: the level is kept out of the durable id entirely.

The identity grammar itself is not restated here.
Every kind, requirement included, uses one opaque grammar with no exception, defined once in [Uniform opaque identity](identity-and-designations.md){id=note:dec:jhgkwja}; this decision rests on that grammar and adds only the rule that the level is no part of it.

## Decision

- **Two default levels in an authoritative field.**
  A requirement carries a `level` field with two default values, `stakeholder` and `system`.
  The field is the authoritative record of the level; a directory that groups requirements by level is a navigation convenience derived from it, never a second source.

- **The level vocabulary is a per-corpus choice.**
  Two values are the default, sufficient for the common case.
  A corpus that earns a finer decomposition (a regulated systems-engineering effort distinguishing a component level, say) declares its own level vocabulary; a single-level prototype declares none.

- **The conformance floor requires no level.**
  A requirement is well-formed without a level, so a corpus that does not yet distinguish levels carries the field nowhere and pays nothing.
  The level is a rigor-bearing field a heavier profile may require, not a floor field.

- **The level is no part of identity.**
  A requirement's id is the uniform opaque id every kind shares.
  The level is excluded from it deliberately: a level is a classification that may change as a requirement is re-leveled, and an id that embedded the level would begin to lie the moment the classification changed, so re-leveling never disturbs identity.

## Forces and trade-offs

A stakeholder-versus-system cut is the dominant pairing and needs no defense, but naming the lower level `system` shares a word with the system-boundary term.
The overlap is coherent, not accidental: a system requirement is an obligation on the system, so the shared word reads true.

Keeping the level out of the id lets re-leveling stay free.
A requirement promoted from a system obligation to a stakeholder obligation, or a level vocabulary that gains a value, changes a label and disturbs no reference, because the reference carries the opaque id and the id never held the level.

The default of two values absorbs the cost of the choice.
A corpus that wants the common cut declares nothing and gets stakeholder and system; only a corpus that earns a third level pays the cost of naming one.

## Alternatives considered

- **Encode the level in the identifier (a `stakeholder`-or-`system` prefix).**
  Rejected: it couples identity to a mutable classification and makes the prefix mean a level for some artifacts where it means a kind for others, so a bare reference no longer reads cleanly and re-leveling strands citations.
  The level lives in its own field; identity stays opaque and uniform.

- **A fixed three-level enum (`stakeholder`, `system`, `component`) for every corpus.**
  Rejected against Proportionality: it forces every prototype to carry a level it rarely needs.
  A heavier profile may declare a finer vocabulary where regulated systems engineering earns it; the default stays two.

- **`intent` and `solution`, or `design`, as the level names.**
  Rejected: `intent` is the method's umbrella term for the whole corpus, and `solution` and `design` collide with the solution-free rule and the specification kind, so a system requirement named at the `solution` level would read as the leaked mechanism the rule exists to catch.

## Driven by

- groundedIn: [Uniform opaque identity](identity-and-designations.md){id=note:dec:jhgkwja}
- groundedIn: [Unambiguous, testable requirements](../needs/unambiguous-testable-requirements.md){id=note:need:e4k9w2n}
- groundedIn: [Unambiguous, testable obligations](../requirements/stakeholder/unambiguous-testable-obligations.md){id=note:req:h6n3k8w}
- groundedIn: [Tiered conformance](../requirements/system/tiered-conformance.md){id=note:req:bth0rxp}
- groundedIn: [Proportionality](../principles/proportionality.md){id=note:principle:es0vhzn}
