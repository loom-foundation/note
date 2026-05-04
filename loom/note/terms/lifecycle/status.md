---
id: note:term:xcen4v2
name: Status
kind: term
status: current
---

The frontmatter field that records an artifact's lifecycle state: for the ladder values, how far its content has matured; for the terminal values, that it has been retired (`obsolete`) or declined (`rejected`).

Every artifact carries it; an artifact with no `status` is read as `tbd`.

Its value is one of the five states below.

## Inclusion test

Does the field answer "how far has this artifact's content matured, or has it reached a terminal state?", rather than "what kind of artifact is it?" (kind) or "is its content correct?" (validation state)?

If it tracks lifecycle state, it is the status field; if it fixes the artifact's body shape, that is kind.

## Origin

General English (Oxford: "the situation at a particular time during a process"), specialized here to the maturity of an artifact's content.
Document control (ISO 9001:2015 §7.5) and docs-as-code practice settle on a `status` field over `state`, `maturity`, or a `draft` boolean, and on a closed set of named states rather than a free-text label.
