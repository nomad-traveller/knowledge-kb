# Knowledge Base Update Log

## 2026-08-29
* **Maintenance**: Fixed 10 orphan pages under `wiki/concepts/kr-ch1-masm/` by adding inbound links from the directory index; removed duplicate `raw/masm-tutorials 1.docx`; cleaned duplicated/incomplete log entries; rebuilt `wiki/index.md`.

## 2026-08-27 (Iczelion MASM tutorials ingestion)
* **Ingestion**: Added source `raw/masm-tutorials.docx` (Iczelion's 35-part Win32 assembly tutorial series, ~568,082 bytes).
* **Creation**: Source summary `wiki/sources/masm-tutorials.md`.

## 2026-08-27 (C / K&R ingestion)
* **Ingestion**: Added source `raw/ansi_c_kernighan_ritchie.pdf` (Kernighan & Ritchie, 2nd ed., 238 pages, 2.9 MB).
* **Creation**: Source summary `wiki/sources/ansi_c_kernighan_ritchie.md`.

## 2026-08-27 (K&R Ch 1 MASM translation)
* **Creation**: 10 MASM equivalents of K&R Ch 1 C examples under `wiki/concepts/kr-ch1-masm/` (ex01–ex10 + index).
* **Cross-link**: From `wiki/sources/ansi_c_kernighan_ritchie.md`.

## 2026-08-26 (Art of Assembly integration)
* **Ingestion**: Retrieved 32 PDFs of Randall Hyde's *The Art of Assembly Language* into `raw/art_of_assembly/` (FORWARD, TOC, CH01-25, APNDX B/C/D).
* **Creation**: Added source summary `sources/art-of-assembly.md`, 25 chapter concept pages under `wiki/concepts/art_of_assembly/`, a hub index, entities (80x86, Randall Hyde), and `concepts/masm-assembler.md`.
* **Validation**: `tools/okf.py validate` (35 concepts, 0 errors) and `lint` (0 problems) pass.

## 2026-08-26 (Initialization)
* **Initialization**: Created OKF v0.2 bundle structure under `wiki/` with `raw/` source layer and `tools/okf.py`.
* **Creation**: Seeded foundational concepts ([Open Knowledge Format](concepts/open-knowledge-format.md), [LLM Wiki Pattern](concepts/llm-wiki-pattern.md)).
* **Creation**: Seeded source pages for [Karpathy llm-wiki](sources/karpathy-llm-wiki.md) and [Google OKF SPEC](sources/google-okf-spec.md).