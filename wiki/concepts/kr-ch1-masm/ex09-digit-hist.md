---
type: Source Summary
title: Ex09 Digit Hist
description: 32-bit MASM equivalent of K&R Chapter 1 example.
tags: [c, masm, kandr, tutorial]
status: stable
generated: { by: agent/hermes, at: 2026-08-27T00:00:00Z }
sources:
  - id: kandr-ch1-ex09-digit-hist
    resource: "wiki/concepts/kr-ch1-masm/ex09-digit-hist.md"
    title: "Ex09 Digit Hist"
    usage_count: 1
---

; ============================================================================
; kandr-ch1-ex09-digit-hist.asm
; K&R Ch 1.6: Count digit occurrences in input
;
; C original:
;   #include <stdio.h>
;   main() {
;       int c, i, nwhite, nother;
;       int ndigit[10];
;       nwhite = nother = 0;
;       for (i = 0; i < 10; ++i)
;           ndigit[i] = 0;
;       while ((c = getchar()) != EOF)
;           if (c >= '0' && c <= '9')
;               ++ndigit[c - '0'];
;           else if (c == ' ' || c == '
' || c == '	')
;               ++nwhite;
;           else
;               ++nother;
;       printf("digits =");
;       for (i = 0; i < 10; ++i)
;           printf(" %d", ndigit[i]);
;       printf(", white space = %d, other = %d\n", nwhite, nother);;   }\n;
; MASM equivalent — 10-element array in .data, same three-way branch.
; ============================================================================

.386
.model flat, c

.data
    ndigit  dd  10 dup(0)
    nwhite  dd  0
    nother  dd  0
    ch      byte  ?
    i       dd  0

.code
main proc
    push    ebp
    mov     ebp, esp

    ; initialize ndigit[0..9] = 0, nwhite = 0, nother = 0
    lea     eax, ndigit
    xor     ecx, ecx
    mov     edx, 10
.init_loop:
    mov     [eax + ecx*4], 0
    inc     ecx
    cmp     ecx, 10
    jl      .init_loop

    ; main loop: read char, classify, update counters
.loop:
    push    1
    push    offset ch
    push    0
    call    @stdcall read
    add     esp, 12
    test    eax, eax
    jz      .done

    movzx   eax, ch
    cmp     al, '0'
    jb      .not_digit
    cmp     al, '9'
    ja      .not_digit
    ; digit found: ndigit[c - '0']++
    sub     al, '0'
    movzx   ecx, eax
    lea     eax, ndigit
    mov     eax, [eax + ecx*4]
    inc     eax
    mov     [ndigit + ecx*4], eax
    jmp     .end_iter

.not_digit:
    movzx   eax, ch
    cmp     al, ' '
    je      .is_white
    cmp     al, 0Ah
    je      .is_white
    cmp     al, 9
    je      .is_white
    ; other
    mov     eax, nother
    inc     eax
    mov     nother, eax
    jmp     .end_iter

.is_white:
    mov     eax, nwhite
    inc     eax
    mov     nwhite, eax

.end_iter:
    jmp     .loop

.done:
    pop     ebp
    ret
main endp

end main


