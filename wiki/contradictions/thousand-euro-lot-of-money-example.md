---
type: Contradiction
title: "1000 EUR: a lot of money or not"
description: Worked example of a frame-variable conflict over a gradable predicate, resolvable only by parameterization or by stipulating a threshold that converts the claim's class.
tags: [contradiction, example, frame-variable, vague-predicate]
status: stable
generated: { by: hermes-agent/qwen3.8-flash, at: 2026-09-03T00:00:00Z }
claims:
  - id: not-a-lot
    statement: "1000 EUR is not a lot of money."
    source: this conversation
    scope: "speaker's comparison standard unstated (unspecified)"
    class: frame-variable
    actor: human:coworker-a
    at: 2026-09-03T00:00:00Z
  - id: is-a-lot
    statement: "1000 EUR is a lot of money."
    source: this conversation
    scope: "speaker's comparison standard unstated (unspecified)"
    class: frame-variable
    actor: human:coworker-b
    at: 2026-09-03T00:00:00Z
resolution: resolved
resolved_by: "parameterization — both kept as conditional claims; residual vagueness addressed by threshold stipulation, which converts class"
sources:
  - id: conversation
    resource: this conversation
    title: Taxonomy test case from user
    author: human:user
    last_modified: 2026-09-03T00:00:00Z
---

# 1000 EUR: a lot of money or not

## Summary

Two speakers call the same sum — 1000 EUR — "not a lot" and "a lot".
Classified **frame-variable (class 3)**: "a lot" is a gradable predicate whose
standard of comparison (whose income, which purchase, which country, which
year) is left implicit, so both claims can be true at once. Unlike the
sky-blue/grey case, a residual remains even after parameterization: if two
speakers share the full frame and still disagree, the clash is not factual but
a difference of **standards** — unresolvable by evidence. The resolution
mechanism is *definition-conversion*: stipulate a threshold (e.g. "a lot = more
than 50% of monthly net income") and the claim becomes frame-fixed (class 2) or
necessary-given-definition (class 1), i.e. checkable. Filed as a worked
example; under workflow step 0 a live vault would record no dispute here.

## The disagreement

| | Claim A | Claim B |
|---|---|---|
| Statement | 1000 EUR is not a lot | 1000 EUR is a lot |
| Asserted by | coworker-a | coworker-b |
| Scope | unstated | unstated |
| Class | frame-variable | frame-variable |

## Evidence

### For not-a-lot
- True relative to high income, large purchases (a car, several months' rent),
  or historical prices. *(unverified — illustrative frames)*

### For is-a-lot
- True relative to low income, small purchases, or a minimum-wage monthly
  salary. *(unverified — illustrative frames)*

## Adjudication

**Step 1 — parameterize (dissolves the apparent conflict):** attach the frame
to each claim: "not a lot *for speaker A's monthly income / for a laptop
purchase*" vs. "a lot *for B's income / for a weekly shop*". Both survive;
neither is wrong.

**Step 2 — the residual (why this case beats the sky example):** "a lot" has no
sharp boundary. Two speakers with an identical complete frame can still
disagree without either being factually mistaken — the predicate is vague, not
the world. No observation settles it; only a **stipulation** does. Defining
"a lot := > X% of monthly net income" converts the claim's class — from
frame-variable judgment to a frame-fixed (or definitional) fact that data can
adjudicate.

**Vault rule this demonstrates:** when a contradiction's evidence stays
"unverified — illustrative" after parameterization, you are looking at a vague
predicate, not a live dispute. Record the agreed definition instead of leaving
`resolution: open` forever.

## Cross-links

- Protocol: [Contradiction Protocol](/concepts/contradiction-protocol.md)
- Taxonomy: [Claim Classes and Contradictions](/analyses/claim-classes-and-contradictions.md)
- Sibling example: [Sky colour: blue vs grey](/contradictions/sky-blue-vs-grey-example.md)
