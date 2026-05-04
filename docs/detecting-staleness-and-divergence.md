# Detecting staleness and divergence

How to read the two drift signals a corpus carries: staleness, that a referenced artifact's text has moved, and divergence, that a running system has parted from the contract a specification describes.
This is orientation and applied guidance, not normative text; the binding meanings live in [Staleness](../loom/note/terms/drift/staleness.md){id=note:term:psh3vcg} and [Divergence](../loom/note/terms/drift/divergence.md){id=note:term:47bcgvy}, the mechanism is fixed in [Detect staleness from git provenance, not a stored digest](../loom/note/decisions/detect-staleness-from-git-not-a-stored-digest.md){id=note:dec:dvk7m2x}, and the obligations they answer are [Detectable staleness](../loom/note/requirements/system/detectable-staleness.md){id=note:req:46xm59a} and [Detectable divergence](../loom/note/requirements/system/detectable-divergence.md){id=note:req:vttexty}.

## Two different questions

Staleness and divergence are easy to blur, so it helps to keep them apart from the start.

Staleness is about text.
A dependent relied on a referenced artifact at one version; that text has since changed; so the dependency is no longer known to hold and is due for a re-check ([Staleness](../loom/note/terms/drift/staleness.md){id=note:term:psh3vcg}).
The inclusion test is blunt: did the thing pointed at change, regardless of whether anything is now actually incorrect?
If yes, it is stale.

Divergence is about behavior.
A specification states a contract; the running system no longer honors it; the two have parted, whether or not any text was touched ([Divergence](../loom/note/terms/drift/divergence.md){id=note:term:47bcgvy}).
The test mirrors the first: has the running behavior parted from the contract, independent of any text change?
Judging that needs execution, so it is a different kind of check with a different owner.

The short version: staleness you can detect from the files; divergence you can only confirm by running the system.

## The signal is three-valued, and never false-clears

Staleness detection reports one of three states for each dependent: fresh, stale, or can't-tell.

- *Fresh*: the cited text has not moved since the citing relationship was established.
- *Stale*: it has moved, so the dependent is surfaced for re-check.
- *Can't-tell*: the reference point cannot be established, so the signal honestly declines to answer.

The point of the third value is that the signal never reports a false all-clear.
Where it cannot establish when the citing relationship was set or when the target last changed, it says can't-tell, never a silent pass.
This matters most in a history-stripped working copy: a shallow clone, a squashed or rebased history, or a plain-file export with no git history at all.
There the honest output is can't-tell.
A tool that quietly returned fresh in that situation would be lying about exactly the catastrophic change this signal exists to catch.

## Where the signal comes from (and what is forthcoming)

Detection is computed, not stored.
It compares when the target artifact's content last changed against when each citing relationship was established, both read from git provenance against the existing citation graph ([Detect staleness from git provenance, not a stored digest](../loom/note/decisions/detect-staleness-from-git-not-a-stored-digest.md){id=note:dec:dvk7m2x}).
A dependent whose citing relationship predates the target's last content change relied on the older text, so it is surfaced.

There is deliberately no stored content digest and no new per-link field.
A digest would be the first load-bearing part of a citation that no human could author or audit by hand, which breaks the floor that well-formedness is checkable from the file alone.
Reusing git history adds nothing an author must write or maintain, and nothing that can rot into a silent lie.

Be clear about what runs today.
The bare files do not compute this themselves.
Walking git history across repositories and resolving the citation graph is work the supporting tool (Sett) owns, and that cross-corpus computation is forthcoming, not something the corpus performs on its own right now.
The corpus records the choice, its scope, and its residual risk; the scan is the tool's job.

## History-stripped copies: the tool-side baseline

Git provenance answers from history, and history is exactly what a sandboxed agent, a continuous-integration runner, or a plain-file export often does not have.
There the honest answer is can't-tell, and the method keeps it that way: Note adds no authored field, no stored digest, and no marker to its files for this case.

The gap is anticipated and closed on the tool side.
The supporting tool regenerates, where full history lives, a committed derived baseline recording when each artifact's content last changed, a content fingerprint per artifact, and when each citing relationship was established; a history-stripped working copy reads that baseline instead of history and answers fresh or stale for everything it covers, while anything beyond its coverage honestly stays can't-tell (Sett's freshness-index decision).

A method-side alternative, a hand-authored per-citation quote of the relied-on clause, was designed in full and declined for the authoring load it would place on every protected citation; the weighing is recorded in [Detect staleness from git provenance, not a stored digest](../loom/note/decisions/detect-staleness-from-git-not-a-stored-digest.md){id=note:dec:dvk7m2x} under Alternatives considered.

## What to do with each signal

A stale citation is a prompt, not a verdict.

A stale dependent is an invitation to re-check, never a build blocker.
Surfacing text-movement is all the signal claims to do; whether the change actually invalidates the dependent is the re-check, a human or AI judgment, and it is deliberately not auto-decided.
Most reworded text leaves its dependents perfectly valid; a few changes break them; only a re-check tells the two apart.

Behavior parting from contract is the other case entirely.
That is divergence, it needs execution, and it is routed to whoever can run the system: the Orchestrating Authority, not this signal ([Detectable divergence](../loom/note/requirements/system/detectable-divergence.md){id=note:req:vttexty}).
Note represents the relationship and the obligation to check; it does not run the check.

## A worked example

A system requirement once read "the service shall respond within 10 seconds."
Under review, the threshold is tightened, and the requirement is revised in place to "the service shall respond within 10 milliseconds."
The id never moves; the obligation behind it does.

Because the text changed under a stable id, every artifact that cited that requirement now relied on the older wording.
Each one surfaces as stale: the specifications that descend from it, any acceptance criteria that quote it, and every in-code `@intent` citation that points an implementation back at it.
Nothing is auto-failed.

The stale flags route the team to a single question: does the implementation still honor the new wording?
A handler that comfortably answers in microseconds is fine; the citation is re-checked, found still valid, and the flag clears.
A handler that took eight seconds is now in trouble, and the re-check says so.
If the team then runs the service and observes it missing the 10 millisecond contract, that is no longer staleness at all; it is divergence, and it goes to whoever can run the system.

## Normative sources

The orientation here restates what these fix:

- [Staleness](../loom/note/terms/drift/staleness.md){id=note:term:psh3vcg}: the text of a referenced artifact changed since a dependent relied on it.
- [Divergence](../loom/note/terms/drift/divergence.md){id=note:term:47bcgvy}: running behavior has parted from the contract a specification describes.
- [Detect staleness from git provenance, not a stored digest](../loom/note/decisions/detect-staleness-from-git-not-a-stored-digest.md){id=note:dec:dvk7m2x}: the three-valued signal is computed from git and the citation graph, never from a stored digest, and never false-clears.
- [Detectable staleness](../loom/note/requirements/system/detectable-staleness.md){id=note:req:46xm59a}: it shall be detectable, from the files, that referenced text has moved since a dependent relied on it.
- [Detectable divergence](../loom/note/requirements/system/detectable-divergence.md){id=note:req:vttexty}: it shall be detectable that an implementation no longer honors its contract, as a signal distinct from staleness, with the check routed to the Orchestrating Authority.
- Sett's freshness-index decision (tool side): the committed derived baseline that narrows can't-tell in history-stripped copies; the method itself adds no field for this.
