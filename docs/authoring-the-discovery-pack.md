# Authoring the discovery pack

How to think your way into a Need when the discovery pack is enabled, so the persona, the job, the situation, and the motivation each land in the right facet and you do not end up with a pair of facets that say the same thing twice.
This is a promoted thinking aid, orientation and applied guidance, not normative text; nothing here adds a rule. The binding shape of a Need and its facets lives in the [Need](../loom/note/terms/artifact-kinds/need.md){id=note:term:x4vqdj1} and [Job](../loom/note/terms/artifact-kinds/job.md){id=note:term:41qzg6f} terms, in the lead-naming rule fixed by [The spine pack](../loom/note/specifications/note/spine-pack.md){id=note:spec:6kjja5r}, and in [Earned Substance](../loom/note/principles/earned-substance.md){id=note:principle:yecemfe}.
For the model these facets sit in, the Need-Fit-Offering picture and the discovery pack's kinds, see [from-need-to-specification.md](from-need-to-specification.md).

## A sentence to think with, not a format to fill in

When you sit down to capture a need, a single formulation holds all four parts in view at once:

> **As a [persona], when [situation], I want [outcome], so [why].**

Read off the parts and each maps onto something the discovery pack already names:

- **WHO** -- the **persona**, the holder of the need; the `persona` field on the [Need](../loom/note/terms/artifact-kinds/need.md){id=note:term:x4vqdj1}, named in its lead.
- **WHEN** -- the **situation**, the circumstance in which the need arises; the trigger, the context that makes the want live.
- **WHAT** -- the **outcome the persona wants to get done**; the [Job](../loom/note/terms/artifact-kinds/job.md){id=note:term:41qzg6f}, stated independently of any mechanism.
- **WHY** -- the **motivation**, the pull behind the want; a [Pain](../loom/note/terms/artifact-kinds/pain.md){id=note:term:hb74nmn} they want to escape, a [Gain](../loom/note/terms/artifact-kinds/gain.md){id=note:term:7e4f92v} they want to reach, or both when each names a genuinely distinct facet.

This is the same job-story shape the requirements and jobs-to-be-done traditions reach for, and it is exactly the register a faceted Need's lead already reads in.
Use the sentence to *think*. It is a scaffold for getting the four parts straight in your head before you split them across facet files; it is not a mandated lead format and nothing checks for it.
When you write the artifacts, the persona goes in the `persona` field and the lead, the outcome becomes the Job, the situation colours the lead and any illustrative-situation prose, and the motivation, if it earns its place, becomes a Pain or a Gain.

## A recommended order of capture

The formulation also suggests the order to capture things in, which keeps you from inventing motivation before you know whose it is or what it is for.

1. **Persona first.** Decide whose need this is. Everything downstream is stated in that persona's terms, so settle the holder before the prose. If you find yourself wanting to name two personas who turn out to want different things, that is a sign to split the need rather than to stack names (the lead-naming rule in [The spine pack](../loom/note/specifications/note/spine-pack.md){id=note:spec:6kjja5r}).
2. **Their jobs next.** Name what the persona is trying to get done, the [Job](../loom/note/terms/artifact-kinds/job.md){id=note:term:41qzg6f}, at the level of the task itself and free of any mechanism for doing it. The job is the frame everything else is felt against.
3. **The situation the need arises in.** When does this want become live? The circumstance is what makes the job urgent rather than abstract, and it is what an Offering will eventually have to meet the persona inside of.
4. **Pain or gain, only when it adds unique substance.** Now ask what actually moves the persona here: a hurt they want to escape (a Pain), a benefit they want to reach (a Gain), or genuinely both. Capture a Pain, a Gain, or both, and capture each *only* when it names a distinct facet of the motivation, never as a positive-and-negative restatement of one thing.

The first three steps are nearly always worth taking. The fourth is where most over-authoring happens, which is why it carries a condition rather than an instruction.

## On the fourth step: do not mirror the motivation

The trap at step four is to write the motivation twice, once as a Pain and once as the same thing turned positive into a Gain, so a single facet of motivation reads as two.
This is the mirror-image trap, and the discipline for avoiding it, decide the primary motivation, lead with it, and reach for the second facet only when the two name genuinely different outcomes, is set out in full in [authoring-pains-and-gains.md](authoring-pains-and-gains.md), together with the test for whether a candidate second facet has earned its place and the "when in doubt, prefer one" guidance.
That doc is the home for this; this one only points you to it at the moment in the capture order where the trap waits.

## A worked example

Take a support engineer who needs to find which past incidents resemble the one on their screen right now.

Walk the order:

1. **Persona:** the Support Engineer. Whose need this is, settled first.
2. **Job:** *find prior incidents that resemble the one in front of me.* What they are getting done, stated without naming search, tags, or any mechanism.
3. **Situation:** *a live incident is open and the clock is running.* The circumstance that makes the job urgent rather than idle curiosity.
4. **Motivation:** the real pull here is avoidance, so the primary facet is a **Pain**: *re-solving an incident the team has already solved, because the prior fix could not be found in time.* Ask the step-four question, strip the Pain and does a distinct positive remain that the persona seeks? If the only candidate Gain is "the prior fix is found," that is the Pain in positive voice and earns nothing, so it stays a single Pain. A distinct Gain would have to name a different outcome, say *building reusable institutional memory the whole team draws on later*, and only then would it earn a place beside the Pain.

Held in the thinking sentence, the need reads:

> As a **Support Engineer**, when **a live incident is open and the clock is running**, I want to **find prior incidents that resemble it**, so **I do not waste time re-solving what the team already solved.**

From that one sentence: the persona goes in the `persona` field and the lead, the job becomes the Job facet, the situation colours the lead, and the motivation lands as a single Pain, no mirrored Gain manufactured to keep it company.

## Normative sources

The orientation here restates, and never adds to, what these fix:

- [Need](../loom/note/terms/artifact-kinds/need.md){id=note:term:x4vqdj1} and [Job](../loom/note/terms/artifact-kinds/job.md){id=note:term:41qzg6f}: a Need is a persona's problem profile over its facets, stated in the persona's terms and free of solutions; a Job is the task framing the persona's pains and gains are felt against.
- The lead-naming rule in [The spine pack](../loom/note/specifications/note/spine-pack.md){id=note:spec:6kjja5r}: the holder is named in the lead and the `persona` field stays authoritative.
- [Earned Substance](../loom/note/principles/earned-substance.md){id=note:principle:yecemfe}: a facet that carries no distinct load has not earned its place, the rule behind the fourth step's condition.
- [authoring-pains-and-gains.md](authoring-pains-and-gains.md): the mirror-image trap, the test for a distinct second facet, and the "prefer one" guidance the fourth step defers to.
