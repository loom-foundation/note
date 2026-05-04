---
id: note:ver:k8w3m4n
name: Identity and reference integrity
kind: verification
status: current
method: analysis
---

This verification confirms that a corpus conforms to the identity, designation, and relation-link rules the substrate specification fixes: every artifact carries a well-formed, unique durable id whose kind-segment agrees with its `kind` field; every inline citation resolves by both path and id; every relation is authored once on the dependent end with no authored inverse; every hierarchical edge chain is acyclic; and every designation is unique within its namespace at minting, with any ambiguity in an effective set at a reading scope surfaced rather than silently resolved.

The check is a static pass over the committed files; it computes and reports findings only.
The verdict belongs to the Orchestrating Authority.

## Criteria

A pass requires, across every artifact in the corpus, that:

- each `id` is well-formed: three colon-separated segments where the opaque is a Crockford Base32 string of the configured length (defaulting to seven characters), drawn from the permissible alphabet (`0`-`9`, `A`-`Z` minus `I`, `L`, `O`, `U`, case-insensitive);
- no `id` appears on more than one artifact (global uniqueness);
- the id's kind-segment agrees with the artifact's `kind` field through the enabled pack's declared kind-segment mapping (an abbreviated segment such as `req` for `requirement` is agreement; a segment outside the mapping is a failure), as the substrate requires the `kind` field to be authoritative;
- no slug id remains anywhere in the corpus (all opaque segments conform to the Crockford Base32 grammar; a readable slug in the opaque position is a failure);
- each inline `]{id=...}` citation is well-formed: the linked relative path exists, and the artifact at that path carries the exact id the citation names (a dangling path, a path-to-id mismatch, or a malformed citation token is a failure);
- each entry in a reference-bearing frontmatter field (`persona`, `supersedes`, `superseded_by`) is a well-formed citation in the standard citation form (name label, relative path, id); the relative path resolves and the artifact at that path carries the exact id the citation names; a bare id with no label and path is a failure;
- each relation is authored once, on the dependent end: no inverse relation is directly authored in a file (an authored edge that duplicates the inverse of another authored edge on the same pair of artifacts is a failure);
- the hierarchical edges are acyclic: no artifact reaches itself by following `derivedFrom`, `partOf`, `groundedIn`, `amends`, or the hierarchical term relations (`is a`, `is a value of`, `is part of`); a cycle is a failure;
- each `name` and each entry in `aliases` is unique within its namespace at minting time; a duplicate designation within the namespace is a failure;
- any designation that is ambiguous in the effective set of terms and personas at a reading scope (which can arise from namespace inheritance) is surfaced in the report as a cascade tie, with the sanctioned resolution being the cascade's replace operator; ambiguity here is a warning, not a hard failure, but it is never silently ignored.

A pass is zero hard failures across the whole corpus; warnings are reported but do not fail the run.

## Procedure

By analysis.
A static reader traverses every committed Markdown file in the corpus.

For each file it:
1. Parses the frontmatter and extracts `id`, `kind`, `name`, and `aliases`.
2. Validates the id's structure against the three-segment grammar and the Crockford Base32 alphabet, and checks that the kind-segment matches the `kind` field through the enabled pack's declared kind-segment mapping.
3. Accumulates all ids into a global set and records any collision.
4. Accumulates all designations (`name` values and alias entries) per namespace and records any duplicate within a namespace.
5. Scans the Markdown body and the reference-bearing frontmatter fields (`persona`, `supersedes`, `superseded_by`) for every `]{id=...}` citation token; for each, resolves the relative link path against the file's own location (not the caller's working directory) and reads the `id` from the target file's frontmatter, flagging any path-not-found, id-mismatch, or bare reference-field entry.
6. Records every authored relation verb and its direction; after the full pass, detects any authored edge that mirrors an authored inverse on the other artifact.
7. Builds the directed graph of the hierarchical edges and searches it for cycles, recording any cycle found with the chain of artifacts that closes it.

Citations inside inline code spans or fenced code blocks, where a grammar-defining file is illustrating the citation form itself, are documentation and are excluded from resolution checks.

Once the traversal is complete, the reader performs a second pass to compute designation ambiguity against the effective scope graph, reporting any name or alias that resolves to more than one artifact within a reading scope.

The reader only reads; it executes nothing and writes nothing, so the check is reproducible by anyone with the repository.

## Evidence

A run produces a report: the count of artifacts and citations checked, the list of any hard failures (id collisions, malformed ids, kind-segment mismatches, slug ids, dangling paths, path-to-id mismatches, bare reference-field entries, duplicate designations, authored inverses), and the list of any warnings (designation ambiguities in effective sets).

The report is produced per run and kept with that run by the Orchestrating Authority; it is not stored in this artifact.

## Relations

- verifies: [The substrate](../specifications/note/substrate.md){id=note:spec:tkhd63e}
- verifies: [Checkable well-formedness and identity](../requirements/system/checkable-well-formedness.md){id=note:req:sp8g0my}
- verifies: [Stable, location-independent identity](../requirements/system/stable-identity.md){id=note:req:sfmkwmm}
- verifies: [Typed, checkable relations](../requirements/system/typed-relations.md){id=note:req:yb1xez2}
- verifies: [Single authoritative representation per relationship](../requirements/system/single-authoritative-relation.md){id=note:req:s5fh0e8}
- verifies: [Stated-once, typed, checkable term-relations](../requirements/system/typed-term-relations.md){id=note:req:n8w4k6m}
- verifies: [Single authoritative term-relation](../requirements/system/single-authoritative-term-relation.md){id=note:req:k4w7n9t}
- verifies: [Acyclic core relation graph](../requirements/system/acyclic-relation-graph.md){id=note:req:r8h4g6t}
