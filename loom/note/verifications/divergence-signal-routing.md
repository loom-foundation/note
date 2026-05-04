---
id: note:ver:dv9rk4t
name: Divergence is represented and routed, never adjudicated
kind: verification
status: current
method: inspection
---

This verification confirms that divergence, an implementation no longer honoring the contract a specification describes, is represented as a signal distinct from staleness and routed to the Orchestrating Authority, with the corpus holding no verdict of its own.
The check inspects the committed artifacts; whether any implementation has actually diverged is a run the Orchestrating Authority owns, not this check.

## Criteria

A pass requires that:

- the drift vocabulary keeps the two signals distinct, behavior against text: [Divergence](../terms/drift/divergence.md){id=note:term:47bcgvy} and [Staleness](../terms/drift/staleness.md){id=note:term:psh3vcg} each carry an inclusion test that tells one from the other;
- the obligation routes the running of any divergence check to the Orchestrating Authority, since it requires execution the System does not perform;
- no artifact in the corpus authors a divergence verdict: no frontmatter field and no body section records a pass or fail as authoritative state.

A pass is all three holding across the corpus.

## Procedure

By inspection.
A reader confirms the two drift terms draw the text-versus-behavior distinction, confirms the routing statement on the divergence obligation, and scans every artifact's frontmatter and sections for an authored verdict, expecting none.
The inspection needs only the committed files, so it is reproducible by anyone with the repository.

## Evidence

A run records the three confirmations and any verdict-shaped field or section found.
The record is kept with the run by the Orchestrating Authority; it is not stored in this artifact.

## Relations

- verifies: [Detectable divergence](../requirements/system/detectable-divergence.md){id=note:req:vttexty}
