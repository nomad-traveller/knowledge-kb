---
type: Source Summary
title: The ANSI C Programming Language
description: The definitive reference for the C programming language — second edition (ANSI C / C89) by Kernighan and Ritchie.
tags: [c, ansi-c, c89, programming-language, kernighan, ritchie, pointers, data-structures, stdio, posix]
status: stable
generated: { by: agent/hermes, at: 2026-08-27T00:00:00Z }
sources:
  - id: ansi-c-kernighan-ritchie
    resource: "raw/ansi_c_kernighan_ritchie.pdf"
    title: "The ANSI C Programming Language, Second Edition (1988)"
    author: "Brian W. Kernighan and Dennis M. Ritchie"
    usage_count: 1
---

# The ANSI C Programming Language (K&R, 2nd ed.)

**Authors:** Brian W. Kernighan (Bell Labs) and Dennis M. Ritchie (Bell Labs)
**Edition:** Second Edition, 1988 — the definitive ANSI C / C89 reference
**Source:** `raw/ansi_c_kernighan_ritchie.pdf` (238 pages, 2.9 MB)

K&R2 is the book everyone who knows C knows as "K&R". It replaced the first edition (1978) to reflect the ANSI standard (X3.159-1989). Every chapter is a mix of concise exposition and working code; the language is presented bottom-up (C's own approach), not top-down.

## Chapter Structure

| Ch  | Title                              | Pages     |
|-----|------------------------------------|-----------|
| 1   | A Tutorial Introduction            | 9 to 33   |
| 2   | Types, Operators, Expressions      | 35 to 50  |
| 3   | Flow Control                       | 52 to 61  |
| 4   | Functions and Program Structure    | 62 to 80  |
| 5   | Pointers and Arrays                | 83 to 113 |
| 6   | Structures                         | 114 to 134|
| 7   | Input and Output                   | 135 to 150|
| 8   | The UNIX System Interface          | 151 to 167|
| A   | Appendix A: The C Language Reference| 168 to 219|
| B   | Appendix B: Library Reference      | 220 to 238|

## Key Sections

### Ch 1 — Tutorial Introduction
Quick start: variables, arithmetic, for loops, symbolic constants (#define), I/O with getchar/putchar, arrays, functions, call-by-value, character arrays, external variables and scope. The classic "hello, world".

### Ch 2 — Types, Operators, Expressions
Data types and sizes, constants, declarations, arithmetic/relational/logical operators, type conversions (integer promotion, arithmetic conversions), increment/decrement, bitwise operators, assignment operators, conditional operator, operator precedence and order of evaluation.

### Ch 3 — Flow Control
If/else, else-if chains, switch, while, for, do-while, break, continue, goto.

### Ch 4 — Functions and Program Structure
Function basics, return types, external variables, scope rules, header files, static (local and file-scope), register, block structure, initialization, recursion, the C preprocessor (#define, #include, #ifdef, #line, #pragma, #error).

### Ch 5 — Pointers and Arrays
The hardest chapter in C. Pointers and addresses, pointer arguments, pointer/array duality, address arithmetic, character pointers and functions, pointer arrays, pointers to pointers, multi-dimensional arrays, command-line arguments, function pointers, complicated declarations.

### Ch 6 — Structures
Basic structs, structs and functions, arrays of structs, pointers to structs, self-referential structs (linked lists, trees), table lookups, typedef, unions, bit-fields.

### Ch 7 — Input and Output
stdio (fopen, fclose, fgets, fputs), printf/scanf formatted I/O, variable-length argument lists (stdarg.h), file access modes, stderr and error handling, line I/O, miscellaneous (sprintf, sscanf, perror, exit, rand, srand).

### Ch 8 — UNIX System Interface
File descriptors, low-level I/O (read/write), open/creat/close/unlink, random access (lseek), implementing fopen and getc on top, listing directories (opendir/readdir), a storage allocator. The Unix/POSIX bridge chapter.

### Appendix A — C Language Reference
Full ANSI C grammar in BNF, storage classes, type qualifiers, l-values, conversion rules, complete expression grammar (primary to postfix to unary to assignment to comma), declarations and declarators, statements, external declarations, scope and linkage, preprocessing rules, grammar productions.

### Appendix B — Library Reference
Full function listings for stdio.h, ctype.h, string.h, math.h, stdlib.h, assert.h, locale.h, setjmp.h, signal.h, time.h, limits.h, float.h.

## Notable Properties

- **C as a systems language:** deliberately thin. Ch 8 exposes the POSIX file API directly. The book treats C as an assembly language that happens to be portable.
- **ANSI C / C89 (1989):** strict typing, void parameters, const/volatile, enumerated types, function prototypes, void *.
- **Pointer-first design:** pointer model (Ch 5) is the conceptual core — arrays are pointers, strings are character pointers, functions return pointers.
- **Preprocessor as macro language:** Ch 4 and App A.12 document #define, #ifdef, #pragma — a second language inside C.

## Relation to the Other Sources in this Vault

| Topic      | C K&R              | AoA (x86)         | Iczelion (Win32)  |
|------------|--------------------|-------------------|-------------------|
| Abstraction| Portable systems   | Machine level      | Windows API        |
| Memory     | Compiler + OS      | Real/protected     | Flat 32-bit        |
| Use case   | Libraries, kernels | Low-level 8/16-bit| 32-bit Win GUI     |

K&R complements the x86 books: understanding C's memory model (pointers, structs, unions, sizeof, alignment) is essential when reading or writing assembly or when interfacing C with MASM/Win32 code. The typedef and struct patterns in Ch 6 map directly onto record-type thinking in Pascal/Hyde's AoA data structures.

See also: [Intel 80x86](/entities/80x86.md), [MASM Assembler](/concepts/masm-assembler.md), [Open Knowledge Format](/concepts/open-knowledge-format.md)

*K&R Ch 1 MASM translation:* [kandr-ch1-masm](/concepts/kr-ch1-masm/index.md) — 10 MASM equivalents of every C example in Ch 1.
