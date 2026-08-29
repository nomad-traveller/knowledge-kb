---
type: Source Summary
title: Ex07 Linecount
description: 32-bit MASM equivalent of K&R Chapter 1 example.
tags: [c, masm, kandr, tutorial]
status: stable
generated: { by: agent/hermes, at: 2026-08-27T00:00:00Z }
sources:
  - id: kandr-ch1-ex07-linecount
    resource: "wiki/concepts/kr-ch1-masm/ex07-linecount.md"
    title: "Ex07 Linecount"
    usage_count: 1
---

; ============================================================================
; kandr-ch1-ex07-linecount.asm
; K&R Ch 1.5.3: Count lines in input
;
; C original:
;   #include <stdio.h>
;   main() {
;       int c, nl;
;       nl = 0;
;       while ((c = getchar()) != EOF)
;           if (c == '
')
;               ++nl;
;       printf("%d\n", nl);;   }\n;
; MASM equivalent — counts occurrences of byte 0x0A (newline) in stdin.
; ============================================================================

.386
.model flat, c

.data
    ch    byte  ?
    nl    dd  0

.code
main proc
    push    ebp
    mov     ebp, esp

    xor     eax, eax
    mov     nl, eax

.loop:
    ; c = getchar()
    push    1
    push    offset ch
    push    0
    call    @stdcall read
    add     esp, 12
    test    eax, eax
    jz      .done

    ; if (c == '
') ++nl;
    movzx   eax, ch
    cmp     al, 0Ah
    jne     .skip
    mov     eax, nl
    inc     eax
    mov     nl, eax
.skip:
    jmp     .loop

.done:
    pop     ebp
    ret
main endp

end main


