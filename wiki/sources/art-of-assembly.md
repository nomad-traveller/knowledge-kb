---
type: Source Summary
title: The Art of Assembly Language (AoA)
description: Randall Hyde's classic 80x86/MASM assembly language textbook — 25 chapters + appendices.
resource: https://flint.cs.yale.edu/cs422/doc/art-of-asm/pdf/
tags: [art-of-assembly, assembly, 80x86, masm, seed-source]
status: stable
generated: { by: human:user, at: 2026-08-26T00:00:00Z }
sources:
  - id: aoa-site
    resource: https://flint.cs.yale.edu/cs422/doc/art-of-asm/pdf/
    title: The Art of Assembly Language (PDF mirror)
    author: human:randall-hyde
    last_modified: 1996-01-01T00:00:00Z
---

# The Art of Assembly Language (AoA)

*The Art of Assembly Language* by Randall Hyde is a comprehensive textbook teaching
80x86 assembly language programming using MASM and the UCR Standard Library. The full
PDF set (FORWARD, TOC, CH01–CH25, appendices B/C/D) was retrieved into
`raw/art_of_assembly/` (32 files, ~5.6 MB) on 2026-08-26.

## Structure (sections)

- **Section One** (Ch 1–4): Data representation, boolean algebra, system organization, memory layout
- **Section Two** (Ch 5–11): Variables/data structures, the 80x86 instruction set, UCR lib, MASM, arithmetic/logical ops, control structures, procedures
- **Section Three** (Ch 12–16): Advanced procedures, MS-DOS/BIOS I/O, floating point, strings, pattern matching
- **Section Four** (Ch 17–19): Interrupts/traps/exceptions, resident programs, processes/concurrency
- **Section Five** (Ch 20–24): PC hardware — keyboard, parallel/serial ports, video, game adapter
- **Section Six** (Ch 25): Program optimization
- **Appendices**: ASCII/IBM charset, annotated bibliography, keyboard scan codes, instruction set reference

## How it's integrated

Each chapter is summarized as a wiki concept under
`wiki/concepts/art_of_assembly/aoa-chNN-<slug>.md`, with provenance pointing back to
the exact source PDF. Cross-link hub pages: [80x86 architecture](/entities/80x86.md),
[MASM assembler](/concepts/masm-assembler.md).

See also the [AoA concept index](/concepts/art_of_assembly/).

## Navigation

* [AoA Chapter Index (hub)](/concepts/art_of_assembly/index.md)

Related: [Iczelion's Win32 Assembly Tutorials](sources/masm-tutorials.md) — Win32 protected-mode counterpart (80x86/MASM, Windows API, GUI, threading).
