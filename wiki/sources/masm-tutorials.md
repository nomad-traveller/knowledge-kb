---
type: Source Summary
title: Iczelion's Win32 Assembly Tutorials
description: 35-step Win32 assembly programming tutorial series — from basic skeleton programs through GUI, threading, DLLs, and debugging.
tags: [win32, assembly, masm, 80x86, 80386, windows-api, iclelions, gui, protected-mode]
status: stable
generated: { by: agent/hermes, at: 2026-08-27T00:00:00Z }
sources:
  - id: masm-tutorials-docx
    resource: "raw/masm-tutorials.docx"
    title: "Iczelion's Win32 Assembly Tutorials"
    usage_count: 1
---

# Iczelion's Win32 Assembly Tutorials

**Origin:** Iczelion's Win32 Assembly HomePage (Win32asm.org) — a classic numbered tutorial series that became the de-facto standard for Win32 assembly on Windows 95+. This .docx is the consolidated text of all 35 tutorials.

**File:** `raw/masm-tutorials.docx` — 568,082 bytes

This is the complementary counterpart to Randall Hyde's *The Art of Assembly Language* (see [AoA](sources/art-of-assembly.md)): Hyde covers x86 real-mode fundamentals and MASM; Iczelion's series shows how to build **protected-mode Windows GUI applications** with the same MASM assembler.

## Tutorial Index

| # | Title |
|---|-------|
| 1 | The Basics |
| 2 | MessageBox |
| 3 | A Simple Window |
| 4 | Painting with Text |
| 5 | More about Text |
| 6 | Keyboard Input |
| 7 | Mouse Input |
| 8 | Menu |
| 9 | Child Window Controls |
| 10 | Dialog Box as Main Window |
| 11 | More about Dialog Box |
| 12 | Memory Management and File I/O |
| 13 | Memory Mapped Files |
| 14 | Process |
| 15 | Multithreading Programming |
| 16 | Event Object |
| 17 | Dynamic Link Libraries |
| 18 | Common Controls |
| 19 | Tree View Control |
| 20 | Window Subclassing |
| 21 | Pipe |
| 22 | Superclassing |
| 23 | Tray Icon |
| 24 | Windows Hooks |
| 25 | Simple Bitmap |
| 26 | Splash Screen |
| 27 | Tooltip Control |
| 28 | Win32 Debug API Part 1 |
| 29 | Win32 Debug API Part 2 |
| 30 | Win32 Debug API part 3 |
| 31 | Listview Control |
| 32 | Multiple Document Interface (MDI) |
| 33 | RichEdit Control: Basics |
| 34 | RichEdit Control: More Text Operations |
| 35 | RichEdit Control: Syntax Hilighting |

## Topic Progression

1. **Foundations (Tut 1–2)** — skeleton program, `.MODEL flat,stdcall`, sections (`.DATA`, `.DATA?`, `.CONST`, `.CODE`), import libraries, ANSI vs Unicode, first MessageBox.
2. **Windows & GDI (Tut 3–7)** — window creation, WndProc, GDI text painting, keyboard and mouse input.
3. **GUI Controls (Tut 8–11, 18–19, 27, 31, 33–35)** — menus, dialogs, child windows, Common Controls, TreeView, tooltips, ListView, RichEdit (including syntax highlighting).
4. **System Programming (Tut 12–17, 21, 24)** — memory management, file I/O, memory-mapped files, processes, threads, event objects, DLLs, pipes, hooks.
5. **Advanced (Tut 20, 22–26, 28–30, 32)** — window superclassing, tray icons, Windows hooks, bitmaps, splash screens, Win32 Debug API (3 parts), MDI.

## Relationship to Art of Assembly Language

| Aspect | Hyde (AoA) | Iczelion |
|--------|-----------|----------|
| Mode | Real mode + protected mode | Protected mode (32-bit) |
| OS | MS-DOS / UCR standard library | Windows 95+ / Win32 API |
| Focus | 80x86 ISA, MASM syntax, real mode | Win32 API, GUI, threading, DLLs |
| Prerequisite | x86 fundamentals | AoA fundamentals |
| Assembler | MASM | MASM (same) |

Both series use MASM. AoA is the prerequisite for the register/memory model referenced throughout Iczelion's code; Iczelion then applies that foundation to the Windows protected-mode environment.

See also: [MASM Assembler](concepts/masm-assembler.md), [Intel 80x86](entities/80x86.md), [Open Knowledge Format](concepts/open-knowledge-format.md)
