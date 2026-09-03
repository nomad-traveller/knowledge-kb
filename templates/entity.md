---
type: Entity
title: <Entity Name>
description: <One sentence: who or what this entity is>
tags: [<entity>, <category>]
status: stable
generated: { by: <agent>/<version>, at: <ISO8601Z> }
sources:
  - id: <source-id>
    resource: <path in raw/ or URL>
    title: <Source Title>
    usage_count: 1
---

# <Entity Name>

## Summary

<One paragraph: identity, role, relevance to this vault.>

## Facts

- <Fact, attributed [^<source-id>]>

## Contradictions

<!-- Record disagreements here instead of averaging them away. Delete this
     block if none. One entry per conflict; keep 'status' current. -->
- **Claim:** <the statement that is disputed>
  - Opposed by: <the competing claim, source, or page>
  - Evidence: <what each side rests on>
  - status: <open|resolved>

## Cross-links

- [<Related Concept>](/concepts/<related>.md)

[^<source-id>]: <citation>.