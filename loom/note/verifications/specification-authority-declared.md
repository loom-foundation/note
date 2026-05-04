---
id: note:ver:sp9k2rt
name: Specification authority is declared
kind: verification
status: current
method: analysis
---

This verification confirms that every current Specification in a strict corpus declares its authority in frontmatter: an `authority` field is present, and every external pointer it lists resolves to a file that exists.
An empty list is a valid declaration that the Specification answers to no external authority.
The check is a static pass over the Specification artifacts; it computes and reports findings only, and the verdict belongs to the Orchestrating Authority.

## Criteria

A pass requires, across every artifact of kind `specification` at `status: current` in a corpus whose declared profile is `strict`, that:

- an `authority` frontmatter field is present, holding a list; a missing field is a failure;
- every entry in the list is a repository-relative path that resolves to an existing file; a dangling pointer is a failure;
- an empty list is valid, declaring that the Specification answers to no external authority.

A pass is zero failures across the Specifications in scope.

## Procedure

By analysis.
A static reader traverses every committed artifact of kind `specification` at `status: current`.

For each it:
1. Reads the `authority` frontmatter field, recording its absence as a failure.
2. For each entry in the list, resolves the repository-relative path against the repository root, recording any that does not exist.

The reader only reads; it executes nothing and writes nothing, so the check is reproducible by anyone with the repository.
Whether a running implementation honors a Specification is a separate concern, a Verification of that implementation against the Specification, not this check.

## Relations

- verifies: [Independently validatable specifications](../requirements/system/independently-validatable-specifications.md){id=note:req:fph0vnr}
- verifies: [Verifiable, independently checkable design](../requirements/stakeholder/verifiable-independently-checkable-design.md){id=note:req:vh3k82n}
