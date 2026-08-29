---
type: Source Summary
title: Ex05 Filecopy
description: 32-bit MASM equivalent of K&R Chapter 1 example.
tags: [c, masm, kandr, tutorial]
status: stable
generated: { by: agent/hermes, at: 2026-08-27T00:00:00Z }
sources:
  - id: kandr-ch1-ex05-filecopy
    resource: "wiki/concepts/kr-ch1-masm/ex05-filecopy.md"
    title: "Ex05 Filecopy"
    usage_count: 1
---

; ============================================================================
; kandr-ch1-ex05-filecopy.asm
; K&R Ch 1.5.1: Copy stdin to stdout, one character at a time
;
; C original (1st version):
;   #include <stdio.h>
;   main() {
;       int c;
;       c = getchar();
;       while (c != EOF) {
;           putchar(c);
;           c = getchar();
;       }
;   }
;
; C original (2nd version — canonical):
;   main() {
;       int c;
;       while ((c = getchar()) != EOF)
;           putchar(c);
;   }
;
; MASM equivalent — reads a byte from stdin (fd 0), writes to stdout (fd 1).
; EOF is signalled by read() returning 0 bytes.
; ============================================================================

.386
.model flat, c

.data
    ch    byte  ?

.code
main proc
    push    ebp
    mov     ebp, esp

.loop:
    ; c = getchar()  — read one byte from fd 0
    push    1                   ; count
    push    offset ch
    push    0                   ; fd = stdin
    call    @stdcall read
    add     esp, 12
    test    eax, eax
    jz      .done               ; eax == 0 → EOF

    ; putchar(c) — write one byte to fd 1
    push    1
    push    offset ch
    push    1                   ; fd = stdout
    call    @stdcall write
    add     esp, 12
    jmp     .loop

.done:
    pop     ebp
    ret
main endp

end main


