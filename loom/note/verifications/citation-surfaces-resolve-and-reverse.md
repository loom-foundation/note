---
id: note:ver:c1t3s9m
name: Citation surfaces resolve and reverse
kind: verification
status: current
method: analysis
---

This verification confirms the two out-of-corpus citation surfaces: an `@intent` code comment and a Title-Case commit trailer are each recognizable without parsing the host language or the prose, their durable ids resolve into the corpus, only the id is held load-bearing, and the reverse view, which files and commits cite a given artifact, is computable as a derived set.
The check is a static pass over the repository's files and, where present, its commit history; it computes and reports findings only, and the verdict belongs to the Orchestrating Authority.

## Criteria

A pass requires that:

- every citation behind the fixed `@intent` marker parses to a durable id that resolves to an artifact, with the verb key and label read as advisory only, an unknown key or implausible target kind raised as a non-blocking warning and never a failure;
- every Title-Case citation trailer in a sampled commit range parses to a durable id that resolves, with the id appearing in the trailer block and not required in subject or prose, and the imperative state-change family absent;
- no check treats a key or label as load-bearing: a drifted label changes no outcome, and only an unresolvable id is a failure;
- for a sampled set of artifacts, the citing-units view (the files and commits carrying each artifact's id) is computable by inspection and complete against a direct search for the id.

A pass is zero unresolvable ids across both surfaces; where history is absent the trailer criterion honestly reports can't-tell.

## Procedure

By analysis.
A static reader greps the repository for the `@intent` marker, parses each citation, and resolves each id against the corpus; where git history is present it walks a commit range, extracts trailer-block citations, and resolves them the same way.
It then inverts the collected citations into a per-artifact citing-units set and cross-checks a sample against a plain-text search for the same ids.
The reader only reads; it executes nothing, so the check is reproducible by anyone with the repository.

## Evidence

A run produces a report: the citations found per surface, each resolution, the advisory warnings, and the sampled reverse views with their cross-check.
The report is kept with the run by the Orchestrating Authority; it is not stored in this artifact.

## Relations

- verifies: [In-code citation of intent](../requirements/system/in-code-citation-of-intent.md){id=note:req:cffvvdz}
- verifies: [Commit-message citation of intent](../requirements/system/commit-message-citation-of-intent.md){id=note:req:cm7vq3x}
- verifies: [Implementation traceable to intent](../requirements/stakeholder/implementation-traceable-to-intent.md){id=note:req:m520064}
- verifies: [Computable citing units of an artifact](../requirements/system/computable-citing-units.md){id=note:req:p2w8j5q}
