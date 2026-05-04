---
id: note:term:g6t22j7
name: Artifact
kind: term
status: current
---

A single file that captures one unit of intent: a YAML frontmatter block carrying its Durable Identifier, Kind, and metadata, followed by a Markdown body.

One artifact per file; its Kind fixes the body shape it takes and the relations it may carry, and it is the unit that is identified, referenced, related, scoped, and versioned.
The note is the whole woven body of intent at a scope; an Artifact is a unit of the note (the note layer holds the note, and each Artifact in it is one piece of that whole).

## Inclusion test

Is it a single self-contained file with a durable id and a kind, capturing a unit of intent that can be referenced and related to others?
If so, it is an Artifact; the corpus as a whole, a directory, or a group of files is not, and the manifest and a group README, which carry no id or kind, are not Artifacts.

## Relations

- *is part of* [Note](note.md){id=note:term:6yb8hnm}
- *carries* [Kind](kind.md){id=note:term:1vm1yqf}
- *carries* [Status](../lifecycle/status.md){id=note:term:xcen4v2}

## Origin

Oxford: "an object made by a human being, typically of cultural or historical interest", narrowed to a made object of the corpus: a file that captures intent.

The docs-as-code and build-artifact traditions use "artifact" for a discrete, versioned, addressable unit a process produces and consumes, which is the sense here.
