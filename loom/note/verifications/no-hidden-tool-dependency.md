---
id: note:ver:t7fr33n
name: No hidden tool dependency
kind: verification
status: current
method: inspection
---

This verification confirms the method's floor: every operation the specifications define is performable, and every check they fix is reproducible in principle, by an actor with basic reading and writing alone, on artifacts that are plain text bound to no tool or vendor, with the method confining itself to representation and defined checks rather than enforcement.
The check inspects the normative specifications and the committed files; the verdict belongs to the Orchestrating Authority.

## Criteria

A pass requires that:

- every operation the substrate and pack specifications define (authoring an artifact, minting an id, citing, resolving a reference, walking the cascade, retiring an artifact) is stated so that an unaided actor can perform it with file access alone, with no step that names a required tool;
- every check the specifications fix is decidable from the committed files, so a tool accelerates but never gates participation;
- every artifact is a single plain-text file whose reading depends on no proprietary store, schema registry, or online service, so the corpus remains readable when any tool is gone;
- no specification assumes actor identity, permission, dispatch, or enforcement: everything that reaches into who and may is routed to the Orchestrating Authority, and the corpus authors no verdict or permission state.

A pass is all four holding across the specifications and the corpus.

## Procedure

By inspection.
A reader walks each defined operation and check in the substrate, the pack specifications, and the cascade and closure specifications, confirming per item that the procedure is performable and decidable from files alone, and scans the corpus for any artifact whose reading or validation would require more than text.
The inspection needs only the committed files, which is itself the property under check.

## Evidence

A run records the operation-by-operation confirmations and any step found to assume a tool, a service, or an authority the files do not carry.
The record is kept with the run by the Orchestrating Authority; it is not stored in this artifact.

## Relations

- verifies: [Universal participation](../requirements/stakeholder/universal-participation.md){id=note:req:j4kecn7}
- verifies: [File-native capture](../requirements/system/file-native-capture.md){id=note:req:mgdg9q0}
- verifies: [Durable, portable intent](../requirements/stakeholder/durable-portable-intent.md){id=note:req:93kczqj}
- verifies: [Representation, not enforcement](../requirements/system/representation-not-enforcement.md){id=note:req:agncpcc}
