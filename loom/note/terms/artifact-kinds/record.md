---
id: note:term:nc9gjs9
name: Record
kind: term
status: current
---

A side-car artifact standing in for an opaque external file: a node carrying the file's durable identity, its provenance, and an integrity-checked pointer to it (a path and a content hash), so the file participates in the graph while its bytes stay outside the corpus.

A Record is a shared, tamper-evident node many artifacts cite once, distinct from a reference, which is a single artifact's editable pointer.

## Inclusion test

Is it a stand-in for an opaque file that is referenced by id, made tamper-evident by a content hash, and cited or implemented by more than one artifact?

If it is a pointer carried by one artifact to a document that it alone cites, it is a reference or a specification's authority path, not a Record; if its content is authored as inspectable intent rather than held as an opaque payload, it is a native artifact of its own kind, not a Record.

## Relations

- *relates to* [Specification](specification.md){id=note:term:9xd6ejd} (a payload pointer with an integrity hash, the counterpart for an opaque file of a specification's external authority path)

## Origin

General English (Oxford: "a thing constituting a piece of evidence about the past, especially an account kept in writing or some other permanent form").

The evidential sense is ISO 15489's, where a record is information kept as evidence, carrying the metadata, authorship, date, and integrity, that makes it authentic. The verifiable-pointer shape, a path paired with a cryptographic digest, is NIST OSCAL's back-matter resource link and the content-addressed side-car pattern of XMP, DVC, and Git-LFS.
