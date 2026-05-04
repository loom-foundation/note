---
id: note:dec:p13e5ay
name: The layer model
kind: decision
status: current
decided: 2026-06-12T00:00:00Z
---

A Layer is a coherent body of artifacts riding the one substrate for a single concern.
The method names three Layers: note, which is live and carries intent; plan, which is deferred and carries work and its order; and guild, which is reserved, named for the disciplines, roles, and skills that govern AI agents, but unspecified in this version.
A Layer is a method surface an adopter authors into, never a tool's space: a tool keeps its own hidden directory and never lives in a Layer.
A Layer is enabled by its manifest, not by a folder: a layer-root is wherever that Layer's manifest sits, and a `loom/<layer>/` folder is the navigational mirror of an enabled Layer, not the switch.

## Context

A sustained body of work, whether a software system, a hardware product, a process, or a methodology like this corpus, accumulates more than one concern that wants its own coherent body of artifacts.
The intent of the work, what is wanted and why, is one such body.
The plan of the work, the units of effort and the order they run in, is another, and it answers to different questions and a different cadence.
The disciplines that govern the agents doing the work, their roles and the skills each carries, are a third.

These bodies share machinery.
Each captures its content in the kind-agnostic substrate that carries the file envelope, identity, lifecycle, typed relations, scope and cascade, and the citation surfaces ([Kind-agnostic substrate and kind packages](substrate-and-kind-packages.md){id=note:dec:w4awceq}).
What differs between them is the concern, not the substrate: each rides the same machinery for a different purpose.
Naming that unit, the Layer, lets the method add a concern without inventing a second machinery, and lets an adopter enable a concern without taking on the others.

Two questions the Layer raises have to be settled here.
First, what makes a Layer enabled, since an adopter who authors only intent should not be presumed to be running a plan.
Second, where a Layer ends and a tool begins, since a tool that materializes or indexes a Layer is not itself part of any Layer.

## Decision

- **A Layer is a concern riding the substrate.**
  A Layer is a coherent body of artifacts that rides the one substrate to serve a single concern of the work.
  The substrate is shared across every Layer; the concern is what a Layer names.
  A Layer carries its own kinds through the pack mechanism, its own manifest, and its own root; it does not carry its own machinery.

- **Three named Layers: note, plan, guild.**
  - **note** is the live Layer: it carries intent, the want and the why, in the spine and discovery packs.
    It is the only Layer this version specifies in full.
  - **plan** is the deferred Layer: it carries the work and its order, the unit of effort and what each depends on.
    Its pack is designed and named but not landed in this version ([The plan pack](plan-pack-deferred.md){id=note:dec:p1peaam}).
  - **guild** is the reserved Layer: it is named for the disciplines, roles, and skills that govern AI agents doing the work.
    It is listed among the Layers so the model is complete, but this version specifies no kinds and no format for it.

- **A Layer is a method surface; a tool keeps its own space.**
  An adopter authors into a Layer, and the Layer's artifacts are primary work products.
  A tool's generated and operational state lives in the tool's own hidden directory, a tool's `.sett/` for example, which is never a Layer and never holds Layer content.
  The separation matches the placement rule that keeps the corpus out of the tool's space ([Adopter corpus placement](corpus-placement.md){id=note:dec:q2v7nk3}).

- **The layer-root rule: the manifest is the root, the folder is the mirror.**
  A layer-root is wherever that Layer's manifest sits.
  The recommended adopter placement nests each Layer under the umbrella, `loom/note/`, `loom/plan/`, `loom/guild/`, so folder presence is the navigational mirror of an enabled Layer.
  The folder is the mirror, never the switch: the manifest is authoritative for whether a Layer is enabled and for everything that affects validation, consistent with the manifest authority the substrate fixes ([Kind-agnostic substrate and kind packages](substrate-and-kind-packages.md){id=note:dec:w4awceq}).
  A corpus that keeps a non-normative placement, as this project does, still has a layer-root wherever its note-layer manifest sits, even without a `loom/` folder.

- **The guild Layer is named for the method, not for a tool.**
  Guild names the *method* that governs roles, skills, and disciplines, the way Note names the method that governs intent.
  An adopter's roles and skills are their instantiation of the guild method, sourced perhaps from a tool, exactly as their intent is their instantiation of Note.
  The Layer therefore carries the method name, never a tool's name.

## Forces and trade-offs

Naming the Layer earns its substance on the three concerns that already exist: intent is live, plan is designed, and the agent disciplines are a real third body the work needs a home for.
A Layer that rode a separate machinery for each concern would multiply the substrate; one substrate under several Layers keeps the machinery single and the concerns separate, which is the split the factoring exists to make.

Reserving guild without specifying it states the model's full shape while keeping this version's surface small.
The cost is a named Layer an adopter cannot yet author into; the benefit is that the layer list does not change shape when guild lands, so a corpus that reads the list today reads the same list tomorrow.

Making the manifest, not the folder, the switch costs a reader one indirection: the presence of a `loom/note/` folder strongly suggests but does not prove the note Layer is enabled.
Accepted: the folder-as-switch rule cannot express a non-normative placement, and it would declare no Layer enabled in a corpus that places its Layers outside `loom/`, including this one, so the manifest has to be the authority and the folder the mirror.

## Alternatives considered

- **One undifferentiated corpus with no Layer concept.**
  Rejected: it gives the plan and the agent disciplines no home but the intent corpus, mixing the want with the work order and the governing roles, three concerns with different cadences and different readers.
  The Layer separates them without a second machinery.

- **A separate substrate per concern.**
  Rejected against Earned Substance: the concerns differ in their kinds, not in their envelope, identity, lifecycle, relations, scope, or citation surfaces, so a second substrate would duplicate the machinery the first already carries.
  One substrate under several Layers is the cheaper, single-source shape.

- **Folder presence enables a Layer (the folders are the list).**
  Rejected: it self-destructs against non-normative placement, declaring no Layer enabled in a corpus that does not use a `loom/` folder, and it splits authority from the manifest that already governs validation.
  The manifest is the switch; the folder is the navigational mirror.

- **Name the reserved Layer for the tool that sources its roles.**
  Rejected: a Layer is a method surface, so it carries the method's name; tying the Layer to a tool would couple the method to one tool and break the parallel with the note Layer, which is named for Note and not for any tool.

## Driven by

- groundedIn: [Kind-agnostic substrate and kind packages](substrate-and-kind-packages.md){id=note:dec:w4awceq}
- groundedIn: [Single Source of Truth](../principles/single-source-of-truth.md){id=note:principle:8691937}
- groundedIn: [Earned Substance](../principles/earned-substance.md){id=note:principle:yecemfe}
- groundedIn: [Intent that outlives its tooling](../needs/intent-outlives-tooling.md){id=note:need:jwvn9b7}
