---
id: <namespace>:spec:<opaque>
name: <Name>
kind: specification
status: draft
authority:
  - contracts/authz/<service>.fga
---

This specification governs what subjects may perform which operations on which resources, and under what conditions, within <Service>.

## Authority

The governing contract is an OpenFGA model (DSL schema 1.1) at the path listed in `authority`.
It expresses all relation types, computed permissions, and resource-scoped grants as a machine-verifiable graph.
Where this document and the OpenFGA model diverge, the model governs.
An implementation's conformance to the model is a separate Verification; it is not established here.

## Authorization matrix

Projects that define a bounded role set alongside or instead of the relation schema record it here.
Each resource gets its own subsection; omit this section entirely if the OpenFGA model is the sole authority.

### Resource: <ResourceName>

<!-- Repeat this block for each resource type. -->

| | <operation-1> | <operation-2> | <operation-n> |
|---|---|---|---|
| <RoleA> | yes | no | own |
| <RoleB> | yes | yes | yes |

Cell values are `yes` (any instance), `no` (denied), `own` (owned instances only), or `—` (not applicable).

**Ownership:** <Predicate defining what "own" means for this resource, e.g. "a User owns a Document iff Document.created_by = User.id">
(Required whenever any cell carries `own`; omit the heading if no `own` cells appear.)

**Conditions:** <ABAC predicates, tenancy boundaries, time-bounded grants, and OAuth-scope constraints; anchor each bullet to the role and operation it qualifies>
(Omit the heading if no conditions apply.)

## Impersonation and delegation

State which roles may act as which subjects, the scope the impersonator inherits, and how the audit trail records the act.
State `N/A` if neither impersonation nor delegation is supported.
The authentication mechanism for impersonation is covered in the authn specification; this section covers authorization decisions only.

## Rationale

Include a rationale entry only when the form choice (relation schema vs. matrix, or both) requires explanation beyond what the requirement and the OpenFGA model make obvious.

## Relations

- satisfies: [<Requirement>](../../requirements/system/<requirement>.md){id=<namespace>:req:<opaque>}
