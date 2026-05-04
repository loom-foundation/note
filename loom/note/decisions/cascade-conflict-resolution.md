---
id: note:dec:9c4tk2n
name: Cascade conflict resolution
kind: decision
status: current
decided: 2026-06-03T01:50:26Z
---

When intent inherited from more than one scope conflicts on the same point, the cascade resolves the conflict by proximity where the sources are comparable along the scope graph, and surfaces it for explicit resolution where they are not.

A source at a nearer, more specific scope governs a source at a farther one, because the nearer source is itself authored intent rather than a guess.

Two sources at genuinely incomparable positions are surfaced, never auto-tiebroken.

A nearer source that removes an inherited obligation is always surfaced, even when proximity would make its precedence unambiguous.

## Context

A scope can inherit from more than one parent (the scope graph is a directed acyclic graph, not a single chain), so that a cross-cutting concern owned in one branch can apply to products in another ([Scope and inheritance](../requirements/system/scope-and-inheritance.md){id=note:req:96smmcv}).

When two inherited sources disagree on the same point, the cascade must either pick a winner or surface the disagreement.

The standing commitment was that multi-source conflicts are surfaced, not silently merged ([Effective-intent resolution](../requirements/system/effective-intent-resolution.md){id=note:req:5xnajsm}).

Two failure modes bracket the choice.

Surfacing every disagreement turns the common case (a nearer scope strengthening an inherited default, which happens on almost every scope once cross-cutting parents exist) into noise that buries the one genuine conflict; alert fatigue is itself a failure.

Totalizing every conflict to a single winner, as CSS does (nearest wins, ties broken by declaration order), silently resolves a genuine equal-distance conflict by an arbitrary rule, which is the silent wrong-pick discovered only in an audit, and is exactly the silent merge Note rejects.

## Decision

- **Proximity resolves the comparable.**
  Where two conflicting inherited sources are comparable along the scope graph, one nearer the inheriting scope than the other, the nearer source governs, automatically and without surfacing.
  A team's local rule overriding a company default is authored intent, not a guess, and does not need a reviewer's attention.
- **Genuine ties are surfaced, not tiebroken.**
  Where two conflicting sources are not comparable (two cross-cutting parents at incomparable positions), the conflict is surfaced for explicit resolution.
  The cascade shall not invent a distance metric to force a winner.
  "Equal distance, surface" is a defined, non-negotiable residue, not an under-specified fallback.
- **Proximity is a partial order, not a total one.**
  Nearer is defined only between comparable scopes; where it is undefined, the conflict surfaces.
- **Removal is always loud.**
  Proximity auto-resolves only strengthening and replacement.
  A nearer source that removes (disinherits) an inherited obligation is always surfaced, attributable, and rationale-bearing, even when proximity would make its precedence unambiguous, so that an inherited obligation is never silently dropped by a nearer scope ([Visible, attributable deviation](../requirements/system/visible-attributable-deviation.md){id=note:req:64eknb1}).
- **A surfaced conflict carries provenance.**
  Each surfaced conflict names every contributing source and the scope and owner it came from, so resolution happens at the right scope rather than by guesswork.
- **A precedence may be declared once.**
  An author may declare a precedence among otherwise incomparable parents, with a rationale; that declaration is itself a visible, attributable deviation, auditable like any other, and it converts a recurring surfaced tie into authored intent.

## Worked example

The rules above are easier to read on one concrete scenario.
Take an organization, Acme, with this scope graph:

```
                       Acme (organization)
                      /        |         \
              Security      Privacy      Payments (product)
          (cross-cutting) (cross-cutting)      |
                      \        |         /
                        Checkout (service)
```

Checkout inherits along the product chain (Acme, then Payments, then Checkout) and from the two cross-cutting scopes (Security and Privacy).
"Nearer" means fewer inheritance steps away from Checkout.
Payments is nearer to Checkout than Acme is.
Security and Privacy are **incomparable**: neither contains the other, and neither is nearer to Checkout than the other.

Four points of intent, one per rule:

**1. Proximity resolves the comparable (a strengthening).**
Minimum TLS version.
Acme says TLS 1.2; Payments says TLS 1.3.
Both sit on the same chain above Checkout, so they are comparable, and Payments is nearer.

> **Result:** TLS 1.3, resolved automatically, nothing surfaced. Payments tightening Acme's
> floor is authored intent, not a guess, so it needs no reviewer's attention.

**2. A genuine tie is surfaced, not tiebroken.**
Access-log retention.
Security says "retain for 1 year" (for incident forensics); Privacy says "delete after 30 days" (data minimization).
These come from incomparable scopes, so proximity cannot order them.

> **Result:** a surfaced conflict, **not** an automatic pick. It names both sources and their
> owners (Security, owned by SecOps; Privacy, owned by the Data Protection Officer) so the
> right people resolve it at the right scope. The cascade does **not** invent a rule like
> "declaration order wins" to choose one silently.

**3. Removal is always loud.**
Service-to-service mTLS.
The Security scope mandates it.
Checkout has a legacy dependency that cannot do mTLS, so Checkout wants to opt out.
Checkout is nearer than Security, so proximity *could* make Checkout win unambiguously.

> **Result:** still surfaced. Because this is a **removal** of an inherited obligation, not a
> strengthen or replace, proximity does not silently let it through. The opt-out is recorded
> on Checkout with a rationale, attributed to its author, and routed to the Security scope's
> owner. A dropped security control never disappears quietly.

**4. A precedence may be declared once.**
The log-retention tie from case 2 recurs on every service, and Acme has decided Privacy should govern PII in access logs.
Checkout's owner declares, once, "Privacy precedes Security for access-log retention here", with a rationale (GDPR data minimization).

> **Result:** from now on that specific tie resolves automatically to "delete after 30 days".
> The declaration is itself a visible, attributable deviation, auditable like any other, so the
> tie is now *authored* intent rather than a guess, and it stops being surfaced.

Putting the four results side by side:

| Point                | Sources                          | Rule that fires            | Outcome at Checkout                          |
| -------------------- | -------------------------------- | -------------------------- | -------------------------------------------- |
| TLS version          | Acme 1.2, Payments 1.3 (chain)   | Proximity (strengthen)     | TLS 1.3, auto-resolved, silent               |
| Log retention        | Security 1y, Privacy 30d (tie)   | Surface the incomparable   | Conflict surfaced with provenance            |
| mTLS                 | Security mandates, Checkout opts out | Removal is always loud | Opt-out surfaced, attributed, routed to owner |
| Log retention (after declaration) | declared: Privacy precedes Security | Declared precedence | "delete after 30d", auto-resolved, audited |

The pattern in one line: **the cascade resolves what is unambiguously authored (a nearer scope strengthening or replacing) and surfaces what is a genuine judgment call (an incomparable tie or any removal), so silent merges and silent drops both become impossible.**

## Forces and trade-offs

- Resolving the comparable and surfacing the incomparable honors the efficiency of the common case and Note's surface-do-not-merge ethos for the genuine case, at the cost of a model with two outcomes (resolve, surface) rather than one.
  The two outcomes are warranted: collapsing to always-surface buries the signal, and collapsing to always-resolve hides the wrong pick.
- Treating removal as always loud costs an interruption on every nearer-scope opt-out, even unambiguous ones.
  Accepted, because a silently dropped cross-cutting obligation (a security control opted out by a nearer team) is the precise audit surprise the methodology exists to prevent.
- Proximity as a partial order leaves a defined residue that a human or a declared precedence must resolve, rather than the tool.
  This is the intended cost: the residue is the genuine conflict, and the tool's job is to present it faithfully, not to dispose of it.

## Alternatives considered

- **Surface every multi-source disagreement.**
  Rejected: with cross-cutting scopes, most disagreements are benign strengthenings, and surfacing all of them buries the one genuine conflict.
- **Total order: nearest wins, ties broken by a fixed rule such as declaration order.**
  Rejected: it resolves a genuine equal-distance conflict by an arbitrary rule, a silent wrong-pick, and is the silent merge Note rejects.
  This is the CSS model, whose totalization is exactly what does not fit surface-do-not-merge.
- **Let proximity auto-resolve removals too.**
  Rejected: a nearer scope silently nearer-wins-removing a cross-cutting obligation is the exact audit surprise to prevent; removal stays loud regardless of proximity.

## Driven by

- groundedIn: [Effective-intent resolution](../requirements/system/effective-intent-resolution.md){id=note:req:5xnajsm}
- groundedIn: [Deviation operators on inherited intent](../requirements/system/deviation-from-inherited-intent.md){id=note:req:sd7ch4m}
- groundedIn: [Visible, attributable deviation](../requirements/system/visible-attributable-deviation.md){id=note:req:64eknb1}
