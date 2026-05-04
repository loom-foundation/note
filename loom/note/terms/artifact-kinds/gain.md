---
id: note:term:7e4f92v
name: Gain
kind: term
status: current
---

A positive outcome a persona wants to achieve while getting a Job done: a facet of a Need that states what the persona wants, never what a product offers.

A Gain ranges over the Kano expectation ladder, from a *required* outcome through *expected* and *desired* ones to an *unexpected* delight; the optional `expectation` frontmatter field records where on the ladder a gain sits ([Gain expectation field](../../decisions/gain-expectation-field.md){id=note:dec:c1m3hpn}).

## Inclusion test

Does it name an outcome the persona wants, in the persona's own terms?

A Gain may reference, in the persona's voice, the kind of thing they want ("a stable API so my integration keeps working", "a link that fits anywhere"); that is the persona's domain.

It is mis-filed only when it obligates the system, prescribes a specific mechanism, format, or standard, or describes, benefit-led, what the product *offers* to produce the outcome (a Gain Creator on an Offering); keep the focus on the wanted outcome, not a design for the system.

A Gain must name an outcome the persona positively seeks, not merely the absence of a Pain already recorded.
A Gain whose only content is that some Pain does not occur restates that Pain and earns no separate place ([Earned Substance](../../principles/earned-substance.md){id=note:principle:yecemfe}); a Pain and a Gain on the same Job are both kept only where the outcome sought and the outcome avoided genuinely differ.

## Relations

- *is part of* [Need](need.md){id=note:term:x4vqdj1}
- *carries* [Expectation](../gain-expectations/expectation.md){id=note:term:na2bqej}
- *relates to* [Job](job.md){id=note:term:41qzg6f} (the framing facet a Gain is felt against; a Gain artifact may carry the `framedBy` edge to a Job in its own Need, inverse `frames`)
- *contrasts with* [Gain Creator](gain-creator.md){id=note:term:g9fxrs5}

## Origin

The customer profile of the Value Proposition Canvas (Osterwalder, Pigneur, Bernarda, and Smith, *Value Proposition Design*, 2014), where gains are the outcomes and benefits a persona wants alongside the jobs and pains.

The expectation levels are taken from the Kano model (Kano et al., 1984), which grades a desired outcome from a must-be requirement through one-dimensional expectations to a delighter the persona does not anticipate.
