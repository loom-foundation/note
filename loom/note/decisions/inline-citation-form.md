---
id: note:dec:2dxr3xh
name: Inline citations use the reference-link form
kind: decision
status: current
decided: 2026-06-01T10:48:33Z
---

When prose cites a specific artifact, it uses the reference-link form `[label](path){id=<id>}`, the same form as a `## Relations` entry, not a bare identifier.

Plain prose naming, with no link, remains fine for an incidental or conceptual mention that does not point at a specific artifact.

## Context

With human-readable slug identifiers, a prose citation could drop a bare id into a sentence and still read (`...the exception is note:requirement:materialization-of-inherited-intent`).

Once identifiers became opaque ([Requirement levels](requirement-levels-and-identity.md){id=note:dec:nc2yrf4}), a bare id in prose (`...the exception is note:req:k3m9p2x`) is resolvable but unreadable, and a renamed or removed target can rot a prose citation silently, as a numbered-id citation did before.

## Decision

- A prose citation that points at a specific artifact is written as a reference-link: `[the artifact's name](relative/path.md){id=note:kind:opaque}`.
  The link text is the human-readable label (which renders, reads, and may be refreshed against the target's name); the `{id=}` is the durable handle a tool resolves and checks.
- This is the same reference form already used in `## Relations`, so the corpus has one citation form everywhere rather than a separate prose style.
- A mention that does not point at a specific artifact stays plain prose; it is not forced into a link.

## Forces and trade-offs

- Readability and resolvability together: the label carries the meaning a bare opaque id lacks, while the id keeps the citation machine-resolvable and checkable, so a dangling or stale prose citation is caught rather than rotting unnoticed.
- One reference form across `## Relations` and prose; nothing new to learn or parse.
- Cost: a prose reference-link is heavier in raw text than a bare name, and its `{id=}` annotation renders literally in a vanilla Markdown viewer, the same cost already accepted for relations.

## Alternatives considered

- **A bare opaque id in prose** (`(note:req:k3m9p2x)`).
  Rejected: opaque and unreadable in a sentence, which is the very problem the "meaning in the label" principle exists to avoid.
- **A name plus a bare id in prose** (`materialization (note:req:k3m9p2x)`).
  Rejected: redundant when the sentence already names the thing, and an ad-hoc style distinct from the reference form used elsewhere.
- **A plain name with the id only in `## Relations`.**
  Kept for incidental mentions, but rejected as the rule for artifact pointers: an explanatory pointer ("the exception is X") is often not a typed structural relation, so it would carry no resolvable, checkable handle at all.

## Driven by

- groundedIn: [Artifacts are Markdown with YAML frontmatter](artifact-file-format.md){id=note:dec:pxnjmcd}
- groundedIn: [Requirement levels](requirement-levels-and-identity.md){id=note:dec:nc2yrf4}
