---
id: note:need:257yf29
name: State a shared obligation once
kind: need
persona:
  - "[Organization or Platform Owner](../personas/organization-owner.md){id=note:persona:6ek4j8b}"
  - "[Adopter](../personas/adopter.md){id=note:persona:n66rj1d}"
  - "[Reviewer or Auditor](../personas/reviewer-auditor.md){id=note:persona:9jz2a3w}"
status: current
validation: inferred
---

When an obligation applies across many teams or products, an Organization or Platform Owner wants to state it once and have it hold wherever it is in force, with every exception explicit, so policies are not copy-pasted and silently drift apart.
The units beneath, each run by an Adopter, want to inherit that obligation as-is, specialize or adjust it to their specific needs, or exclude it entirely, with every departure from the baseline explained and recorded. A Reviewer or Auditor wants every departure visible and accounted for rather than discovered by chance.

## Illustrative situations

These shaped the need and are kept here, in the problem space, rather than restated in the requirements they motivate;
they are inferred from common organizational patterns, not observed by us.

1. **Regulated subsidiary (strengthen, then opt out).**
   A holding company sets data retention at two years organization-wide.
   An audit subsidiary operating under SOX strengthens it to seven years.
   An ephemeral-sandbox application that handles only throwaway session data opts out entirely, because retention would be a category error.
   With inheritance the organization states retention once;
   the seven-year strengthening and the opt-out are each explicit and justified at their own level.

2. **Mono-repo with a shared baseline (replace / extend per product).**
   A security and data-handling baseline applies to every service in the repo.
   A payments service layers PCI obligations on top;
   a public marketing site opts out of rules that do not apply to it.
   The baseline is authored once at the root.

3. **Platform standards inherited by app teams.**
   A platform team defines auth, logging, and observability standards inherited by every application team;
   an app overrides a standard only where it has a recorded, justified exception.

4. **Cross-cutting concern across divisions (multi-parent).**
   A privacy / GDPR requirement applies to several products that live under *different* divisions.
   A given product therefore inherits both from its structural parent (its division) and from the cross-cutting privacy concern owned elsewhere.
   This is why a product may need to inherit from more than one parent at once, rather than from a single line of ancestry.

5. **Incubator with many entities and apps.**
   An incubator defines common policies once at the root (Privacy, GDPR, data-lifecycle management, right-to-be-forgotten), reused by most entities and their apps.
   Each entity can opt out, change parameters, or extend the policies further as its product needs dictate.
   (When an entity is funded and spun out into an independent company, the intent it inherited must travel with it;
   that portability is captured separately by
   [Self-contained extraction of inherited intent](../requirements/stakeholder/self-contained-extraction.md){id=note:req:qq6eywy}.)

6. **Nested organizations.**
   A parent organization with multiple child organizations, which in turn have departments and multiple systems or apps, needs the same state-once / inherit / deviate flexibility cascading down the chain.

## Source

That duplicated facts drift is established (the single-source-of-truth and DRY traditions).

That organizations need to state shared obligations once across many units, with cross-cutting concerns, is inferred from common organizational patterns: holding-company and regulated-subsidiary structures, a mono-repo baseline of shared standards, platform-standards ownership, incubator setups, and nested organizations.

Tier is `inferred` to reflect the organizational claim rather than the underlying drift mechanism.

This need is distinct from [Operate one corpus across many repositories](operate-corpus-across-repositories.md){id=note:need:03gs33j}, which concerns federation across repository boundaries, resolving references across separately-owned repositories; this need concerns single-source via the scope graph, an obligation stated once high and inherited by the units below.
