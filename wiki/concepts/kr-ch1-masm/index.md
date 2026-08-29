---
type: Concept
title: K&R Ch 1 → MASM 32-bit
description: 32-bit MASM equivalents of every C example in Kernighan & Ritchie Chapter 1.
tags: [c, masm, kandr, tutorial, 80x86, 32-bit, protected-mode, flat-model, win32, didactic]
status: stable
generated: { by: agent/hermes, at: 2026-08-27T00:00:00Z }
sources:
  - id: kandr-ch1-c
    resource: "raw/ansi_c_kernighan_ritchie.pdf"
    title: "The ANSI C Programming Language, Ch 1"
  - id: iczelion-tut1
    resource: "raw/masm-tutorials.docx"
    title: "Iczelion Tutorial 1: The Basics"
---
# Dataview query

List of all MASM equivalents of K&R Chapter 1 examples:

```dataview
TABLE file.mtime as Modified, file.size as Size, file.tags as Tags
FROM "knowledge_base/wiki/concepts/kr-ch1-masm"
WHERE !contains(file.path, "index")
SORT file.mtime DESC
```

## Pages

- [ex01 – Hello World](/concepts/kr-ch1-masm/ex01-hello.md)
- [ex02 – Fahrenheit/Celsius table](/concepts/kr-ch1-masm/ex02-fahr-cel.md)
- [ex03 – For loop with floats](/concepts/kr-ch1-masm/ex03-for-float.md)
- [ex04 – Symbolic constants](/concepts/kr-ch1-masm/ex04-symbolic.md)
- [ex05 – File copy](/concepts/kr-ch1-masm/ex05-filecopy.md)
- [ex06 – Character count](/concepts/kr-ch1-masm/ex06-charcount.md)
- [ex07 – Line count](/concepts/kr-ch1-masm/ex07-linecount.md)
- [ex08 – Word count](/concepts/kr-ch1-masm/ex08-wordcount.md)
- [ex09 – Digit histogram](/concepts/kr-ch1-masm/ex09-digit-hist.md)
- [ex10 – Power function](/concepts/kr-ch1-masm/ex10-power.md)

# K&R Chapter 1 → 32-bit MASM Equivalents

This directory contains a **MASM translation** of every C example in K&R Chapter 1. Each `.asm` file is a standalone, syntactically valid MASM 32-bit source with a `C source` section as a comment header.

## Why this matters

K&R teaches C; the examples are portable and elegant. But when you're writing assembly — or debugging a C program compiled to assembly — you need to see the **concrete machine-level equivalent** of each construct. These files bridge that gap.

## Conventions

- **Calling convention:** `cdecl` (caller cleans the stack) for C interop; `stdcall` shown where Windows requires it
- **Memory model:** flat (Win32 32-bit, or protected-mode x86)
- **I/O:** POSIX `read`/`write` (fd 0/stdin, fd 1/stdin) for portability; Iczelion-style Win32 `WriteFile`/`ReadFile` noted where relevant
- **Integer width:** 32-bit (`dd`) throughout
- **Comment style:** `;` single-line (MASM standard)

## Files

| File                  | Section | C source                  | MASM features demonstrated                                                  |
| --------------------- | ------- | ------------------------- | --------------------------------------------------------------------------- |
| `ex01-hello.asm`      | 1.1     | hello world               | `.386`, `.model flat`, procedure, call, ret                                 |
| `ex02-fahr-cel.asm`   | 1.2     | while loop + integer math | `while` → `jg`/`jmp` pattern, `imul`/`idiv` (signed), `loop` via branch     |
| `ex03-for-float.asm`  | 1.3     | for + FPU                 | FPU stack (`fld`/`fmulp`), `for` → init/test/increment                      |
| `ex04-symbolic.asm`   | 1.4     | `#define` constants       | `equ` (equates), MASM constant mechanism                                    |
| `ex05-filecopy.asm`   | 1.5.1   | getchar/putchar loop      | `read`/`write` syscall, EOF detection (ret → 0)                             |
| `ex06-charcount.asm`  | 1.5.2   | character counter         | 32-bit counter, increment idiom                                             |
| `ex07-linecount.asm`  | 1.5.3   | newline counter           | byte comparison (0x0A), if-then branch                                      |
| `ex08-wordcount.asm`  | 1.5.4   | IN/OUT state machine      | state register, multi-branch, `equ` symbolic constants                      |
| `ex09-digit-hist.asm` | 1.6     | array indexing            | `dd 10 dup(0)`, indexed addressing, three-way branch                        |
| `ex10-power.asm`      | 1.7     | function call + loop      | cdecl calling convention, `[ebp+8]`/`[ebp+12]` parameter access, local vars |

## Key MASM idioms highlighted

### While loop → branch
```nasm
; C:  while (fahr <= upper) { body; fahr += step; }
.loop_start:
    cmp     eax, upper
    jg      .done          ; if (fahr > upper) goto done
    ; ... body ...
    add     fahr, step
    jmp     .loop_start    ; unconditional jump back
.done:
```

### For loop → init + while
```nasm
; C:  for (i = 0; i < 10; ++i) { body; }
    xor     ecx, ecx       ; i = 0
.loop:
    cmp     ecx, 10
    jge     .done
    ; ... body ...
    inc     ecx            ; ++i
    jmp     .loop
.done:
```

### `#define` → `equ`
```nasm
; C:  #define LOWER 0
LOWER equ 0
```

### Function call (cdecl) → `push` + `call` + `add esp`
```nasm
; C:  power(base, n)  — 2 args
push    n              ; push args right-to-left
push    base
call    power
add     esp, 8         ; caller cleans (cdecl)
```

### Array → `dup` + indexed addressing
```nasm
; C:  int ndigit[10];
ndigit dd 10 dup(0)

; C:  ndigit[c - '0']
movzx   ecx, c         ; index 0-9
lea     eax, ndigit
mov     eax, [eax + ecx*4]
```

### Local variables → frame pointer (`ebp`)
```nasm
; C:  int power(int base, int n) { int i, p; ... }
power proc
    push    ebp
    mov     ebp, esp
    ; base = [ebp+8]
    ;   n  = [ebp+12]
    ; local at [ebp-8], [ebp-12] etc.
    pop     ebp
    ret
power endp
```

## Relationship to the other sources

- **Hyde (AoA)** — Chapters 7-8 cover MASM directives and UCR standard library; see [AoA Ch 8](/concepts/art_of_assembly/aoa-ch08-masm-directives-pseudo-opcodes.md) for `.MODEL`, sections, and MASM syntax details
- **Iczelion Tut 1** — protected-mode Win32 basics (flat model, STDCALL, section directives); see [masm-tutorials](/sources/masm-tutorials.md) Tut 1
- **K&R Ch 2-4** — the remaining K&R chapters will be translated in future work (not in the vault yet)

## Usage

Each `.asm` file is a standalone MASM source. To assemble and link a minimal Win32 console program:

```
ml /c ex01-hello.asm          ; assemble
link /subsystem:console kernel32.lib user32.lib ex01-hello.obj
```

For the POSIX I/O versions (read/write), link against the C runtime instead of the Win32 API, or substitute `ReadFile`/`WriteFile` calls per Iczelion Tut 1.

See also: [MASM Assembler](/concepts/masm-assembler.md), [K&R Ch 1 source](/sources/ansi_c_kernighan_ritchie.md), [Iczelion Tutorial 1](/sources/masm-tutorials.md)
```
