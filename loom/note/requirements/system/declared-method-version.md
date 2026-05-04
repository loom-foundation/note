---
id: note:req:vtbay6d
name: Declared method version
kind: requirement
level: system
type: functional
status: current
---

Note shall ensure a corpus can declare the method version it targets, so that conformance is evaluated against the ruleset of that version and a migration across versions can be driven from a known starting point.

## Rationale

A forward path requires knowing where a corpus starts.

Declaring the targeted version lets a tool apply the right rules and lets a migration know what it is migrating from.

The compatibility and migration guarantees built on this declaration are the system requirements derived from [Non-breaking evolution with a guaranteed forward path](../stakeholder/non-breaking-evolution.md){id=note:req:peh9g30}, and the tool's role in executing a migration is carried by Sett's own migration-execution requirement; the version scheme is specification.

## Relations

- derivedFrom: [Non-breaking evolution with a guaranteed forward path](../stakeholder/non-breaking-evolution.md){id=note:req:peh9g30}
