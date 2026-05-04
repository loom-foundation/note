---
id: note:req:w4k7n2h
name: Legible system boundary
kind: requirement
level: stakeholder
type: functional
status: current
---

The boundary of the system whose intent is captured shall be explicit and legible: what lies inside it, what lies outside it, and what crosses it shall be determinable by inspection, so that every Need and Requirement is interpreted within a stated boundary rather than an assumed one.

## Source

See the Source of [System boundary knowledge](../../needs/know-the-system-boundary.md){id=note:need:c7k2n9w}.

## Rationale

An obligation is interpretable only against the system it constrains;
left implicit, the boundary is supplied differently by each reader and each agent, and scope drifts without anyone deciding it should.

Stating the boundary explicitly fixes one reading for everyone and makes what is out of scope a deliberate, visible choice rather than an omission.

This is a problem-space property the method must guarantee;
whether the boundary is captured as an artifact of its own, in what form, and how it composes across scopes are left to the system requirements and to specification, so the obligation commits to no mechanism.

## Relations

- addresses: [System boundary knowledge](../../needs/know-the-system-boundary.md){id=note:need:c7k2n9w}
