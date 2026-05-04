---
id: note:need:03gs33j
name: Operate one corpus across many repositories
kind: need
persona:
  - "[Organization or Platform Owner](../personas/organization-owner.md){id=note:persona:6ek4j8b}"
  - "[Forking or Spun-Out Team](../personas/forking-team.md){id=note:persona:aqx1gv3}"
  - "[Reviewer or Auditor](../personas/reviewer-auditor.md){id=note:persona:9jz2a3w}"
status: current
validation: inferred
---

When an Organization or Platform Owner keeps its intent in more than one repository, for real reasons of ownership, team boundary, or release cadence, it wants that intent to still function as one connected body, so the corpus does not fragment at repository boundaries.

## Illustrative situations

These shaped the need and are kept here, in the problem space.

They are inferred from common organizational patterns, not observed by us.

1. Layered ownership.
   An organization keeps its cross-cutting, org-level intent in one repository and its per-product intent in others, because each is owned by a different team on its own release cadence.
   The per-product intent must still depend on, and inherit from, the org-level intent across the repository boundary.
2. A reference across the edge.
   Intent that satisfies an obligation lives in one repository while the obligation it satisfies lives in another;
   the link between them must resolve so the trace stays whole, rather than dead-ending at the repository edge.
3. Local repositories, no service.
   Two repositories cloned side by side on one machine reference and inherit from each other by their relative path on disk, with no remote host involved.
   A Git host is one way to locate another repository, not a precondition;
   the method requires no online service.

## Source

Multi-repository organizations are real and external.

The need to keep Note intent connected across them is inferred, since the method does not yet exist to have been observed operating this way.

The federation of a corpus across repositories is anticipated in the design discussion and noted as future work in the Note paper.

This need is distinct from [State a shared obligation once](state-obligation-once.md){id=note:need:257yf29}, which concerns single-source via the scope graph, an obligation stated once high and inherited by the units below; this need concerns federation across repository boundaries, resolving references across separately-owned repositories. It is also distinct from [Trust and drift visibility](trust-intent-is-honored.md){id=note:need:46tkxcn}: both serve a Reviewer or Auditor confirming obligation coverage, but that one does so within a single corpus while this need does so across repository boundaries.
