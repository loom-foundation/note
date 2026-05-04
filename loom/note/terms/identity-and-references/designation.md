---
id: note:term:17dkrj5
name: Designation
kind: term
status: current
---

A name or alias by which a concept is referred to in a corpus.
A concept may have one or more designations; replacing one designation with a synonym, an abbreviation, or a preferred term leaves the concept itself, and its Durable Identifier, unchanged.
The `name` field holds the primary designation; the `aliases` list holds additional designations of the same concept.

Designation is the concept behind the `name` and `aliases` fields: it is not a field name, it is the semantic role those fields play.
A reference's visible text is always a designation of the target concept; when a concept is renamed, the reference text refreshes, and because the Durable Identifier is the citation, no link breaks.

## Inclusion test

Is it a label by which a concept is looked up and displayed, separate from the concept's identity and stable across a rename?
If it is the stable handle that survives a rename (the `id`), it is a Durable Identifier, not a Designation.
If it is part of the concept's substance (a field value that changes the concept's meaning), it is content, not a Designation.

## Relations

- *relates to* [Durable Identifier](durable-identifier.md){id=note:term:24hmw8y} (a Designation is the human-facing label the Durable Identifier anchors; the identifier survives every change to the Designation)

## Origin

Oxford: "designation: the action of choosing a name or title for something; a name, description, or title, typically one that is officially bestowed".

In ISO 704 (Principles and Methods of Terminology) and ISO 1087 (Terminology Work), the foundational distinction is between a concept and its designations: a concept is a unit of knowledge, and a designation is any linguistic expression (a word, a phrase, an abbreviation) by which the concept is referred to.
A concept has one or more designations; two terms denoting the same concept are synonyms; retiring one designation and adopting another is a renaming, not a change of concept.
The Note usage follows this lineage directly: the `name` and `aliases` fields each hold a designation; the opaque id holds the concept's identity; and a rename is a change of designation, never a change of concept or a break of reference.
