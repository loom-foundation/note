---
id: note:dec:pxnjmcd
name: Artifacts are Markdown with YAML frontmatter
kind: decision
status: current
decided: 2026-06-01T08:26:49Z
---

Every artifact is a single UTF-8 text file: a YAML frontmatter block carrying the structured metadata, followed by a Markdown body carrying the prose.
One artifact per file.

## Context

An artifact must serve two readers at once.
A person or an AI actor reads and authors its prose through ordinary file access, with no special tool; a checker reads its structured fields (identity, kind, typed relations) and validates them mechanically.

The bodies in this corpus are substantial prose, not short fields: a rationale, a job story, a set of illustrative situations.

The format has to keep prose pleasant to write and to diff while keeping metadata unambiguous to parse.

## Decision

Store each artifact as Markdown with a YAML frontmatter block, one artifact per file.

Structured metadata lives in the frontmatter, between the opening and closing `---` fences.
Everything below the closing fence is Markdown prose.

Relations are written in the body as Markdown links that carry the durable identifier as an annotation, so a single line is both navigable for a human and resolvable for a checker.

## Forces and trade-offs

- Frontmatter is a fenced, universally parsed envelope: a checker reads the metadata without parsing prose, and a renderer or editor reads the prose without parsing metadata.
  The two readers do not collide.
- Markdown is the most widely rendered plain-text prose format; every editor, host, and renderer handles it, which is what makes "any capable actor, no special tool" true in practice rather than in principle.
- One artifact per file keeps diffs small and local, ties identity to a single file, and lets a constrained actor read one artifact without loading a larger document.
- The cost accepted: two grammars in one file (YAML above the fence, Markdown below it), and a standing discipline about which facts are metadata and which are content.
  The relation-link annotation is not part of core CommonMark, so a plain renderer shows it literally; this is a known cost, pinned precisely by the format specification.

## Alternatives considered

- **A single structured-data format** (one YAML or JSON document per artifact, with prose carried as a quoted string field).
  Rejected: substantial prose held inside a data scalar is hostile to author and to review, and the diff legibility this corpus depends on is lost.
  The structured-only form earns its place only where bodies are one short field, which is not this corpus.
- **Unstructured Markdown with parsing conventions** (no frontmatter; metadata and relations inferred from headings and prose).
  Rejected: the structured fields then have to be recovered from prose by convention, which is brittle and gives up the cheap, robust mechanical checking that typed identity and typed relations require.
- **A different frontmatter dialect** (for example TOML).
  Rejected: it buys marginally fewer parsing foot-guns at the cost of far less ubiquitous tool support, which trades directly against the no-special-tool goal.

## Driven by

- groundedIn: [File-native capture](../requirements/system/file-native-capture.md){id=note:req:mgdg9q0}
- groundedIn: [Universal participation](../requirements/stakeholder/universal-participation.md){id=note:req:j4kecn7}
- groundedIn: [Durable, portable intent](../requirements/stakeholder/durable-portable-intent.md){id=note:req:93kczqj}
- groundedIn: [Checkable well-formedness and identity](../requirements/system/checkable-well-formedness.md){id=note:req:sp8g0my}
- groundedIn: [Inspectable traceability](../requirements/stakeholder/inspectable-traceability.md){id=note:req:sg0npmv}
