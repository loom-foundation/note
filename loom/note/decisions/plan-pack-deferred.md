---
id: note:dec:p1peaam
name: The plan pack
kind: decision
status: current
decided: 2026-06-12T00:00:00Z
---

The method defines a **plan** pack carrying a **task** kind (a unit of work to be done, distinct from a requirement, which states what must be true), a **`dependsOn`** field (task to task, the central authored planning fact), an optional `estimate`, and the verb **`delivers`** that traces a task into the intent graph.
From the authored `dependsOn` graph a tool computes the schedule structure (parallelizable sets, topological orders, the critical path, per-task float, the next-dispatchable set), while wall-clock dates and resource calendars stay deliberately out of scope.
The design is settled here, but the pack does not land in this version: it is deferred entirely, to land as the proof-of-concept pack once the pack membrane is proven.

## Context

A sustained body of work, whether a software system, a hardware product, a process, or a methodology like this corpus, eventually has to be sequenced: the work breaks into units, the units depend on one another, and someone has to know what can start now and what is on the longest path.
Planning is a real and distinct concern from intent: a requirement states what must be true of the result, while a task is work to be done toward it, and conflating the two loses the difference between a goal and the labor that reaches it.

The pack's design is settled and its research is done, but it does not land in this version for three reasons that compound.
It is tool-heavy: the value of a `dependsOn` graph is the schedule structure computed from it, and that computation (critical path, float, the dispatchable frontier) lands in the tool, not in the files, so the pack is thin without the tool that reads it.
It overlaps an unsettled orchestration question, how work is dispatched and by whom, which is not yet decided and which the planning model would have to assume.
And the pack mechanism it would ride is itself new: the discipline is to prove the membrane between substrate and pack on the built-in packs first, then land the plan pack as the proof-of-concept pack that exercises the membrane from the outside.

## Decision

- **A task kind, distinct from a requirement.**
  A task is a unit of work to be done.
  It is not a requirement: a requirement states a condition the result must satisfy, while a task names labor undertaken toward the result, so the two are different kinds with different lifecycles, and the model keeps them apart rather than overloading one.

- **A `dependsOn` field is the central authored planning fact.**
  A task reaches another task through `dependsOn`, authored on the dependent task, naming the task that must precede it.
  Its inverse is `blocks`, a derived view.
  The dependency graph is kept acyclic, so a topological order always exists.
  An edge may optionally carry a dependency type, `FS`, `SS`, `FF`, or `SF` (finish-to-start, start-to-start, finish-to-finish, start-to-finish), defaulting to `FS`, the ordinary "this finishes before that starts" case.

- **An optional `estimate`.**
  A task may carry an optional `estimate`, either a single value or an optimistic, most-likely, and pessimistic triple for a corpus that wants a three-point estimate.
  It is optional: a corpus that sequences without estimating pays nothing for it.

- **The verb `delivers` traces a task into the intent graph.**
  A task reaches the intent it serves through `delivers`, authored on the task, naming a requirement or a need it advances.
  This ties the plan back to the why: a unit of work is legible as the labor toward a stated obligation or want, not a free-floating to-do.

- **Schedule structure is computed; calendars and levelling are out of scope.**
  From the authored `dependsOn` graph a tool computes the parallelizable sets, the topological orders, the critical path, the per-task float, and the next-dispatchable set, all derived views, never authored.
  Wall-clock dates, resource calendars, and resource levelling are deliberately out of scope: a corpus that needs them exports the graph to a scheduler, and the method does not reimplement one.

- **The pack is deferred entirely from this version.**
  No part of the plan pack lands now: the task kind, the `dependsOn` field, the `delivers` verb, and the computed schedule are all absent from this version's built-in packs.
  The pack lands once the substrate-and-pack membrane is proven on the built-in packs, as the proof-of-concept pack that first exercises the membrane.

## Forces and trade-offs

Deferring the whole pack, rather than landing a thin authored core now and the computation later, keeps the pack coherent: its value is the schedule structure a tool derives, so shipping `task` and `dependsOn` without the computation that reads them would ship a planning kind that does not yet plan, against Earned Substance.
The pack earns its place when the tool that computes from it does too, and the two land together.

Settling the design now, while deferring the pack, costs one decision record and fixes the boundary that the research resolved: `dependsOn` is the one authored planning fact, everything downstream of it is computed, and wall-clock scheduling is out of scope.
Recording that boundary here keeps a later pass from re-litigating it or smuggling a calendar into the method.

The deferral is safe for the same reason the risk kind's is: a pack is additive against the substrate-and-pack model, so landing it later changes nothing a current corpus authored.
It is the natural first external exercise of the pack membrane, which is why it is sequenced to follow the membrane's internal proof rather than to precede it.

## Alternatives considered

- **Land the plan pack in this version.**
  Rejected: the pack is tool-heavy, its value living in a critical-path computation the tool performs, so landing the authored kinds without the tool ships a thin pack; it also overlaps the unsettled orchestration question, which the planning model would have to assume; and it would be the first pack to ride the membrane, which the discipline proves internally first.

- **Land the authored core (`task`, `dependsOn`) now and add the computed schedule later.**
  Rejected against Earned Substance: a `dependsOn` graph with no tool to compute the critical path, the float, and the dispatchable frontier is a planning kind that does not yet plan, so the authored core and the computation that gives it value land together, not apart.

- **Include wall-clock dates, resource calendars, and resource levelling in the pack.**
  Rejected: those are a scheduler's job, and reimplementing one inside the method would be large, perpetually incomplete, and outside the pack's purpose; the pack authors the dependency graph and computes its structure, and a corpus that needs dates exports to a scheduler.

## Driven by

- groundedIn: [Kind-agnostic substrate and kind packages](substrate-and-kind-packages.md){id=note:dec:w4awceq}
- groundedIn: [Proportionality](../principles/proportionality.md){id=note:principle:es0vhzn}
- groundedIn: [Earned Substance](../principles/earned-substance.md){id=note:principle:yecemfe}
