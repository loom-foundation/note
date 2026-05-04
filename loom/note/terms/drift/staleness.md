---
id: note:term:psh3vcg
name: Staleness
kind: term
status: current
---

The condition where the text of a referenced artifact has changed since a dependent relied on it, so the dependent should be re-checked.

Staleness is about the text moving, not about behavior being wrong.

## Inclusion test

Did the thing pointed at change, regardless of whether anything is now incorrect?
If so, it is staleness; if instead the running behavior has parted from the contract independent of any text change, that is divergence.

## Origin

General English (Oxford: "stale", no longer fresh or current, of something that has lost its currency through the passage of time or events).

The corpus narrows the everyday sense to a precise relation: a dependent relied on a referenced artifact at one version, that text has since moved, and so the dependency is no longer known to hold and is due for re-checking.

The notion is standard in build and caching systems, where a cached or derived result is stale once an input it was computed from has changed.
