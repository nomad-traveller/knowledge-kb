# Knowledge Base Template

A reusable, empty knowledge base built on **Google Open Knowledge Format (OKF) v0.2**,
maintained using **Karpathy's LLM Wiki pattern**. Copy this folder to start a new
topic vault; everything structural is included, no content is preset.

- `raw/`        — immutable source documents (you add, the LLM only reads)
- `wiki/`       — the OKF bundle: LLM-generated, interlinked markdown + frontmatter
  - `index.md`    catalog (regenerated)
  - `log.md`     change history
  - `overview.md` orientation
  - `sources/`, `entities/`, `concepts/`, `analyses/`, `references/`
- `AGENTS.md`   — the schema: how an LLM should ingest / query / lint this wiki
- `tools/okf.py`— OKF validator, index generator, and linter (no external deps)

## Quick start
1. Put a source (article, paper, pdf) into `raw/`.
2. Ask your LLM agent to ingest it (it follows `AGENTS.md`).
3. Browse `wiki/` — e.g. in Obsidian.
4. Periodically run:
   ```bash
   python3 tools/okf.py lint
   python3 tools/okf.py rebuild-index
   ```

## OKF in one line
A directory of markdown files; each has YAML frontmatter with `type`,
provenance (`sources`), trust (`generated`/`verified`), and lifecycle
(`status`/`stale_after`). Spec: https://github.com/GoogleCloudPlatform/knowledge-catalog/blob/main/okf/SPEC.md

## Obsidian integration

This folder is a valid Obsidian vault (it contains `.obsidian/`).

- **Graph view**: colour-coded by category — concepts (purple), entities (red),
  sources (blue), analyses (green). Configure in `.obsidian/graph.json`.
- **Dataview dashboard**: open `okf-dashboard.md` (requires the Dataview plugin,
  already enabled). It shows pages by type, recent changes, untagged/stale gaps —
  all live from frontmatter.
- **CSS snippet**: `okf.css` colour-codes the file explorer by folder. Enable via
  Settings → Appearance → CSS snippets → toggle "okf".
- **Markdown links**: `app.json` forces `useMarkdownLinks: true` so links stay
  portable (e.g. rsync/git) and OKF-bundle-relative (`/concepts/...`).