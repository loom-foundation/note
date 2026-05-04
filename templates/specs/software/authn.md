---
id: <namespace>:spec:<opaque>
name: <Name>
kind: specification
status: draft
authority: []
---

This specification defines the authentication surface for <scope>: the methods and policies by which the system verifies a claimed identity at access time.

## Identity providers

<List each accepted IdP: first-party credential databases, federated OIDC providers, SAML 2.0 identity providers, enterprise SSO. For workload identity (service-to-service), declare the mechanism (SPIFFE, mTLS, signed JWTs) or state `N/A, no workload-identity surface`.>

## Authentication factors

<List each supported factor: passwords, passkeys (WebAuthn), TOTP, SMS OTP, push notification, magic link. Note each factor's AAL contribution per NIST SP 800-63B.>

## Session model

```yaml
token_type:               # one of: opaque | jwt | paseto
access_lifetime_seconds:  # integer
refresh_lifetime_seconds: # integer; 0 = no refresh
refresh_rotation:         # one of: none | sliding | absolute
revocation_mechanism:     # short string naming the mechanism
binding:                  # one of: none | device | dpop | mtls
```

## Multi-factor policy

<Table of MFA rules. NIST SP 800-63B governs AAL definitions.>

| Trigger | Required AAL | Allowed factors | Grace period |
|---|---|---|---|
| <trigger> | <AAL1\|AAL2\|AAL3> | <factor list> | <duration or none> |

## Step-up triggers

<Table of operations requiring re-authentication at higher AAL (password change, consent grant, sensitive actions). Same column shape as multi-factor policy.>

| Trigger | Required AAL | Allowed factors | Grace period |
|---|---|---|---|
| <trigger> | <AAL1\|AAL2\|AAL3> | <factor list> | <duration or none> |

## API key and service-account model

<Key format, scope binding, rotation policy, leak-detection posture, prefixing convention. State `N/A, no programmatic access` if not applicable.>

## Account recovery

<Recovery channels, AAL required during recovery, lockout policy, evidence retained. Account recovery is a primary site of AAL collapse and a frequent attack surface; do not mark N/A without justification.>

## Federation

<Federation flows in use: OIDC Core 1.0, OAuth 2.0 (RFC 6749), OAuth Token Exchange (RFC 8693), SAML 2.0, WebAuthn (W3C Recommendation). Cite each protocol by name and RFC or W3C identifier; no vendor SDK prescribed.>

## Logout and session termination

<Global logout, single-device logout, OIDC back-channel logout, revocation propagation timing.>

## Impersonation and delegation

<`act_as` flow, OAuth Token Exchange (RFC 8693) profile, or `N/A`. When supported: name who may impersonate whom, the scope inherited, and how audit captures it. Authorization decisions for impersonation are out of scope here; only the authentication mechanism is recorded.>

## Rationale

<Optional. Record only design choices this spec makes that neither NIST SP 800-63B nor the cited protocol RFCs prescribe; one line per choice. Omit this section if no such choices were made.>

## Relations

- satisfies: [<Requirement>](../../requirements/system/<requirement>.md){id=<namespace>:req:<opaque>}
