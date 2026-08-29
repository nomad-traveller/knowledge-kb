---
type: Source Summary
title: Ex02 Fahr Cel
description: 32-bit MASM equivalent of K&R Chapter 1 example.
tags: [c, masm, kandr, tutorial]
status: stable
generated: { by: agent/hermes, at: 2026-08-27T00:00:00Z }
sources:
  - id: kandr-ch1-ex02-fahr-cel
    resource: "wiki/concepts/kr-ch1-masm/ex02-fahr-cel.md"
    title: "Ex02 Fahr Cel"
    usage_count: 1
---

; ============================================================================
; kandr-ch1-ex02-fahr-cel.asm
; K&R Ch 1.2: Fahrenheit → Celsius table
;
; C original:
;   #include <stdio.h>
;   main() {
;       int fahr, celsius;
;       int lower, upper, step;
;       lower=0; upper=300; step=20;
;       fahr = lower;
;       while (fahr <= upper) {
;           celsius = 5*(fahr-32)/9;
;           printf("%d\t%d\n", fahr, celsius);
;           fahr = fahr + step;
;       }
;   }
;
; MASM equivalent — same table, UCR console output.
; ============================================================================

.386
.model flat, c

.data
    lower   dd  0
    upper   dd  300
    step    dd  20
    fahr    dd  0
    celsius dd  0
    ; format buffer: "%d\t%d\n"
    fmt     byte  "%d	%d\n", 0
    len     dd  7

.code
main proc
    push    ebp
    mov     ebp, esp

    mov     eax, 0
    mov     lower, eax

    mov     eax, 300
    mov     upper, eax

    mov     eax, 20
    mov     step, eax

    mov     fahr, 0

.loop_start:
    mov     eax, fahr
    cmp     eax, upper
    jg      .done

    ; celsius = 5 * (fahr - 32) / 9
    mov     eax, fahr
    sub     eax, 32
    imul    eax, 5
    cdq                         ; sign-extend into EDX:EAX for idiv
    idiv    9                   ; EAX = quotient, EDX = remainder
    mov     celsius, eax

    ; printf("%d\t%d\n", fahr, celsius)
    push    1
    push    offset fmt
    call    @stdcall printf
    add     esp, 8

    mov     eax, fahr
    add     eax, step
    mov     fahr, eax
    jmp     .loop_start

.done:
    pop     ebp
    ret
main endp

end main


