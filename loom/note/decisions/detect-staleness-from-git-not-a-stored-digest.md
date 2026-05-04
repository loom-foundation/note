---
id: note:dec:dvk7m2x
name: Detect staleness from git provenance, not a stored digest
kind: decision
status: current
decided: 2026-06-24T00:00:00Z
---

Staleness (that a referenced artifact's text has changed since a dependent relied on it) is detected by computing from git provenance against the existing citation graph, never by storing a content digest or any new per-link field.
A tool compares when the target's content last changed against when each citing relationship was established, and surfaces the dependents that relied on the older text for reassessment.
The detection is three-valued and never reports a false "all clear": fresh, stale, or can't-tell; in history-stripped working copies it reports can't-tell rather than a silent pass.
The cross-corpus computation is the responsibility of the supporting tool (Sett); the corpus records the choice and its residual risk.

## Context

This serves the drift-visibility family and, specifically, the risk that an artifact's text is materially revised under a stable id, silently invalidating the requirements, specifications, and code that descend from it: the "< 10 seconds → < 10 milliseconds" class of change, where the id never moves but the obligation behind it does.

Staleness is the text moving, not semantic correctness ([Staleness](../terms/drift/staleness.md){id=note:term:psh3vcg}): the inclusion test is "did the thing pointed at change, regardless of whether anything is now incorrect".
So the mechanism this decision fixes detects text-movement and surfaces it for re-check.
Judging whether the change is material (whether the revised text actually invalidates a dependent) is the reassessment, a human or AI re-check, and it is deliberately not auto-judged here.
Where the question is instead whether running behavior has parted from the contract, that is divergence, which needs execution and is routed to the Orchestrating Authority ([Detectable divergence](../requirements/system/detectable-divergence.md){id=note:req:vttexty}), not adjudicated by this signal.

## Decision

- **Staleness is computed, not stored.**
  Detection compares the target artifact's git history (when its content last changed) against the establishing commit of each citing relationship in the existing citation graph.
  A dependent whose citing relationship predates the target's last content change relied on the older text, and is surfaced for reassessment.
  No content digest, and no new per-link field, is introduced.

- **The signal is three-valued and never false-clears.**
  The output for any dependent is fresh (the cited text has not moved since the relationship was established), stale (it has), or can't-tell (the reference point cannot be established).
  It never reports a false "all clear": where the provenance is unavailable, the honest output is can't-tell, never a silent pass.

- **It detects text-movement; it does not judge materiality.**
  Surfacing a stale dependent invites a re-check; whether the change actually invalidates the dependent is the reassessment (human or AI), and whether running behavior has parted from the contract is divergence ([Detectable divergence](../requirements/system/detectable-divergence.md){id=note:req:vttexty}), neither of which this signal auto-judges.

- **The cross-corpus computation is the tool's responsibility.**
  Comparing histories across repositories and resolving the citation graph is work the supporting tool (Sett) owns; the corpus records the choice, its scope, and its residual risk, and depends on no per-link bookkeeping to make the signal available.

## Forces and trade-offs

Computing staleness from git reuses a signal the substrate already carries (the history every committed file has), so it adds no field an author must write or audit and nothing that can rot into a silent lie.
This is the decisive trade against storing a digest: a stored digest would be cheap for a tool to read but would put a load-bearing, non-hand-computable token into the citation, breaking the floor that well-formedness is checkable from the file alone.

The cost is honestly bounded.
Where git history is intact the signal is full; where it is not, the method does not pretend: it returns can't-tell, which is strictly better than a counter or a digest that can be stale, forgotten, or misjudged into a false reassurance.
Discharging the cross-corpus computation onto Sett is acceptable here because the corpus's job is to record the choice and keep the substrate hand-auditable, not to perform the scan; the same claim-and-tool split the method uses elsewhere.

## Alternatives considered

- **Store a content digest of the target in each cross-reference link, re-stamped on re-check.**
  Rejected.
  A digest is not hand-computable, so it would be the first load-bearing citation component no human can author or audit, violating the substrate's floor that well-formedness is "checked from the file alone, with no special tool" ([The substrate](../specifications/note/substrate.md){id=note:spec:tkhd63e}).
  It re-adopts the named-field annotation form already rejected for in-code citation, where a bespoke structured annotation "adds parsing surface and a thing to learn without earning its weight ([Earned Substance]; [Proportionality])" ([In-code intent citation](in-code-intent-citation.md){id=note:dec:nfaeyk9}).
  Its whole-body granularity also causes a fan-in storm (one reword flags every dependent), and it discharges acceptance onto an unbuilt tool.

- **An author-bumped revision counter (semver-style) on the target, pinned by the dependent.**
  Rejected.
  It duplicates what git already records, and it relies on the author remembering to bump: a forgotten or misjudged bump yields a false "all clear" on exactly the catastrophic material change this exists to catch.

- **A hand-authored "last reviewed / last modified" date marker.**
  Noted, not adopted now.
  It relies on author discipline (acceptable in principle, since the method relies on discipline until tooled, but it adds bookkeeping for only partial benefit), and filesystem modified-times are unreliable because a git clone overwrites them.
  Deferred as a possible future enhancement.

- **A hand-authored relied-on quote marker on the citation.**
  Designed in full and declined.
  The dependent would quote, on the citation entry, the verbatim clause it relies on (a `Quote: "..."` continuation line); a checker would decide the quote from the files alone, verbatim presence in the target's current body attesting that the relied-on clause stands, and absence surfacing the citation as stale in any environment, history or none.
  Re-checking would be re-quoting, so the quote-line diff would carry a human-readable, attributable acknowledgment of each re-check.
  The design is hand-auditable, history-loss-proof, and clause-level (so a reword elsewhere in a heavily-cited artifact would not flag every dependent), and it remains the strongest known shape for a method-side marker should one ever be revisited.
  Declined because it places a what-to-quote judgment on every author at every citation that wants protection, a standing authoring load out of proportion to the gap, and because the availability half of the gap is answered with no authoring load at all by the tool-side baseline recorded under Residual risk, which leaves the method's files untouched.

## Driven by

- groundedIn: [Detectable staleness](../requirements/system/detectable-staleness.md){id=note:req:46xm59a}
- groundedIn: [Compute and Report](../principles/compute-and-report.md){id=note:principle:6e7f28k}
- groundedIn: [Earned Substance](../principles/earned-substance.md){id=note:principle:yecemfe}

## Residual risk

The mitigation is partial, and the gap is written down rather than papered over.

Detection establishes its reference point from git history, so it does not reach history-stripped working copies: shallow clones, squashed or rebased history, and plain-file exports with no `.git` cannot establish when a citing relationship was set or when the target last changed.
There the text-change signal is unavailable and the corpus reports can't-tell: never a false-assurance, never a silent pass.

This residual was first deferred with two anticipated paths: an opt-in, hand-authored marker in the method, or the supporting tool owning the environment robustness.
The tripwire on it has since fired: AI agents in sandboxes and continuous-integration runners are primary actors of the method, and those environments routinely provide shallow or history-free checkouts, so can't-tell is the common answer exactly where machine-speed action most needs the signal.

The residual is resolved on the tool side, and the method deliberately adds nothing for it: no authored field, no stored digest, no marker.
The settled direction is a committed, derived staleness baseline the supporting tool regenerates as a pure function of a repository revision where full history lives, and that a history-stripped copy reads instead of history, narrowing can't-tell to fresh or stale for everything the baseline covers while the never-false-clear rule stands, the freshness-index decision recorded on the Sett side.
The method-side marker that was weighed and declined for this residual, a hand-authored relied-on quote, is recorded under Alternatives considered, never a revision counter.
