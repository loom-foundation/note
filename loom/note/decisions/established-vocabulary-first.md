---
id: note:dec:8f3m5vk
name: Reuse established vocabulary before coining new terms
kind: decision
status: current
decided: 2026-06-10T07:43:04Z
---

When Note needs a word for a relation, a kind, or a concept, it reaches first for the term the methods and standards it descends from already use, and coins a new one only where no established term fits or a coined one adds genuine, unique, and superior clarity.

A relation is fixed by the typed kinds at its two ends together with its verb, so a verb need not be globally unique; reusing an established verb across different end-kinds is cheap and keeps the vocabulary legible to anyone who knows the canon.

New vocabulary is a cost paid in learning and drift, justified only by the clarity it buys.

## Context

Note does not invent its concepts from nothing.
It stands on an established body of methods, standards, and literature, and borrows their vocabulary so a reader who knows the field recognizes Note's terms rather than learning a private dialect.

The canon Note draws on, by the area each informs.

Each term's `## Origin` records the specific lineage at the point of definition, and `docs/from-need-to-specification.md` records the value-side lineage in full; this list is the standing overview, not a duplicate of either.

- **Terminology and concept systems.**
  ISO 704 and ISO 1087 (the generic, partitive, and associative concept relations that underlie Note's typed term-relations).
- **Requirements engineering.**
  ISO/IEC/IEEE 29148 (the stakeholder-versus-system split, the *shall* obligation form, the solution-free rule, and verification versus validation); EARS, the Easy Approach to Requirements Syntax (the constrained-requirement patterns); INCOSE's Guide for Writing Requirements and Systems Engineering Handbook (the constraint type, the verification-method set, and the system, subsystem, and component decomposition); and ISO/IEC 25010 for the product-quality attributes.
- **Architecture description and modeling.**
  ISO/IEC/IEEE 42010 (architecture description); TOGAF (the architecture-principle template: Name, Statement, Rationale, Implications); the architecture-modeling tradition of ArchiMate and SysML/MBSE, where a concrete element realizes a more abstract one through the realization relationship and requirements relate by satisfy, derive, refine, and verify; and goal-oriented requirements engineering (KAOS, i*, GRL) for the spine-versus-transverse-anchor split.
- **Decision records.**
  Michael Nygard's Architecture Decision Record pattern (the Context, Decision, Consequences shape Note's decision body follows).
- **Value and customer modeling.**
  The Value Proposition Canvas (Osterwalder, Pigneur, Bernarda, and Smith) for jobs, pains, and gains and the reliever and creator pairing; Lanning and Michaels (McKinsey, 1988) for the value-proposition term; the Jobs-to-be-Done lineage (Levitt, Christensen, Ulwick, Klement) for the Need and Job; and the Kano model for the gain expectation ladder. The fuller value-side lineage (Quality Function Deployment and Voice of the Customer, Haley's benefit segmentation, Gutman's means-end chains, Kotler's market offering) is recorded in `docs/from-need-to-specification.md`.
- **System boundary and actors.**
  The C4 model's system-context view, the structured-analysis context diagram (DeMarco; Gane and Sarson), Jackson's Problem Frames, and UML actors, for the Context and Persona kinds.
- **Quality, risk, and the principle register.**
  ISO 9000 and ISO 9001:2015 (the management-system sense of a Principle, and the status and lifecycle terms); ISO 31000 (the risk sense); Dworkin's principles-versus-rules distinction (a rule applies all-or-nothing; a principle has weight and is balanced), which fixes what a Note Principle is; and the design-principle tradition (the Unix philosophy, SOLID, DRY, KISS, YAGNI, Dieter Rams), with DRY grounding Single Source of Truth and KISS and YAGNI grounding Earned Substance.
- **Identity, versioning, and the file substrate.**
  The persistent-identifier tradition (the DOI system and ISO 26324, the URN and URI split) for the durable identifier; Crockford Base32 for the opaque-id alphabet; Semantic Versioning for the version scheme; RFC 2119 for the normative keywords; and Codd's relational model and DITA's single-source pattern for Single Source of Truth.

TOGAF and ArchiMate are registered trademarks of The Open Group, and SysML and UML are Object Management Group specifications; they are named here nominatively, as lineage, with no implication of conformance, certification, or endorsement.

The Value Proposition Canvas is cited by name with credit; Note reproduces none of its diagram or text and renames away from its labels (Value Map to Offering, Customer Profile to Need), so the borrowing stays to the generic concepts and to nominative reference.

This register is not exhaustive and grows as Note borrows further; the standing preference it states is reuse before coinage.

## Decision

- **Reuse before coinage.**
  When naming a relation verb, a kind, or a concept, reach first for the established term the canon already uses for it.
  Coin a new term only where no established term fits, or where a coinage adds genuine, unique, and superior clarity that no borrowed term carries.
- **Verbs need not be globally unique.**
  A relation is identified by the typed kinds at its two ends together with its verb, so the same verb may name relations between different end-kind pairs without ambiguity; Note already reuses `relieves`, `creates`, and `addresses` this way.
  Avoiding a fitting verb merely to keep it unique is not a reason to coin.
- **Coinage carries the burden of proof.**
  A new term is justified where it is introduced, in a term's `## Origin` or in the decision that adds a kind or relation, by naming the established terms considered and why each was insufficient.
  A coinage with no such justification is a candidate for replacement by a canonical term.
- **The canon is recorded and cited.**
  The methods, standards, and literature Note borrows from are listed here and cited at the point of use, so every borrowing is traceable to its source.

## Forces and trade-offs

Reusing an established term costs a moment's check against the canon and the occasional verb that fits less than perfectly.

It buys immediate recognition for anyone who knows the field, and it grounds Note's claims in a body of work rather than in assertion.

Coining a term is sometimes right: where the canon has no word for a concept Note genuinely introduces, a precise coinage beats stretching a borrowed term past its meaning.
The rule is not "never coin"; it is "coin only when the clarity earned exceeds the cost of a new word to learn and keep honest", Earned Substance applied to vocabulary.

## Alternatives considered

- **Coin freely for internal consistency.**
  Rejected: a private dialect is unlearnable from the outside and drifts from the canon it silently parallels; recognition is worth more than a tidy internal scheme.
- **Forbid coinage entirely.**
  Rejected: some concepts Note introduces have no canonical name, and forcing a borrowed term onto them stretches the term until it lies.
- **Require every relation verb to be globally unique.**
  Rejected: the typed end-kinds already disambiguate a relation, so global verb uniqueness buys nothing and would force needless coinage.

## Driven by

- groundedIn: [Single Source of Truth](../principles/single-source-of-truth.md){id=note:principle:8691937}
- groundedIn: [Earned Substance](../principles/earned-substance.md){id=note:principle:yecemfe}

## Worked example

Naming the relation between a requirement and the principle it puts into practice, the natural first stop was the architecture-modeling tradition: ArchiMate and SysML define a realization relationship in which a concrete element realizes a more abstract one.
That established verb was considered and then set aside.
`realizes` carries UML interface-implementation baggage, and in a corpus that also draws on the Value Proposition Canvas the same verb would read two ways in one place; the full reasoning is in [Principles as a first-class kind](principles-first-class.md){id=note:dec:eym5t5g} under its alternatives.
`enacts` was coined instead: to enact is, in the Oxford sense, to put into practice or to make into law, which is the more precise fit for an obligation that puts a principle into practice.
The coinage earned its place against the canonical reuse because the borrowed term would have misread in this corpus.

Not adopting `realizes` for requirement → principle is specific to that relation and to the built-in spine pack.
The name is deliberately left available for an adopter-authored kind pack to use on its own end-kinds: a capability pack, for instance, might use `realizes` for a relation in which a concrete element realizes a more abstract capability, where no collision with the built-in pack arises.
