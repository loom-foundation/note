---
id: note:pain:ntyth85
name: Shared Namespace Collides Under Parallel Minting
kind: pain
subkind: risk
persona: "[Organization or Platform Owner](../../personas/organization-owner.md){id=note:persona:6ek4j8b}"
status: current
---

When sub-systems of one system share a single namespace across their repositories, two contributors minting offline in different repositories can draw the same identifier, a collision that surfaces only when the workspace is assembled, by which time both ids are committed and neither is clearly the original.

## Relations

- partOf: [Operate one corpus across many repositories](../operate-corpus-across-repositories.md){id=note:need:03gs33j}
