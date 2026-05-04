---
id: <namespace>:spec:<opaque>
name: <Name>
kind: specification
status: draft
authority: []
---

This specification governs the identity-proofing flow by which the system establishes that a claimed identity corresponds to a real-world person or organization.

## Assurance level

<IAL1 | IAL2 | IAL3>
<!-- State the target IAL token and a one-line justification anchored to the project's risk and regulatory context. NIST SP 800-63A defines the three levels. -->

## Identity claims required

```yaml
claims:
  - <legal-name | address | date-of-birth | nationality | government-id | ...>
```
<!-- List every claim the flow collects. OpenID Connect for Identity Assurance (OIDC4IDA) provides standard claim vocabulary. -->

## Proofing methods accepted

| Method | Claims verified |
|---|---|
| <government-issued ID / biometric liveness / bank-statement letter / employer attestation / in-person check> | <claim, claim> |

<!-- One row per accepted method. Each method must map to at least one claim in the table above. -->

## Evidence requirements

```yaml
evidence:
  <method>:
    captures:
      - <image | scan | attestation-chain | signed-result | ...>
```
<!-- State what the proofing service captures per method. Do not describe the storage mechanism here; that belongs in Evidence retention. -->

## Evidence retention

```yaml
retention:
  <method>:
    what: <description of retained artifact>
    window: <duration, e.g. 7 years>
    jurisdiction: <jurisdiction>
```
<!-- Retention windows and jurisdictions must align with the project's privacy data inventory for the categories captured. -->

## Verifier or provider

<first-party human review | third-party provider | hybrid>
<!-- Name the provider or describe the first-party process. State whether the decision is automated, human-reviewed, or both. -->

## Re-proofing triggers

- <legal-name change>
- <address change>
- <dormancy threshold, e.g. 24 months inactive>
- <regulatory anniversary>
- <suspected compromise>
<!-- List conditions that require this flow to re-run. -->

## Rejection criteria

<Describe what fails the check and what happens next: manual review queue, fallback flow, or hard reject.>

## Relations

- satisfies: [<Requirement>](../../requirements/system/<requirement>.md){id=<namespace>:req:<opaque>}
