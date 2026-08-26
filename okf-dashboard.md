---
type: Reference
title: OKF Knowledge Base Dashboard
description: Live overview of the bundle, rendered by the Dataview plugin.
status: stable
generated: { by: human:user, at: 2026-08-26T00:00:00Z }
---

# OKF Knowledge Base Dashboard

> Requires the **Dataview** community plugin (already enabled in `.obsidian/community-plugins.json`).

## Concepts by type

```dataview
TABLE type, status, generated.by AS "author"
FROM "wiki"
WHERE type
SORT type ASC, file.name ASC
```

## Recent changes (by generated date)

```dataview
TABLE generated.at AS "created", type
FROM "wiki"
WHERE generated.at
SORT generated.at DESC
LIMIT 15
```

## Untagged concepts (data gap)

```dataview
LIST FROM "wiki" WHERE !tags AND type
```

## Stale concepts

```dataview
LIST FROM "wiki" WHERE stale_after AND date(stale_after) <= date(now)
```

## Art of Assembly — chapter map

```dataview
LIST FROM "wiki/concepts/art_of_assembly"
SORT file.name ASC
```
