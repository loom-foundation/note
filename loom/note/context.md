---
id: note:ctx:rzbtzq9
name: System context
kind: context
status: current
---

Standalone, Note is the System: the representation-and-checks layer (see the System and boundary group under `terms/`).

Embedded in a larger methodology-and-orchestration system, Note is a Subsystem of it.

The boundary is the same in both cases; only the supersystem differs, and it may be absent.

## External entities

The external entities the System interacts with, whether or not an orchestrator is present:

- Actors, human and AI, that read and author artifacts through file access.
  Some AI actors operate in constrained environments (sandboxes, continuous-integration runners, small models).
- A Git host or repository, the substrate of record and the trust root: history, signatures, protected branches, code-owners.
- A continuous-integration system that runs checks and gates merges.
- Downstream tools that consume the artifacts: Markdown renderers, code generators, contract testers, schema validators.
- Sett: a reference tool that reads the artifacts, computes derived views and validation, and proposes authoring changes; Sett is never authoritative.
- An Orchestrating Authority, when present: an orchestration system, or the combination of the Git host's controls with code review, playing the roles described below.

```
        Actors (human / AI)        Downstream tools
                 \                      /
                  v                    v
            +-------------------------------+
            |         Note (System)         |
            +-------------------------------+
                  ^                    ^
                  |                    |
            Git host / CI        Orchestrating Authority
            (substrate, gates)   (identity, permission; may be absent)
                  ^
                  |
                 Sett
            (reads, computes,
             proposes; external)
```

## What crosses the boundary

The boundary is a port: Note defines representations and checks; an Orchestrating Authority consumes them and decides permission.

Note depends on no orchestrator, but it exposes a clean interface for one.

| From                  | To                   | Interaction                                          |
| --------------------- | -------------------- | ---------------------------------------------------- |
| Actors (human / AI)   | Note artifacts       | Read and author through file access                  |
| Sett                  | Note artifacts       | Reads and computes derived views, and proposes validated authoring changes (never authoritative) |
| Orchestrating Authority | Sett                 | May invoke and consume results to decide             |
| Orchestrating Authority | Artifacts and merges | Permits or blocks; enforces separation and authority |
| Git host / CI         | Artifacts and merges | Stores, gates, signs                                 |

## What is out of scope

Stated negatively, on purpose.

Note does not:

- Enforce access control over files.
  Who may read or write an artifact is the Git host's and the Orchestrating Authority's concern.
- Ensure that the actor who builds the code differs from the one who authored the specification or the verification.
  That separation needs actor identity the System does not hold.
- Build code from an artifact.
  Building is an actor's job.
  The System represents the design; it does not act on it.
- Independently verify code against intent.
  Note represents the verifies relation and defines what checkability means;
  a downstream tool such as Sett computes whether a relation resolves and is fresh;
  the dispatch and independence of a verifying actor are the Orchestrating Authority's.
- Authorize lifecycle transitions.
  Note defines which transitions are well-formed;
  who is permitted to make one is decided outside it.
- Govern who may exclude an inherited requirement.
  Note makes a deviation visible, attributable, and rationale-bearing;
  who may approve it is decided outside it.

The litmus test for any future responsibility: if it is a statement about an artifact, it belongs to Note; if it is a statement about an actor or about permission, it belongs to the Orchestrating Authority.

Representation and checkability stop at the file boundary; everything that reaches into *who* and *may* is outside.

This boundary holds without naming any particular orchestrator.

The Orchestrating Authority is a role, not a component: whatever the embedding system designates plays it.

Where Note is embedded in Loom, Loom plays the role, carrying the orchestration rules the methodology states (for example, that no one marks their own work).

Where Note is adopted into another system, that system designates its own: commonly the Git host's controls together with code review and continuous integration, sometimes a full orchestration platform, sometimes a human reviewer.

The System is unchanged either way.
