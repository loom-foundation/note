---
id: <namespace>:spec:<opaque>
name: <Name>
kind: specification
status: draft
authority: []
---

This specification defines the data-protection posture of <system name>.

## Applicable regimes

<!-- List each regime in scope: GDPR, CCPA, LGPD, PIPEDA, UK_DPA, or others. -->
<!-- If the system processes no personal data, state N/A and give a one-line justification. -->

<GDPR | CCPA | LGPD | PIPEDA | UK_DPA | N/A, <justification>>

## Lawful basis catalogue

<!-- One row per processing purpose; allowed Lawful basis values are listed below. -->
<!-- State N/A in every cell if no personal data is processed. -->

| Purpose | Lawful basis | Notes |
|---|---|---|
| <purpose> | <contract \| legitimate_interest \| consent \| legal_obligation \| vital_interest \| public_task> | <note> |

## Data inventory

<!-- One row per data category. -->
<!-- Residency: jurisdiction(s) where data is stored or transferred; N/A if no cross-border concern. -->
<!-- Special-category: true/false; flags GDPR Art. 9 data (health, biometrics, race, religion, political views). -->
<!-- Retention: duration or event trigger (e.g., "90 days after account deletion"). -->

| Category | Purpose | Lawful basis | Retention | Residency | Special-category |
|---|---|---|---|---|---|
| <category> | <purpose> | <lawful basis> | <retention> | <jurisdiction \| N/A> | <true \| false> |

## Consent topics

<!-- One row per topic where consent is the lawful basis. -->
<!-- Proof mechanism: how a valid consent record is captured and stored (ISO 27560 structures the record). -->
<!-- Revocation flow: the user journey and system action when consent is withdrawn. -->
<!-- State N/A, no consent-based processing if consent is not the lawful basis for any purpose. -->

| Topic | Granularity | Proof mechanism | Revocation flow |
|---|---|---|---|
| <topic> | <per-purpose \| bundled> | <mechanism; see ISO 27560> | <flow> |

## Data subject rights

<!-- One row per right. For GDPR-scoped systems, include all six rows below. -->
<!-- Verification: how the system confirms the requester is the data subject. -->
<!-- SLA: the calendar window for fulfilling the request (e.g., "30 days"). -->
<!-- Endpoint: the API or UI surface that accepts the request; use a descriptive label, not a readable export id. -->
<!-- The W3C Data Privacy Vocabulary provides a controlled vocabulary for right names and status terms. -->

| Right | Endpoint | Verification | SLA |
|---|---|---|---|
| Access (Art. 15) | <endpoint label> | <verification method> | <SLA> |
| Rectification (Art. 16) | <endpoint label> | <verification method> | <SLA> |
| Erasure (Art. 17) | <endpoint label> | <verification method> | <SLA> |
| Restriction (Art. 18) | <endpoint label> | <verification method> | <SLA> |
| Portability (Art. 20) | <endpoint label> | <verification method> | <SLA> |
| Objection (Art. 21) | <endpoint label> | <verification method> | <SLA> |

## Retention policies

<!-- One block per data category from the data inventory. -->
<!-- State the deletion trigger, the archive trigger (if any), and the enforcement mechanism. -->

```yaml
- category: <category>
  delete_after: <duration or event>
  archive_after: <duration or event | none>
  trigger: <cron | event | manual | N/A>
  enforced_by: <migration, job name, or storage-layer policy>
```

## Cross-border transfer mechanism

<!-- State the mechanism used for each cross-border transfer, or N/A if none occurs. -->
<!-- Allowed values: SCCs, adequacy_decision, BCRs, derogation, N/A. -->

```yaml
- receiving_jurisdiction: <country or region>
  mechanism: <SCCs | adequacy_decision | BCRs | derogation | N/A>
  notes: <transfer tool reference or derogation basis>
```

## Breach notification

<!-- Timelines are measured from confirmed discovery of the breach. -->
<!-- Evidence retained: what records the controller keeps of the incident. -->

| Notification target | Window | Channel | Evidence retained |
|---|---|---|---|
| Supervisory authority (Art. 33) | <hours, e.g., 72 h> | <channel> | <records> |
| Data subjects (Art. 34) | <window, e.g., without undue delay> | <channel> | <records> |

## Children's data

<!-- State whether the system knowingly processes data of users below the regional age threshold. -->
<!-- GDPR Art. 8 default: 16; member-state minimums of 13 to 16 apply. -->
<!-- If yes: name the threshold and the parental-consent mechanism. -->
<!-- If no: state N/A. -->

<N/A, children's data is out of scope | Age threshold: <age>; parental-consent mechanism: <mechanism>>

## DPIA records

<!-- List completed Data Protection Impact Assessments (GDPR Art. 35) with their conclusions. -->
<!-- State N/A if no high-risk processing is in scope. -->

```yaml
- title: <DPIA title>
  date: <YYYY-MM-DD>
  scope: <brief scope description>
  conclusion: <approved | approved with measures | not approved>
  measures: <mitigation measures, or none>
```

## Relations

- satisfies: [<Requirement>](../../requirements/system/<requirement>.md){id=<namespace>:req:<opaque>}
