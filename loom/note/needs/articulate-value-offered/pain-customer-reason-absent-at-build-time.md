---
id: note:pain:k3m9x2v
name: Commitment Does Not Carry Its Customer Reason
kind: pain
subkind: obstacle
persona:
  - "[Implementer](../../personas/implementer.md){id=note:persona:s4v9hn2}"
  - "[Product Owner](../../personas/product-owner.md){id=note:persona:pd8w3kq}"
status: current
---

A commitment, as written, does not carry the customer problem it answers, so a reader cannot recover from it whose problem it serves or why it matters.
An Implementer about to build it cannot tell which customer problem it addresses, so when the specification runs out mid-implementation they have no basis for choosing correctly between interpretations.

## Illustrative situations

1. **Implementer mid-build.**
   An Implementer reads a commitment they are about to build, the specification leaves a choice open, and nothing in the commitment names the customer problem it serves, so they have no ground for judging which interpretation actually solves it.

2. **Product Owner reviewing their own commitment.**
   A Product Owner looks back at a commitment they authored and finds it reads as a technical instruction with no customer story attached, so neither the team building it nor a reviewer reading it can tell whose problem it answers or why it matters.

## Relations

- partOf: [Articulate value offered](../articulate-value-offered.md){id=note:need:9w2k4pt}
- framedBy: [Carry the Customer Reason With Each Commitment](job-anchor-requirement-to-value.md){id=note:job:7et7eba}
