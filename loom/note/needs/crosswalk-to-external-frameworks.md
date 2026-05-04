---
id: note:need:5mmrydr
name: Crosswalk intent to the frameworks it answers to
kind: need
persona:
  - "[Organization or Platform Owner](../personas/organization-owner.md){id=note:persona:6ek4j8b}"
  - "[Reviewer or Auditor](../personas/reviewer-auditor.md){id=note:persona:9jz2a3w}"
  - "[Systems Engineer](../personas/systems-engineer.md){id=note:persona:25fdjrx}"
  - "[Adopter](../personas/adopter.md){id=note:persona:n66rj1d}"
status: current
validation: inferred
---

When an organization's intent must answer to an external control framework, a security standard, a regulatory catalog, or a customer's control set, everyone accountable for that intent, the Organization or Platform Owner who answers for coverage, the Systems Engineer who fits the framework to a system, the Reviewer or Auditor who must show it is met, and the Adopter bringing the framework in, wants the correspondence between their own obligations and that framework's controls captured as part of the intent and kept with the obligations it maps, so that showing coverage is a reading of their own record rather than a separate mapping that drifts the moment either side changes.

## Source

The Requirements Traceability Matrix and control-mapping practice of governance, risk, and compliance work, where each obligation is linked to the control that satisfies it, its status, and its owner; and the machine-readable control-mapping models of OSCAL (the `component-definition` and `mapping` models, the latter carrying the relationship types `equivalent`, `subset-of`, and `intersects-with`).

External to this corpus and not derived from it.

This need is distinct from [State a shared obligation once](state-obligation-once.md){id=note:need:257yf29}, which concerns an organization's own obligations holding across its own units, and from [Intent that outlives its tooling](intent-outlives-tooling.md){id=note:need:jwvn9b7}, which concerns intent surviving a tool: this need concerns the correspondence between the organization's obligations and a framework owned by someone else.

## Illustrative situations

1. A platform adopting a security standard maps each of its own controls to the standard's catalog and must show, on demand, which of the standard's controls are covered and which are not.
2. A regulated system answers to two catalogs at once, and one of its controls satisfies a control in each; the correspondence to both must be recorded against that one obligation.
3. A system that must comply with a standard drops a control that does not apply to it, and the exception, with its reason, must be as legible as the controls it does honor.
