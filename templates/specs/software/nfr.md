---
id: <namespace>:spec:<opaque>
name: <Name>
kind: specification
status: draft
authority:
  - contracts/nfr/<service>.openslo.yaml
---

This specification states the measurable quality targets the system must meet and the degradation behavior that governs when those targets cannot be held.

## Authority

The SLIs and SLOs for this service are expressed in the OpenSLO document named in the `authority` field.
OpenSLO (governance-soft as of this writing) is treated as a derived export rather than a binding ratified standard; the file governs on any divergence with prose here.
Conformance of a running implementation is a separate Verification and is not asserted by this specification.

The OpenSLO document covers the following quality dimensions; each corresponds to a named `SLO` object in that file:

- Latency: per-operation response-time targets (percentile and magnitude under stated load conditions).
- Availability: per-component uptime ratios and permitted downtime within a stated measurement window.
- Resource usage: per-component metric limits (memory, CPU, storage, connection counts).
- Throughput: per-operation sustained-load targets.

## Degradation

What the system must do when a dependency fails or a resource limit is exceeded.
The OpenSLO file records what the targets are; this section records how the system must behave when they cannot be met.

### Retry and backoff

| Condition | Retry strategy | Backoff | Max attempts |
|-----------|---------------|---------|--------------|
| <condition> | <strategy> | <backoff> | <n> |

Fill each row with one dependency-failure or limit-exceeded scenario; cite a specific condition, not a category.

### Fallback

| Condition | Fallback behavior |
|-----------|------------------|
| <condition> | <behavior> |

Fallback behavior is what the system returns or does when retries are exhausted or a dependency is unavailable; must be observable by the caller.

### Circuit breakers

| Dependency | Open threshold | Half-open probe | Reset window |
|------------|---------------|-----------------|--------------|
| <dependency> | <threshold> | <probe> | <window> |

Omit this table if the system applies no circuit-breaker pattern.

### Graceful degradation

| Condition | Degraded capability | Retained capability |
|-----------|--------------------|--------------------|
| <condition> | <what is dropped> | <what still works> |

State which features are dropped and which are retained when operating in a degraded state.
Informing practice: Google Site Reliability Engineering chapter on degradation and load shedding.

## Relations

- satisfies: [<Requirement>](../../requirements/system/<requirement>.md){id=<namespace>:req:<opaque>}
