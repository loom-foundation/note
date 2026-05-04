---
id: note:req:mx4w8k3
name: Intent promotable to a broader scope
kind: requirement
level: stakeholder
type: functional
status: current
---

Those responsible for intent shall be able to re-home an artifact from its scope to a broader scope, so that the scopes beneath the new home inherit it, with every inbound reference kept whole or every break surfaced, and with the artifact's prior identity recorded so the move is traceable.

## Source

See the Source of [Promote intent to a broader scope](../../needs/promote-intent-to-broader-scope.md){id=note:need:hq7k4w2}.

## Rationale

Promotion is reference-safe evolution along the scope axis: it moves intent to the scope that owns it and lets the cascade carry it down, the inverse of materialization, which captures inherited intent down into a scope and severs it.

Because the move changes the artifact's owning scope, and the namespace denotes that scope, promotion is the case where identity is deliberately re-minted rather than preserved;
recording the prior identity keeps the lineage legible.

How the new identity is minted, how references are re-pointed, and who may approve the move are the system requirement, the tool, and the Orchestrating Authority's concern.

## Relations

- addresses: [Promote intent to a broader scope](../../needs/promote-intent-to-broader-scope.md){id=note:need:hq7k4w2}
