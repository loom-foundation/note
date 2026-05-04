---
id: note:term:hb74nmn
name: Pain
kind: term
status: current
---

A negative outcome, obstacle, or risk a persona wants to avoid while getting a Job done.

A Pain is a facet of a Need, captured as its own artifact, and states what the persona suffers, never what a product offers.

A Pain may be an undesired outcome or problem the persona already endures, an obstacle that stands in the way of a Job, or a Risk: a potential, not-yet-realized undesired outcome the persona fears.

## Inclusion test

Does it state, in the persona's own terms, what they suffer or fear while getting a Job done, and its consequence?

A Pain may name the kind of thing the persona lacks or struggles with in their own domain ("a stable API my integration can rely on", "a link that looks trustworthy"); that is the persona's voice, not a prescribed solution.

It is mis-filed only when it obligates the system ("Shortr shall provide a stable API" is a Requirement), prescribes a specific mechanism, format, or standard ("a versioned endpoint using the XYZ standard" is a leaked solution), or describes, benefit-led, what the product *offers* to relieve it (a Pain Reliever on an Offering).

Keep the focus on the persona's experienced problem and its consequence, not on a design for the system.

A Pain must name a negative the persona genuinely suffers or fears, not merely the absence of a Gain already recorded.
Where a Pain and a Gain on the same Job would say the same thing in opposite voice, only one has earned its place ([Earned Substance](../../principles/earned-substance.md){id=note:principle:yecemfe}); keep both only where the outcome avoided and the outcome sought genuinely differ.

## Relations

- *is part of* [Need](need.md){id=note:term:x4vqdj1}
- *carries* [Subkind](../pain-subkinds/subkind.md){id=note:term:2tzss22}
- *relates to* [Job](job.md){id=note:term:41qzg6f} (the framing facet a Pain is felt against; a Pain artifact may carry the `framedBy` edge to a Job in its own Need, inverse `frames`)
- *contrasts with* [Pain Reliever](pain-reliever.md){id=note:term:7qrdxnp} (suffered versus offered)

## Origin

The customer profile of the Strategyzer Value Proposition Canvas (Osterwalder et al.), which lists the pains a persona experiences alongside their jobs and gains.

The pain sub-kinds (undesired outcome or problem, obstacle, and risk) follow that canvas's own classification, so a risk is recognized as a kind of pain rather than overlooked; a pain's sub-kind is recordable as the optional `subkind` frontmatter field ([Pain subkind field](../../decisions/pain-subkind-field.md){id=note:dec:qc2nc57}).

Sharpened by Kano's dissatisfiers (must-be quality), whose absence is felt as pain though its presence earns no satisfaction.
