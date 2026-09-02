---
type: Source Summary
title: Karpathy — LLM Wiki
description: Origin essay describing the LLM-maintained persistent wiki pattern.
resource: https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f
tags: [llm, wiki, seed-source]
status: stable
generated: { by: human:user, at: 2026-08-26T00:00:00Z }
sources:
  - id: original
    resource: https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f
    title: LLM Wiki (Karpathy gist)
    author: human:karpathy
    last_modified: 2026-04-04T00:00:00Z
---

# Karpathy — LLM Wiki

## Summary

Source essay by Andrej Karpathy (2026-04-04): *A pattern for building personal
knowledge bases using LLMs.* Defines the three-layer architecture (raw sources /
LLM-owned wiki / schema) and the ingest-query-lint operations. Full text retained
in `raw/karpathy-llm-wiki.md`.

## Key takeaways

- RAG re-derives knowledge per query; a maintained wiki compounds it.
- The wiki is an artifact the LLM writes and the human browses (e.g. in Obsidian).
- Good answers to queries should be filed back as new wiki pages.
- Periodic linting keeps the wiki consistent as it grows.

See [LLM Wiki Pattern](/concepts/llm-wiki-pattern.md) for the synthesized concept.
