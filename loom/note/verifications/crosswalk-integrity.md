---
id: note:ver:cw2xkq6
name: Crosswalk integrity
kind: verification
status: current
method: analysis
---

This verification confirms that mappings to external frameworks stay typed, directional, and honest: every crosswalk edge is one of the defined verbs, authored on the obligation end against a read-only control artifact, and the resulting graph is bipartite and acyclic, so a mapping claims exactly what its verb says and nothing flows back from the framework into the corpus's own intent.
The check is a static pass over the crosswalk edges and control artifacts; it computes and reports findings only, and the verdict belongs to the Orchestrating Authority.

## Criteria

A pass requires that:

- every crosswalk edge uses a verb from the defined crosswalk set, so the strength of each claimed mapping is typed rather than implied;
- every edge is authored on the corpus obligation and points at a control artifact, never the reverse, and each target control resolves by its id;
- every control artifact is a read-only representation of the external clause (an identifier, a title, and a source citation), authoring no obligation of its own, so the framework text stays authoritative where it lives;
- the crosswalk graph is bipartite between obligations and controls and contains no cycle, so coverage rolls up without double counting;
- for any sampled control, the set of obligations mapping to it is computable by inspection, so a coverage view derives from the files rather than a maintained matrix.

A pass is zero failures across the authored crosswalk; a corpus with no crosswalk passes vacuously and is reported as unexercised.

## Procedure

By analysis.
A static reader collects every crosswalk edge, validates its verb against the defined set and its direction against the authored-on-obligation rule, resolves each target control, and checks each control artifact for obligation-free content; it then builds the full graph, tests it for bipartiteness and cycles, and inverts it for a sampled control to confirm the coverage view derives.
The reader only reads; it executes nothing, so the check is reproducible by anyone with the repository.

## Evidence

A run produces a report: the edge census by verb, each resolution and direction check, any control found authoring obligations, the graph-shape result, and the sampled coverage inversion.
The report is kept with the run by the Orchestrating Authority; it is not stored in this artifact.

## Relations

- verifies: [Intent mappable to external frameworks](../requirements/stakeholder/mappable-to-external-frameworks.md){id=note:req:ddh4kfx}
- verifies: [Typed framework crosswalk](../requirements/system/typed-framework-crosswalk.md){id=note:req:p2ry9tv}
