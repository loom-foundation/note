---
id: note:spec:asdh5mv
name: The record pack
kind: specification
status: current
authority: []
---

This specification fixes the record pack: an opt-in built-in kind package with a single kind, record, a Markdown side-car that brings an opaque external file into the model.
It declares the record kind, its id kind-segment, the per-kind frontmatter it adds beyond the common envelope, its body shape, and the relation endpoint row it contributes.

It extends [The substrate](substrate.md){id=note:spec:tkhd63e}, whose rules are not restated here; this specification supplies only what the record pack adds.
The pack is enabled by naming `record` in the manifest `packs`.

## The record kind

| Kind | Kind-segment | Role |
|---|---|---|
| record | `rec` | A side-car standing in for an opaque external file, carrying its identity, provenance, and an integrity-checked pointer to it. |

The record carries the uniform opaque id; the file it stands for carries none, and is reached through the `payload` pointer below.

## Per-kind frontmatter

| Kind | Field | Required | Value |
|---|---|---|---|
| record | `payload` | required | A mapping describing the file the record stands for: `path`, the repository-relative path to it; `media_type`, its IANA media type; `size`, its length in bytes; and `hash`, a mapping of `algorithm` (one of `SHA-256`, `SHA-384`, `SHA-512`, or a stronger SHA-3 variant) and `value` (the lowercase hexadecimal digest). The hash is the integrity the opaque file cannot carry itself. |
| record | `approver` | optional | As a policy's `approver`, where the record stands in for a signed governing instrument: a persona citation of the approving role. |
| record | `approver_name` | optional | A literal name of the approver, where the person is recorded beside the role. |
| record | `effective_date` | optional | An RFC 3339 date at which the instrument the record stands for takes force. |
| record | `review_due` | optional | An RFC 3339 date by which it is next reviewed. |

The side-car is placed beside its payload and named `<payload-name>.<ext>.md`, so the payload's own extension stays visible and the two travel together; placement is a convenience, and the id, not the location, is authoritative.

## Body structure

| Section | Req/Opt | Content |
|---|---|---|
| *(lead)* | required | What the opaque document is, and why it is held in the corpus: the evidence, instrument, or attestation it carries, in one statement. |
| `## Relations` | optional | The record's typed edges: it may be the target of `implements`, so a procedure or standard carries out a policy held only as a signed file; it may `enacts` a principle and carry a crosswalk where it stands in for a governing instrument. A record with only inbound edges and no consumer that checks its hash is an externalized `authority` path, not a record, and belongs back in the citing artifact's reference. |

## Verb endpoint rows

The pack contributes one endpoint row, extending the governance verb `implements` to admit a record as a target.

| Verb | Authored on | To | Inverse |
|---|---|---|---|
| `implements` | standard, procedure, requirement | record | `implementedBy` |

A record stands in for the policy or standard it carries, so a procedure or a standard may `implements` it exactly as it would a native instrument; the inverse `implementedBy` lets the opaque instrument read off what carries it out.
Where the compliance pack is enabled, a record may carry a crosswalk to an external control, so an obligation held as an opaque file maps to the framework it answers like any other.

## Integrity and staleness

The recorded `hash` is the record's load-bearing field.
A consumer confirms the record by hashing the file at `payload.path` and comparing the result to `hash.value`; a mismatch means the payload has changed since the record was sealed, and the record is stale.
This is the binary's counterpart to the substrate's detection of a changed reference: the change is computable from the files alone, without reading the opaque payload, and the record never holds the verdict on whether the change was authorized, which belongs to the Orchestrating Authority.

## Rationale

A record earns a kind, rather than reducing to a citation, on one distinction: a citation is a per-artifact, editable pointer, while a record is a shared node, referenced by id and made tamper-evident by hash, that many artifacts cite once instead of each restating a path and a date that drift.
Holding the kind in its own pack, separate from governance, keeps it general: any opaque artifact may need a record, not only a governing one, and a corpus with no such files carries nothing.

The pointer shape, a path paired with a digest and a media type, is the one NIST OSCAL fixes in its back-matter `rlink` and that content-addressed side-cars share; adopting it rather than inventing one keeps a record verifiable by any tool that can hash a file.

## Relations

- satisfies: [Declarable kind packages](../../requirements/system/declarable-kind-packages.md){id=note:req:ekfkzzt}
- satisfies: [Detectable staleness](../../requirements/system/detectable-staleness.md){id=note:req:46xm59a}
- decidedBy: [The record side-car pack](../../decisions/record-pack.md){id=note:dec:hjv67df}
