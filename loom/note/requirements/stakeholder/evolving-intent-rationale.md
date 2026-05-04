---
id: note:req:6swdxb0
name: Evolving intent with rationale
kind: requirement
level: stakeholder
type: functional
status: current
---

When intent changes, including changes discovered during implementation rather than declared up front, the method shall make it possible to capture the change and the rationale and trade-offs that drove it alongside the affected artifacts, so that, where a team chooses to capture it, why an artifact changed remains recoverable.

Capturing rationale shall not be mandatory;
whether a project does so is governed by its adopted profile (see [Progressive, right-sized adoption](progressive-adoption.md){id=note:req:srzdd07}).

## Source

See the Source of [Remember why intent changed](../../needs/remember-why-intent-changed.md){id=note:need:rwg1y77}.

## Rationale

For complex problems intent is discovered iteratively rather than perfectly articulated at the start.

Recording the forces behind a change lets future actors tell a deliberate change from drift;
but a team prototyping throwaway work should be able to skip it and adopt it later as the system matures.

The method's job is to provide the structure, not to compel its use.

## Relations

- addresses: [Remember why intent changed](../../needs/remember-why-intent-changed.md){id=note:need:rwg1y77}
- delivers: [Rationale in the Same Place](../../offerings/decisions-on-the-record/gc-rationale-in-the-same-place.md){id=note:gc:hvynveb}
- delivers: [Change Is a Deliberate Retirement](../../offerings/decisions-on-the-record/pr-change-is-a-deliberate-retirement.md){id=note:pr:dxyvbka}
- delivers: [Settled Questions Stay Settled](../../offerings/decisions-on-the-record/pr-settled-questions-stay-settled.md){id=note:pr:ng6vyzz}
- delivers: [Trade-offs on the Record](../../offerings/decisions-on-the-record/pr-trade-offs-on-the-record.md){id=note:pr:2btamga}
