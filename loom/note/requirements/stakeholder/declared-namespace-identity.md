---
id: note:req:78hqr3n
name: Declared namespace identity
kind: requirement
level: stakeholder
type: functional
status: current
---

Note shall let a corpus declare its namespace in its manifest, and shall keep an opaque identifier unique within its namespace, so that an identifier is unambiguous wherever its corpus is read and two corpora that choose distinct namespaces never collide.

## Rationale

The namespace is the corpus's identity-space boundary; declaring it once, in the manifest, lets a tool or an agent know which namespace a repository mints into and check that every identifier minted there carries it.
Scoping uniqueness to the namespace, rather than to a single repository, is what lets one namespace span several repositories without an identifier meaning two things; distinct namespaces partition the identity space so independent corpora are collision-free with no coordination.

## Relations

- relieves: [Undeclared Identity-Space Boundary](../../needs/operate-corpus-across-repositories/pain-undeclared-id-space.md){id=note:pain:86y9pke}
- relieves: [Shared Namespace Collides Under Parallel Minting](../../needs/operate-corpus-across-repositories/pain-shared-namespace-collision.md){id=note:pain:ntyth85}
- decidedBy: [The multi-root corpus](../../decisions/multi-root-corpus.md){id=note:dec:0n14gqx}
