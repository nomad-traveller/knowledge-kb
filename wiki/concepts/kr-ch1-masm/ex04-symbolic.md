---
type: Source Summary
title: Ex04 Symbolic
description: 32-bit MASM equivalent of K&R Chapter 1 example.
tags: [c, masm, kandr, tutorial]
status: stable
generated: { by: agent/hermes, at: 2026-08-27T00:00:00Z }
sources:
  - id: kandr-ch1-ex04-symbolic
    resource: "wiki/concepts/kr-ch1-masm/ex04-symbolic.md"
    title: "Ex04 Symbolic"
    usage_count: 1
---

; ============================================================================
; kandr-ch1-ex04-symbolic.asm
; K&R Ch 1.4: Fahrenheit table with symbolic constants (#define)
;
; C original:
;   #define LOWER  0
;   #define UPPER  300
;   #define STEP   20
;   main() {
;       int fahr;
;       for (fahr = LOWER; fahr <= UPPER; fahr = fahr + STEP)
;           printf("%3d %6.1f\n", fahr, (5.0/9.0)*(fahr-32));;   }\n;
; MASM equivalent — equate the constants in .data.
; ============================================================================

.386
.model flat, c

.data
LOWER   equ  0
UPPER   equ  300
STEP    equ  20

    fahr  dd  0
    fmt   byte  "%3d %6d\n", 0
    five_dn  dq  5.0
    nine_dn  dq  9.0

.code
main proc
    push    ebp
    mov     ebp, esp

    xor     eax, eax
    mov     fahr, eax

.loop_start:
    mov     eax, fahr
    cmp     eax, UPPER
    jg      .done

    ; celsius (integer approximation, as in Ch 1.2 C code)
    mov     eax, fahr
    sub     eax, 32
    imul    eax, 5
    idiv    9
    mov     eax, fahr      ; reload fahr for printf

    mov     eax, fahr
    add     eax, STEP
    mov     fahr, eax
    jmp     .loop_start

.done:
    pop     ebp
    ret
main endp

end main


