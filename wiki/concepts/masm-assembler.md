---
type: Concept
title: MASM Assembler
description: Microsoft Macro Assembler — the assembler Randall Hyde uses to teach 80x86 assembly in AoA.
tags: [masm, assembler, 80x86, art-of-assembly]
status: stable
generated: { by: human:user, at: 2026-08-26T00:00:00Z }
sources:
  - id: aoa
    resource: https://flint.cs.yale.edu/cs422/doc/art-of-asm/pdf/CH08.PDF
    title: "AoA Ch8: MASM Directives & Pseudo-Opcodes"
    author: human:randall-hyde
---

# MASM Assembler

**MASM** (Microsoft Macro Assembler) is the assembler *The Art of Assembly Language*
uses to teach 80x86 programming. Beyond raw mnemonics it provides **directives and
pseudo-opcodes** for data definition, segmentation, macros, and procedure framing.
Covered in [AoA Ch8](/concepts/art_of_assembly/aoa-ch08-masm-directives-pseudo-opcodes.md).

## Why it matters

- Declares variables/data structures (see [AoA Ch5](/concepts/art_of_assembly/aoa-ch05-variables-and-data-structures.md)).
- Defines procedures/functions with parameter-passing conventions
  ([AoA Ch11](/concepts/art_of_assembly/aoa-ch11-procedures-and-functions.md)).
- The 80x86 instruction mnemonics it assembles are documented in
  [AoA Ch6](/concepts/art_of_assembly/aoa-ch06-the-80x86-instruction-set.md).

## Related

* [Intel 80x86 architecture](/entities/80x86.md)
* [The Art of Assembly Language (source)](/sources/art-of-assembly.md)

* [Iczelion's Win32 Assembly Tutorials](/sources/masm-tutorials.md)
* [The ANSI C Programming Language (K&R)](/sources/ansi_c_kernighan_ritchie.md)
