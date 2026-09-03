---
type: Concept
title: Contradiction Protocol
description: How this vault captures, adjudicates, and resolves disagreements between sources, agents, and pages instead of averaging them away.
tags: [contradiction, protocol, trust, epistemic]
status: stable
generated: { by: hermes-agent/hy4-preview, at: 2026-09-03T00:00:00Z }
sources:
  - id: okf-spec
    resource: raw/google-okf-spec.md
    title: Open Knowledge Format (OKF) v0.2 SPEC
    author: team:google-cloud
---

# Contradiction Protocol

## Summary

When two claims in this vault disagree, the disagreement is **recorded, not
averaged**. A conflict becomes either an inline `## Contradictions` entry (small,
local) or a dedicated `type: Contradiction` page (substantive, cross-cutting);
the affected pages are marked `status: draft` until the conflict is adjudicated.
Claims are attributed to the *actor that produced them*, because the most common
source of contradiction is not two papers disagreeing — it is the same agent
answering the same question twice, differently.[^okf-spec]

## Why this exists

An LLM-maintained wiki has a specific failure mode: knowledge is regenerated
rather than retrieved, so **the same question asked twice can produce two
different answers**. If both get filed, the vault silently contains two
mutually exclusive "facts," and whichever page an agent happens to read first
determines what it tells you. Nothing detects the drift.

Three distinct kinds of contradiction, which need different handling:

| Kind | Example | Captured as |
|---|---|---|
| **Source vs. source** | Two papers report different numbers | `## Contradictions` on the affected page, or a Contradiction page if load-bearing |
| **Agent vs. agent** | Different models/runs disagree on the same question | Contradiction page; each claim records its `actor` |
| **Agent vs. self** | You ask twice, get different answers | Contradiction page — this is the case the protocol exists for |

## The rules

1. **Never average.** "Some say X, others say Y, so probably somewhere between"
   destroys information. Record both, mark the conflict open.
2. **Attribute to the actor, not just the source.** `claims[].actor` records
   *who produced the claim* (`agent/hy4-preview`, `human:user`, `process:nightly`).
   Without this, agent-vs-self contradictions are invisible — they look like one
   claim with two sources.
3. **Conflict demotes trust.** Any page involved in an open contradiction stays
   `status: draft`. No unverified page gets to look settled.
4. **Open is a valid end state.** A contradiction nobody can resolve is still
   knowledge. Leave it open and say what would settle it — do not paper over it.
5. **Resolution is a separate event.** Adjudication updates `resolution` and
   `resolved_by`, appends to `wiki/log.md`, and restores `status: stable`.

## Thresholds

- **Inline `## Contradictions` entry** — the disagreement affects one page and
  does not change any downstream conclusion.
- **Dedicated Contradiction page** — the disagreement is load-bearing, spans
  several pages, or is an agent/self conflict (these always get a page, since
  they indicate drift rather than a genuine dispute in the literature).

## Workflow

1. **Detect** — a new answer conflicts with something already in the vault.
2. **Check** — search `wiki/index.md` and grep for `resolution: open` first.
   An existing open contradiction may already cover it; extend rather than duplicate.
3. **Capture** — inline entry, or copy `templates/contradiction.md` to
   `wiki/contradictions/<slug>.md`.
4. **Demote** — set affected pages to `status: draft`.
5. **Link** — add a cross-link from every affected page to the Contradiction page.
6. **Log** — `YYYY-MM-DD | create | wiki/contradictions/<slug>.md | <note>`
7. **Rebuild** — `python3 tools/okf.py rebuild-index`

## Adjudicating

Prefer, in this order:

1. The claim traceable to a primary source in `raw/` over one with no source.
2. The claim whose source has better credibility signals (`author`,
   `last_modified`, `usage_count`).[^okf-spec]
3. Direct measurement or a test you can actually run.
4. The more recent claim, when the domain genuinely moves fast.

Record *which* rule decided it in the Adjudication section. If none applies,
leave it `open`.

## Health check

`python3 tools/okf.py lint` reports:

- contradictions left `resolution: open` past `stale_after`
- `type: Contradiction` pages with fewer than two `claims` entries
- `resolution: resolved` with no `resolved_by`
- pages carrying inline contradictions but still `status: stable`

List everything open with: `python3 tools/okf.py contradictions`

[^okf-spec]: Open Knowledge Format v0.2 SPEC, §5 (provenance, trust, lifecycle).
