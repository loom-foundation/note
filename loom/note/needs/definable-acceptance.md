---
id: note:need:fkbs761
name: Definable acceptance
kind: need
persona:
  - "[Product Owner](../personas/product-owner.md){id=note:persona:pd8w3kq}"
  - "[Systems Engineer](../personas/systems-engineer.md){id=note:persona:25fdjrx}"
status: current
validation: observed
---

A Product Owner can state, in their own words and before any build, the conditions that define when a requirement is satisfied, as a standalone artifact they can show, hand off, and sign off against.
When those conditions can only be written into the procedure that later confirms them, authored in a different register and often by a different party against a mechanism the requirement never named, the persona loses the one statement of intent that should have predated and outlived the build.

## Source

The persona evidence is grounded in the three-persona analysis behind the acceptance-criterion design: a Product Owner authors acceptance criteria as their primary artifact, solution-free and before any build, to fix what the team is being asked to deliver; a verification engineer authors the check later, in a different register and against a chosen mechanism; across a startup lead (where the two roles collapse onto one person) and a regulated systems engineer (where they are separate people governed by different standards), the criterion and the check emerged as distinct artifacts with distinct moments of authorship.
The need is therefore marked `observed` against those three personas.

This need is distinct from [Unambiguous, testable requirements](unambiguous-testable-requirements.md){id=note:need:e4k9w2n}, which concerns the requirement's own phrasing being unambiguous and carrying a testable condition; this need concerns the acceptance criterion as a standalone artifact authored before build.

## Illustrative situations

1. **Product Owner signs off a feature.**
   Before any implementation begins, the owner writes the condition: "a user with no existing session can complete onboarding without contacting support."
   That statement is their sign-off instrument; the verification that later runs a test against it is a different thing, authored by a different party.

2. **Regulated systems engineer.**
   A systems engineer authors an acceptance condition per requirement at requirement-capture time, as mandated by their standard.
   The test procedure is a downstream artifact; the condition is the contractual statement of what acceptable means.

3. **Founder holding both roles.**
   A founder who is simultaneously the Product Owner and the Systems Engineer for a requirement writes the acceptance condition before any implementation begins.
   That pre-build condition gives them a clearer check to run later and a record of what was intended, separate from the executable procedure they also author.
