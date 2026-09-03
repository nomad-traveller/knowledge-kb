---
type: Contradiction
title: <Short description of the disagreement>
description: <One sentence: what is disputed and between what>
tags: [<contradiction>, <topic>]
status: draft
generated: { by: <agent>/<version>, at: <ISO8601Z> }
# --- contradiction fields ---
claims:
  - id: <claim-a>
    statement: <the claim as made>
    source: <sources[].id or page path>
    actor: <who/what asserted it, e.g. agent/hy4-preview>
    at: <ISO8601Z>
  - id: <claim-b>
    statement: <the competing claim>
    source: <sources[].id or page path>
    actor: <who/what asserted it>
    at: <ISO8601Z>
resolution: <open|resolved>          # open until adjudicated
resolved_by: <path or actor>         # required when resolution is resolved
sources:
  - id: <source-id>
    resource: <path in raw/ or URL>
    title: <Source Title>
---

# <Title>

## Summary

<One paragraph an agent can read alone: what is disputed, what each side says,
and whether it is still open.>

## The disagreement

Restate both claims neutrally. Do not blend them into a compromise statement —
the whole point of this page is that they have not been merged.

| | Claim A | Claim B |
|---|---|---|
| Statement | ... | ... |
| Asserted by | ... | ... |
| Source | ... | ... |
| When | ... | ... |

## Evidence

### For <claim-a>
- <evidence, attributed [^<source-id>]>

### For <claim-b>
- <evidence, attributed [^<source-id>]>

## Adjudication

<How this was decided, or what would decide it. If still open, state exactly
what observation, source, or test would settle it.>

## Cross-links

- Affected pages: [<Page>](/concepts/<page>.md)
- Sources: [<Source>](/sources/<source>.md)

[^<source-id>]: <citation>.
