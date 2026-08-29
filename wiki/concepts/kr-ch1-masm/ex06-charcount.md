---
type: Source Summary
title: Ex06 Charcount
description: 32-bit MASM equivalent of K&R Chapter 1 example.
tags: [c, masm, kandr, tutorial]
status: stable
generated: { by: agent/hermes, at: 2026-08-27T00:00:00Z }
sources:
  - id: kandr-ch1-ex06-charcount
    resource: "wiki/concepts/kr-ch1-masm/ex06-charcount.md"
    title: "Ex06 Charcount"
    usage_count: 1
---

; ============================================================================
; kandr-ch1-ex06-charcount.asm
; K&R Ch 1.5.2: Count characters in input
;
; C original:
;   #include <stdio.h>
;   main() {
;       long nc;
;       nc = 0;
;       while (getchar() != EOF)
;           ++nc;
;       printf("%ld\n", nc);;   }\n;
; MASM equivalent — counts bytes read from stdin until read() returns 0.
; ============================================================================

.386
.model flat, c

.data
    ch    byte  ?
    nc    dd  0
    fmt   byte  "%d\n", 0

.code
main proc
    push    ebp
    mov     ebp, esp

    xor     eax, eax
    mov     nc, eax

.loop:
    ; read one byte from stdin (fd 0)
    push    1
    push    offset ch
    push    0
    call    @stdcall read
    add     esp, 12
    test    eax, eax
    jz      .done

    ; ++nc
    mov     eax, nc
    inc     eax
    mov     nc, eax
    jmp     .loop

.done:
    ; print nc
    pop     ebp
    ret
main endp

end main


