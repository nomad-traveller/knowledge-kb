# Knowledge Base Update Log

## 2026-08-26
* **Initialization**: Created OKF v0.2 bundle structure under `wiki/` with `raw/` source layer and `tools/okf.py`.
* **Creation**: Seeded foundational concepts ([Open Knowledge Format](concepts/open-knowledge-format.md), [LLM Wiki Pattern](concepts/llm-wiki-pattern.md)).
* **Creation**: Seeded source pages for [Karpathy llm-wiki](sources/karpathy-llm-wiki.md) and [Google OKF SPEC](sources/google-okf-spec.md).
## 2026-08-26 (Art of Assembly integration)
* **Ingestion**: Retrieved 32 PDFs of Randall Hyde's *The Art of Assembly Language* into `raw/art_of_assembly/` (FORWARD, TOC, CH01-25, APNDX B/C/D).
* **Creation**: Added source summary `sources/art-of-assembly.md`, 25 chapter concept pages under `wiki/concepts/art_of_assembly/`, a hub index, entities (80x86, Randall Hyde), and `concepts/masm-assembler.md`.
* **Validation**: `tools/okf.py validate` (35 concepts, 0 errors) and `lint` (0 problems) pass.
