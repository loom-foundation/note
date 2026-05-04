---
id: note:term:644v69v
name: Relation
kind: term
status: current
---

A typed link between two artifacts whose source-kind and target-kind are constrained, so that its validity can be checked mechanically and a graph can be computed from the files alone.

Every Relation has exactly one authoritative representation, stored on its dependent (downstream) artifact and pointing at the artifact it depends on; its inverse is a derived view, never authored.

## Inclusion test

Does the link carry a defined source-kind and target-kind that a validator could check?
If it is a free "related to" with no type obligation, it is not a Relation in this sense and has no home in this corpus.

## Origin

General English (Oxford: "the way in which two or more things are connected").

The typed, direction-bearing sense is standard in data and conceptual modeling, where a relationship holds between entities of constrained types (as in the entity-relationship model) and in requirements traceability, where a trace link connects artifacts of specific kinds so the chain can be checked.
