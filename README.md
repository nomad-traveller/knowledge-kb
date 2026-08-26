# knowledge_base

A personal knowledge base built on **Google Open Knowledge Format (OKF) v0.2**,
maintained using **Karpathy's LLM Wiki pattern**.

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

`knowledge_base/` is a valid Obsidian vault (it contains `.obsidian/`). Open it directly,
or mirror it to another machine (see "Syncing to your MacBook" below).

- **Graph view**: colour-coded by category — concepts (purple), entities (red),
  sources (blue), analyses (green). Configure in `.obsidian/graph.json`.
- **Dataview dashboard**: open `okf-dashboard.md` (requires the Dataview plugin,
  already enabled). It shows concepts by type, recent changes, untagged/stale gaps,
  and the Art of Assembly chapter map — all live from frontmatter.
- **CSS snippet**: `okf.css` colour-codes the file explorer by folder. Enable via
  Settings → Appearance → CSS snippets → toggle "okf".
- **Markdown links**: `app.json` forces `useMarkdownLinks: true` so links stay
  portable (e.g. rsync/git) and OKF-bundle-relative (`/concepts/...`).

### Syncing to your MacBook Air
Either git-push/pull (recommended) or rsync over SSH:
```
rsync -avz --delete user@192.168.0.200:~/knowledge_base/ ~/knowledge_base/
```
Then open `~/knowledge_base` as a vault in Obsidian (desktop or mobile).
