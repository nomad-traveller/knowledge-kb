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
