---
type: Concept
title: LLM Wiki Pattern
description: Karpathy's pattern for a persistent, LLM-maintained interlinked wiki that compounds knowledge over time.
tags: [llm, wiki, knowledge-management, pattern]
status: stable
generated: { by: human:user, at: 2026-08-26T00:00:00Z }
sources:
  - id: karpathy-llm-wiki
    resource: https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f
    title: LLM Wiki (Karpathy gist)
    author: human:karpathy
    last_modified: 2026-04-04T00:00:00Z
---

# LLM Wiki Pattern

Most LLM+document workflows are **RAG**: upload files, retrieve chunks at query
time, generate an answer. The LLM *rediscovers* knowledge from scratch every
question — nothing accumulates.[^karpathy-llm-wiki]

The LLM Wiki pattern is different. Instead of retrieving from raw documents at
query time, the LLM **incrementally builds and maintains a persistent wiki** —
a structured, interlinked set of markdown files that sits between you and the
raw sources. New sources are read, summarized, and integrated: entity pages
updated, topic summaries revised, contradictions flagged. Knowledge is
*compiled once and kept current*, not re-derived per query.[^karpathy-llm-wiki]

## Architecture (three layers)

1. **Raw sources** — immutable curated documents. The LLM reads but never
   modifies them. (This base: `raw/`.)
2. **The wiki** — LLM-generated markdown. Summaries, entity/concept/analysis
   pages. The LLM owns it. (This base: `wiki/`.)
3. **The schema** — a config doc (e.g. `AGENTS.md`) telling the LLM the
   structure, conventions, and workflows. (This base: `AGENTS.md`.)

## Operations

- **Ingest**: drop a source, LLM reads it, writes a summary page, updates the
  index, updates cross-referenced pages, appends to `log.md`.
- **Query**: ask against the wiki; good answers get filed back as new pages so
  explorations compound too.
- **Lint**: periodically health-check for contradictions, stale claims, orphan
  pages, and missing cross-references.

## Why pair it with OKF

Karpathy's pattern is about *process*; OKF is about *format*. OKF's
provenance/trust/lifecycle frontmatter is exactly the "proof layer" critics
note is missing — each wiki page records how it was verified.

[^karpathy-llm-wiki]: LLM Wiki (Karpathy gist)

## Seed references

- Source summary: [Karpathy — LLM Wiki](/sources/karpathy-llm-wiki.md)
