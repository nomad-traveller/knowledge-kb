---
type: Reference
title: Overview
description: Orientation page for this OKF knowledge base template.
status: stable
---

# Overview

This is an **empty OKF v0.2 knowledge base template** — a ready-to-copy storage
vault for any topic. All topic content from the original demo (assembly, C,
natural units) has been removed; only the structural layer remains.

## How this vault is organized

- `raw/` — immutable sources you drop in (PDFs, markdown, exports)
- `wiki/sources/` — one summary page per ingested source
- `wiki/concepts/` — ideas, methods, patterns
- `wiki/entities/` — people, orgs, tools
- `wiki/analyses/` — syntheses and comparisons
- `wiki/references/` — external material, run instructions

The workflow (ingest → summarize → cross-link → index → log) is defined in
`AGENTS.md` at the vault root.

## What is already here

- [LLM Wiki Pattern](/concepts/llm-wiki-pattern.md) — the maintenance pattern itself.
- [Open Knowledge Format (OKF)](/concepts/open-knowledge-format.md) — the file format.
- [Karpathy — LLM Wiki](/sources/karpathy-llm-wiki.md) — origin essay (source kept in `raw/`).
- [Google OKF Specification](/sources/google-okf-spec.md) — the spec (source kept in `raw/`).
- [Google Cloud / knowledge-catalog](/entities/google-cloud.md) — OKF publisher.

## Starting a new topic vault

1. Copy this folder.
2. Add sources to `raw/` and let an agent ingest them per `AGENTS.md`.
3. Update this overview with the topic's scope and entry points.