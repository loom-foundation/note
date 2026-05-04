---
id: note:term:fjmzfre
name: Validation State
kind: term
status: current
---

The result of checking an artifact or a relation: **valid**, **invalid**, or **unresolved**.

Unresolved is distinct from invalid: it marks a reference or scope parent whose target lives in a repository not currently resolvable.

Global properties (acyclicity, coverage, effective-intent resolution) are asserted only over the resolvable closure.

## Inclusion test

Is the artifact or relation ill-formed or in breach of a rule?
If so it is invalid; if instead it is well-formed but its target lives in a repository not currently reachable, that is unresolved, not invalid.

## Origin

General English: "validation" is the act of checking that something is sound or well-founded, and a "state" is a condition something is in (Oxford).
The compound names the verdict such a check yields.

The three-way split tracks the standards sense of validation against a schema or constraint set (as in XML and document validation), with "unresolved" added to keep a reference that cannot be reached from being scored as a failure of the artifact that holds it.
