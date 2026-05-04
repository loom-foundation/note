---
id: note:term:3yted77
name: Materialization
kind: term
status: current
---

The capture of inherited intent as a local, standalone artifact: a copy frozen at a chosen version, with the live link to its source severed and provenance (the source, the version, the resolved commit, and the date of capture) recorded, so the corpus no longer depends on the upstream repository.

A faithful frozen mirror keeps the source's durable identifier; a copy taken over to be evolved is re-homed to the corpus's own namespace, which is a fork rather than a mirror.

## Inclusion test

Was the artifact produced by freezing inherited intent and severing its live link, with provenance recorded, rather than left as a live Reference that still resolves to its source, or authored directly in this corpus?
If so, it is a Materialization.

## Relations

- *contrasts with* [Reference](../identity-and-references/reference.md){id=note:term:evt67dx} (a live link that resolves to its source; Materialization severs that link and depends on no external repository thereafter)

## Origin

A coinage of this corpus, from the general-English "materialize" (Oxford: "become actual or real"): a remote, referenced dependency is made into a concrete local artifact that stands on its own.

The lineage is the database sense of a materialized view, a query result stored rather than recomputed on each read, narrowed here to a one-time freeze with provenance rather than a maintained cache.
