---
id: note:req:93kczqj
name: Durable, portable intent
kind: requirement
level: stakeholder
type: non-functional
status: current
---

The organization's engineering intent and design shall be captured as durable artifacts that remain readable and usable independently of any specific tool or vendor, for as long as the systems they describe remain in service.

## Source

Critique of tool lock-in; see the Source of [Intent that outlives its tooling](../../needs/intent-outlives-tooling.md){id=note:need:jwvn9b7}.

## Rationale

Intent is a long-lived asset.

Held inside a proprietary store, it is lost when the tool is deprecated, replaced, or priced out of reach.

Stating durability and portability as a quality of the artifacts, rather than naming a format, keeps the obligation independent of any one mechanism.

## Relations

- addresses: [Intent that outlives its tooling](../../needs/intent-outlives-tooling.md){id=note:need:jwvn9b7}
- delivers: [Read It Without the Tool That Wrote It](../../offerings/intent-you-own/gc-read-without-the-original-tool.md){id=note:gc:7ad8zkg}
- delivers: [Migrations Without Loss](../../offerings/intent-you-own/pr-migrations-without-loss.md){id=note:pr:qat356q}
- delivers: [Plain-Text Substrate](../../offerings/intent-you-own/pr-plain-text-substrate.md){id=note:pr:xzpv4p0}
