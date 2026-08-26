---
type: Reference
title: Knowledge Base Overview
description: Orientation page for this OKF-based personal knowledge base.
status: stable
generated: { by: human:user, at: 2026-08-26T00:00:00Z }
---

# Overview

This is a personal knowledge base built on two complementary ideas:

1. **Google Open Knowledge Format (OKF)** — the *container*. A bundle of
   markdown files with YAML frontmatter. Every concept carries `type`,
   provenance (`sources`), trust (`generated`/`verified`), and lifecycle
   (`status`/`stale_after`) as first-class, machine-readable fields. See
   [Open Knowledge Format](concepts/open-knowledge-format.md).

2. **Karpathy's LLM Wiki pattern** — the *process*. Raw sources are immutable
   (in `raw/`). An LLM reads them and compiles/maintains an interlinked wiki
   (in `wiki/`), so knowledge compounds instead of being rediscovered on every
   query. See [LLM Wiki Pattern](concepts/llm-wiki-pattern.md).

## How to use it

- **Ingest**: drop a source into `raw/` and ask the LLM to process it. The LLM
  writes a `sources/<slug>.md` summary and updates relevant `entities/`,
  `concepts/`, and `analyses/` pages, then appends to `log.md`.
- **Query**: ask questions against the wiki; answers with durable value get
  filed back as new pages.
- **Lint**: periodically run `python3 tools/okf.py lint` to catch orphans,
  broken links, missing frontmatter, and stale concepts.

## What's here now

- `concepts/` — the two foundational ideas this base is built on.
- `sources/` — summaries of the seed materials (the two URLs provided).
- `entities/` — publishers/orgs referenced.
- `analyses/` — reserved for comparison/synthesis pages you produce over time.

See the [index](index.md) for the full catalog.

## Integrated corpora

* [The Art of Assembly Language](/concepts/art_of_assembly/index.md) — 25 chapter summaries integrated from PDFs in `raw/art_of_assembly/`.
