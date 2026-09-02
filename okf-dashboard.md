---
type: Reference
title: OKF Knowledge Base Dashboard
description: Live overview of the bundle, rendered by the Dataview plugin.
status: stable
---

# OKF Knowledge Base Dashboard

> Requires the **Dataview** community plugin (already enabled in `.obsidian/community-plugins.json`).

## Pages by type

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

## Untagged pages (data gap)

```dataview
LIST FROM "wiki" WHERE !tags AND type
```

## Stale pages

```dataview
LIST FROM "wiki" WHERE stale_after AND date(stale_after) <= date(now)
```