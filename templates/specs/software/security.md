---
id: <namespace>:spec:<opaque>
name: <Name>
kind: specification
status: draft
authority: []
---

The target security posture for <system or scope>, covering encryption obligations, transport hardening, data classification, and audit trail requirements.

## Encryption

<!-- One row per category of sensitive data the system handles. Both columns must be populated; empty cells are a specification error. Check completeness against OWASP ASVS Chapter 6 (Stored Cryptography) and Chapter 9 (Communications). -->

| Data | At Rest | In Transit | Notes |
|------|---------|------------|-------|
| <data category> | <algorithm or standard> | <protocol and version> | <any exception or context> |

## Security Headers

<!-- One row per HTTP security header the system must set. Concrete values are practitioner decisions; the table structure is required. Check completeness against OWASP ASVS Chapter 14 (Configuration) and the OWASP Secure Headers Project. -->

| Header | Value | Purpose |
|--------|-------|---------|
| <header name> | <required value or policy> | <one-line rationale> |

## Data Classification

<!-- One row per classification tier. Every data category handled by the system must be assigned a tier. Classification levels and handling rules are practitioner decisions. -->

| Classification | Examples | Handling Rules |
|----------------|----------|----------------|
| <tier name> | <example data types> | <access, storage, transmission, and disposal rules> |

## Audit Trail

<!-- One row per security-relevant event that must be logged. Events, fields, and retention durations are practitioner decisions. Check completeness against OWASP ASVS Chapter 7 (Error Handling and Logging). -->

| Event | Data Captured | Retention |
|-------|---------------|-----------|
| <event name> | <fields logged> | <duration> |

## Compliance Mapping

<!-- Conditional: include only when a compliance framework (GDPR, SOC 2, HIPAA, PCI-DSS, or similar) applies. Map each section above to the relevant framework controls. Where a framework binds, use OSCAL to express the machine-readable control mapping. Omit this section when no framework applies. -->

| Framework | Control | Addressed By |
|-----------|---------|--------------|
| <framework name and version> | <control id and title> | <section or row above> |

## Rationale

<!-- Include only where the design makes a choice the requirement leaves open. One line per non-obvious decision. -->

- <design choice>: <one-line reason>

## Relations

- satisfies: [<Requirement>](../../requirements/system/<requirement>.md){id=<namespace>:req:<opaque>}
