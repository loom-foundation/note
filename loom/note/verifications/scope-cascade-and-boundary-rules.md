---
id: note:ver:c4sc8dw
name: Scope, cascade, and boundary rules
kind: verification
status: current
method: analysis
---

This verification confirms that scoped intent resolves as the cascade specification fixes: the scope graph is declared and acyclic, every deviation is complete and targets intent the scope actually inherits, the loud cases carry their rationale, effective intent is deterministically resolvable and never stored, and each bounded scope's boundary statement is present with its canonical sections.
The check executes the validation rules the scope-and-cascade specification itself declares ([Scope and cascade](../specifications/note/scope-and-cascade.md){id=note:spec:1r673tc}); it computes and reports findings only, and the verdict belongs to the Orchestrating Authority.

## Criteria

A pass requires that:

- the `parents` edges of every declared scope form a directed acyclic graph, and every scope id named anywhere (a `parents` list, a `scope` field, a `## Deviation` source, a `precedence` entry) resolves to a declared scope, with an unreachable upstream reported unresolved rather than invalid;
- every `## Deviation` entry names an operator from the closed set, a resolvable inherited source in force at an ancestor, and the source scope, with a rationale on every `replace` and `disinherit`, so a replacement or removal is never unexplained;
- every `precedence` entry names two distinct, incomparable ancestors, a point, and its own rationale;
- resolving effective intent at any scope by the specification's procedure terminates and is reproducible: two independent walks yield the same result, with comparable conflicts resolved by proximity and incomparable ties and every removal surfaced;
- no artifact stores a resolved effective-intent result, materialization with provenance being the one exception;
- each bounded scope carries one Context with its canonical sections (`## External entities`, `## What crosses the boundary`, `## What is out of scope`), and a re-authored Context only narrows silently, a widening carrying its rationale.

A pass is zero failures over the resolvable closure; a single-scope corpus passes vacuously on the graph criteria and is checked on its Context alone.

## Procedure

By analysis.
A static reader parses every manifest's scope block, builds the parent graph, and searches it for cycles and unresolvable ids; it parses every `## Deviation` and `precedence` entry against the closed grammar and the inheritance the graph licenses; it resolves effective intent at each scope twice, in different traversal orders, and compares the results; and it validates each Context's sections and, where a parent Context exists, compares boundaries for silent widening.
The reader only reads; it executes nothing, so the check is reproducible by anyone with the repository.

## Evidence

A run produces a report: the scope graph, each deviation and precedence entry with its validity, the surfaced ties and removals, the double-resolution comparison, and any boundary widening found without rationale.
The report is kept with the run by the Orchestrating Authority; it is not stored in this artifact.

## Relations

- verifies: [Scope and inheritance](../requirements/system/scope-and-inheritance.md){id=note:req:96smmcv}
- verifies: [Deviation operators on inherited intent](../requirements/system/deviation-from-inherited-intent.md){id=note:req:sd7ch4m}
- verifies: [Visible, attributable deviation](../requirements/system/visible-attributable-deviation.md){id=note:req:64eknb1}
- verifies: [Effective-intent resolution](../requirements/system/effective-intent-resolution.md){id=note:req:5xnajsm}
- verifies: [Hierarchically scoped intent](../requirements/stakeholder/hierarchically-scoped-intent.md){id=note:req:6n6jdyq}
- verifies: [Legible system boundary](../requirements/stakeholder/legible-system-boundary.md){id=note:req:w4k7n2h}
