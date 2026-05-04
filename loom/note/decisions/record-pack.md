---
id: note:dec:hjv67df
name: The record side-car pack
kind: decision
status: current
decided: 2026-06-19T00:00:00Z
---

The method defines a **record** pack: an opt-in built-in package that adds one kind, record (`rec`), a Markdown side-car that brings an opaque external file into the model with a durable identity, its provenance, typed relations, and an integrity-checked pointer to the file it stands for.
Native authoring stays the default; the record kind is the deliberate exception, for the genuine binary an organization cannot or will not rewrite as intent yet must still cite, crosswalk, and hold to an approver and a date.

## Context

Intent in Note is plain Markdown on purpose: inspectable, diffable, cascadable, owned outright.
The first answer to "we have a policy in Word" is therefore to author it as a native policy, not to wrap the Word file, and the pack does not soften that.

But an organization holds documents whose authoritative form is opaque and fixed: a signed PDF, an executed contract, an exported attestation, a regulator's letter, a vendor's certification.
These cannot be made native without losing the very signatures and seals that make them evidence, and they still belong in the graph: an obligation crosswalks to one, a procedure cites one, an auditor reads the approver and the effective date off one.
A reference cannot answer this, because a reference is a pointer carried *by* an artifact and is editable as prose; it is not a node that can be referenced by id, hashed, and related to by many.
The record kind is that node: the single, citable, tamper-evident stand-in for the opaque file, so the file participates while its bytes stay outside.

## Decision

- **A record pack, opt-in, one kind.**
  The pack adds record, with kind-segment `rec`, enabled by naming `record` in the manifest `packs`.
  It is separate from the governance pack because a record is general: any opaque artifact may need it, not only a governing one.

- **A side-car beside its payload.**
  A record is authored as `<payload-name>.<ext>.md`, beside the file it describes, so the payload's own extension stays visible and the two travel together.

- **The payload is named, typed, sized, and hashed.**
  A record carries a `payload` block: the relative `path` to the file, its `media_type`, its `size`, and a content `hash` (algorithm and value).
  The hash is the load-bearing field: it is the integrity the opaque file cannot carry itself, and the means by which a changed payload is detected.

- **Staleness is the changed payload.**
  When the file at `path` no longer hashes to the recorded value, the record is stale, surfaced as the substrate surfaces a changed reference: the binary's tamper-or-change signal, computed from the files alone.

- **A record participates by relation.**
  A record may be the target of `implements`, so a procedure or a standard may carry out a policy held only as a signed PDF; it may carry a crosswalk to an external control; and where it stands in for a governing instrument it carries the same `approver` and `effective_date` a native policy would.

- **The payload stays opaque, and the record says so.**
  A record buys identity, provenance, integrity, and graph membership; it does not buy inspectable intent.
  The payload is not diffed, not cascaded, and not read as obligations: the record is a governance and traceability bridge, never a way to pass an opaque file off as native intent.

## Forces and trade-offs

A blind adversarial pass tested whether a record is a kind at all or a citation with two extra fields, and it survives on a distinction a citation structurally cannot reach: a citation is a per-artifact, mutable pointer, while a record is a shared node, referenced by id and tamper-evident by hash, that many obligations cite once instead of each restating a path and a date that then drift.
Its lifecycle differs in kind: a citation in prose is freely edited, whereas a record's hash must not change, and a change to it is a detectable integrity event rather than an edit.

The pattern is not invented here.
It is the shape NIST OSCAL fixes in its back-matter resource, an external pointer carried as `rlink` with an optional `hash` for verification and change detection, deliberately distinct from a plain link that "makes no provision for a hash."
The same shape recurs across content-addressed side-cars, from XMP companions named by appended extension to the pointer files of DVC and Git-LFS, each pairing a path with a digest so a changed payload is caught.

The tripwire the pass surfaced is kept as the inclusion test's guard: a record cited by exactly one artifact and verified by no consumer is an `authority` path externalized for no gain, and collapses back into the citing artifact's own reference.

The pack is opt-in by Proportionality: a corpus with no opaque documents to govern carries nothing.

## Alternatives considered

- **Use a reference, an `authority` path, or a citation.**
  Rejected as the general home: each is a pointer from one artifact and cannot be referenced by id, hashed, or related to as a node; the single-source, many-citers case is exactly what a kind, not a pointer, serves.

- **Embed the binary in the corpus as base64.**
  Rejected: it bloats every clone with bytes no reader can diff, and the payload stays as opaque embedded as referenced; a hashed pointer keeps the corpus plain text and the file where it lives.

- **Fold the record kind into the governance pack.**
  Rejected: a record is not a governing instrument but a bridge for any opaque artifact, so binding it to governance would deny it to every other use and tax every governance adopter with a kind many do not need.

## Frameworks surveyed

The record kind draws on records-management and content-integrity practice, not on invention.

- ISO 15489: the document-versus-record distinction, and the metadata an authoritative record must carry, authorship, date, integrity, to be authentic, reliable, and usable.
- NIST OSCAL back-matter: the `resource` with an `rlink` and one or more `hash` values (SHA-256 and above), the proven model for a verifiable pointer to an external document.
- Content-addressed side-car patterns: XMP companions, DVC and Git-LFS pointer files, Metalink, and BagIt manifests, each binding a payload to a digest and using a size mismatch as a fast staleness gate.
- Records-management timestamping practice: a committed file's history is not an effective date, because version-control timestamps are mutable and record transaction time rather than the business time a document took force; the effective date is therefore an authored field, not a derived one.

## Driven by

- groundedIn: [Kind-agnostic substrate and kind packages](substrate-and-kind-packages.md){id=note:dec:w4awceq}
- groundedIn: [Detectable staleness](../requirements/system/detectable-staleness.md){id=note:req:46xm59a}
- groundedIn: [Representation, not enforcement](../requirements/system/representation-not-enforcement.md){id=note:req:agncpcc}
- groundedIn: [Single Source of Truth](../principles/single-source-of-truth.md){id=note:principle:8691937}
- groundedIn: [Proportionality](../principles/proportionality.md){id=note:principle:es0vhzn}
- groundedIn: [Compute and Report](../principles/compute-and-report.md){id=note:principle:6e7f28k}
- groundedIn: [Earned Substance](../principles/earned-substance.md){id=note:principle:yecemfe}
