# knowledge-kb

An Open Knowledge Format (OKF) v0.2 knowledge base maintained with the
LLM-wiki pattern (Karpathy): a persistent, interlinked wiki that compounds
knowledge over time — written and extended collaboratively by humans and
LLM agents.

- `AGENTS.md` — schema + agent rules (frontmatter, workflows, lint rules)
- `wiki/` — the knowledge base: `concepts/`, `entities/`, `sources/`,
  `analyses/`, `references/`, plus `index.md` (catalog) and `log.md` (audit log)
- `raw/` — immutable source material; `raw/inbox/` for unprocessed notes
- `templates/` — mandatory page skeletons (`concept.md`, `source.md`,
  `entity.md`, `analysis.md`)
- `tools/okf.py` — linter and index builder

## Working with the repo

```bash
git clone https://github.com/nomad-traveller/knowledge-kb.git
cd knowledge-kb
python3 tools/okf.py lint           # check before committing
python3 tools/okf.py rebuild-index  # regenerate wiki/index.md after changes
```

## Workflows (short form — see AGENTS.md for details)

1. **Ingest**: put source material in `raw/`, write a summary page in
   `wiki/sources/`, update related concepts/entities/analyses with
   cross-links, rebuild the index, append to `wiki/log.md`.
2. **Inbox**: quick notes and brain dumps go in `raw/inbox/`; refactor them
   into `wiki/concepts/` drafts, then move the note to
   `raw/inbox/processed/`.
3. **Query**: read `wiki/index.md` first, drill into relevant pages,
   synthesize with citations; file durable answers as analyses.

Hard rules: never cite sources not in `raw/` or the page's frontmatter;
pages with unverified claims stay `status: draft`; every page body begins
with a `## Summary` section.