---
type: Analysis
title: Claim Classes and Contradictions
description: A taxonomy of contradictions by claim modality — necessary, frame-fixed, frame-variable — and what each class implies for detection and resolution in this vault.
tags: [contradiction, epistemics, taxonomy, analysis]
status: stable
generated: { by: hermes-agent/qwen3.8-flash, at: 2026-09-03T00:00:00Z }
sources:
  - id: conversation
    resource: this conversation
    title: Discussion on human contradiction detection and frames (sky-blue example)
    author: human:user
    last_modified: 2026-09-03T00:00:00Z
  - id: protocol
    resource: wiki/concepts/contradiction-protocol.md
    title: Contradiction Protocol
---

# Claim Classes and Contradictions

## Summary

A contradiction is not one phenomenon but three, because claims differ in their
**modality**: *necessary* claims are true or false by definition alone (2+2=5 is
an error, not a dispute); *frame-fixed* claims depend on a world-state everyone
tacitly shares ("Berlin is Germany's capital" — one source is simply wrong or
outdated); *frame-variable* claims are true relative to context, so most apparent
conflicts dissolve once the frame is explicit ("the sky is blue" vs. "it's
cloudy" describe different world-states, not a disagreement).[^conversation]
Detection and resolution differ per class — and the dominant failure mode of a
knowledge base is **misclassification**: treating frame-variable claims as
frame-fixed produces false alarms that burn trust in the queue, while treating
frame-fixed claims as frame-variable lets real contradictions escape with a
hand-wave about "context." Triage must therefore check the frame *before*
adjudicating.

## The three classes

### 1. Necessary claims (frame-free)

True or false by definition, logic, or a formal system. No time, place, or
perspective changes them: "a bachelor is unmarried", the arithmetic of a unit
conversion given its definitions, `2 + 2 = 4`.

- **A "contradiction" here is an error**, not a dispute: one side is simply
  wrong. There is no fact of the world to check, only the system.
- **Detection:** mechanical where formalizable — *evaluate* the claim
  (arithmetic is computable; informal cases need a definition check).
- **Vault policy:** never file an open Contradiction page for this class. Amend
  or supersede the wrong page, log the fix. If a class-1 contradiction seems to
  *persist*, that is proof the claims were misclassified.

### 2. Frame-fixed contingent claims (shared world-state)

Contingent on how the world is, but the frame is tacit and common to all
parties: the actual world, today's date, an agreed definition. "Berlin is the
capital of Germany", "OKF v0.2 has 13 sections", "the approved dose is 50 mg".

- **Contradictions are genuine factual disputes:** at least one source is
  wrong, outdated, or miscopied — and that is checkable.
- **Detection:** pure comparison — same key, same recorded scope, different
  value. Mechanically tractable *only if the scope was written down*.
- **Resolution:** the trust hierarchy from the protocol — recency, primary
  before secondary, credibility signals (`author`, `usage_count`,
  `last_modified`), direct verification where possible. Close with
  `resolved_by`.
- **Decay warning:** frame-fixed claims silently slip toward class 3 as the
  world changes — capitals, laws, and APIs all move. "Berlin is the capital"
  (1985, West) vs. "East Berlin is the capital" (1985, East) is *not* a
  contradiction; a class-2 fact read as timeless is how phantom contradictions
  are generated later. `stale_after` exists precisely for this.

### 3. Frame-variable claims (context-relative)

Truth relative to conditions: time, place, observer, measurement setup, or the
definition in use. "The sky is blue." "Drug X is effective." "This wire gauge
is safe."[^conversation]

- **Most apparent contradictions dissolve** when the frame is made explicit:
  the claims were never about the same world-state. They are *complementary,
  not conflicting*.
- **Detection is impossible from text alone** — it needs scope extraction.
  If a claim carries no scope, the machine cannot judge; that is a schema gap,
  not a dispute.
- **Resolution:** *parameterize first* — rewrite both claims with explicit
  scope. Both may then survive as conditional knowledge ("blue under clear-day
  light; grey under overcast"), which is strictly richer than either original.
  What **still** conflicts after parameterization is a true contradiction, and
  it behaves like class 2.
- **Vault policy:** contested claims require a `scope` field — an unframed
  claim is an uncheckable claim.

## Triage order (agent workflow)

Order matters: check the frame *before* declaring a conflict.

1. **Could both be true under different conditions?** Probe the scope of each
   (when, where, measured how, which definition). If yes → class 3:
   parameterize, keep both, no Contradiction page.
2. **Is the truth fixed by definition or formal rule?** → class 1: evaluate,
   correct the wrong page, log an error — never an open contradiction.
3. **Same frame, mutually exclusive, both about the shared world?** → class 2:
   adjudicate via trust hierarchy, close with `resolved_by`.
4. **Cannot establish the frame at all?** → this is not a contradiction but an
   underspecification defect: flag the missing scope, set `status: draft`.

## Why misclassification is the real enemy

| Mistake | Consequence | Example |
|---|---|---|
| Class 3 → treated as 2 | **Phantom contradiction** — false alarms destroy trust in the queue | Flagging "sky blue" vs. "sky grey" |
| Class 2 → treated as 3 | **Missed contradiction** — a real conflict is waved away as "context" | Two 2024-protocol dose claims "might mean different countries" |
| Anything → treated as 1 | **Forced closure** — pretending a dispute is settled logic | "Both can't be right, delete the newer one" |

The dangerous asymmetry: phantom contradictions cost annoyance; missed
contradictions in load-bearing domains (dosage, wiring, load limits) cost
something real. That argues for recording scope *at write time*, so class-2
comparison stays mechanical and class-3 disputes resolve without guessing.

## Classification is dynamic

A claim's class can change as knowledge grows. Discovering a hidden parameter
reclassifies class 2 → 3 ("the dose is 50 mg" — ah, *per country*). Discovering
the frame was always shared reclassifies 3 → 2. Consequently: **before closing
any class-2 contradiction, run a class-3 investigation first** — most
"resolved by source authority" decisions in this vault would, on honest review,
turn out to have been frame clashes all along.

## Question

Asked in session: classify contradictions by claim modality — necessary,
frame-fixed, frame-variable — following the observation that humans resolve
"2+2=5" instantly, "Berlin as US capital" just as fast, but correctly refuse to
call "the sky is blue" vs. "it's cloudy" a contradiction.

## Conclusion

The taxonomy is operational, not decorative: it dictates the *procedure* per
conflict (evaluate → correct), (compare → adjudicate), (parameterize → keep
both), and it makes triage order — frame-check first — a rule, not a
disposition. The vault should classify every incoming contradiction before
routing it.

## Cross-links

- Protocol: [Contradiction Protocol](/concepts/contradiction-protocol.md)
- Related: [Knowledge Collaboration Workflow](/analyses/knowledge-collaboration-summary.md)

[^conversation]: Session discussion on human contradiction detection, 2026-09-03.
