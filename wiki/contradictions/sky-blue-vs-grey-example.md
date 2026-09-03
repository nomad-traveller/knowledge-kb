---
type: Contradiction
title: "Sky colour: blue vs grey"
description: Worked example of a frame-variable apparent contradiction, resolved by making the frame explicit rather than picking a winner.
tags: [contradiction, example, frame-variable]
status: stable
generated: { by: hermes-agent/qwen3.8-flash, at: 2026-09-03T00:00:00Z }
claims:
  - id: sky-blue
    statement: "The sky is blue."
    source: this conversation
    scope: "clear-day observation, sun well above horizon, mid-latitude"
    class: frame-variable
    actor: human:user
    at: 2026-09-03T00:00:00Z
  - id: sky-not-blue
    statement: "It is cloudy, the sky is not blue."
    source: this conversation
    scope: "overcast conditions, same location, cloudy time"
    class: frame-variable
    actor: human:user
    at: 2026-09-03T00:00:00Z
resolution: resolved
resolved_by: "parameterization — both claims kept with explicit scope; no world-state where they co-occur"
sources:
  - id: conversation
    resource: this conversation
    title: Discussion on human contradiction detection and frames
    author: human:user
    last_modified: 2026-09-03T00:00:00Z
---

# Sky colour: blue vs grey

## Summary

Two claims — "the sky is blue" and "it is cloudy, the sky is not blue" — appear
to conflict but do not: each is true under different, stated conditions.
Classified as **frame-variable**, the conflict resolves by parameterization
(keep both, record the scope) rather than adjudication (pick a winner). This
page exists as the worked reference example for the `class`/`scope` fields in
Contradiction records.

## The disagreement

| | Claim A | Claim B |
|---|---|---|
| Statement | The sky is blue | The sky is not blue (cloudy) |
| Asserted by | human:user | human:user |
| Scope | clear day, sun up | overcast |
| Class | frame-variable | frame-variable |

## Evidence

### For sky-blue
- Rayleigh scattering produces a blue zenith on clear days; ordinary
  observation. *(unverified — common knowledge, no source cited)*

### For sky-not-blue
- Water droplets scatter all wavelengths roughly equally, producing
  grey/white overcast skies; ordinary observation. *(unverified)*

## Adjudication

**No adjudication was required — and that is the point.** Triage step 0 of the
[Contradiction Protocol](/concepts/contradiction-protocol.md) asks: *could both
be true under different conditions?* Yes: clear vs. overcast. Therefore this is
class 3 (frame-variable), the claims are complementary, not conflicting. The
"resolution" is the parameterized form: *the sky is blue on clear days and grey
when overcast* — strictly more informative than either original claim, and it
keeps both without declaring either side wrong.

Had the scopes been left unstated, a naive detector would flag this forever as
a live dispute between the same actor — the exact phantom-contradiction failure
mode the protocol warns about.

## Cross-links

- Protocol: [Contradiction Protocol](/concepts/contradiction-protocol.md)
- Taxonomy: [Claim Classes and Contradictions](/analyses/claim-classes-and-contradictions.md)
- Sibling example (harder case): [1000 EUR: a lot of money or not](/contradictions/thousand-euro-lot-of-money-example.md)
