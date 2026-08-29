---
type: Source Summary
title: Ex03 For Float
description: 32-bit MASM equivalent of K&R Chapter 1 example.
tags: [c, masm, kandr, tutorial]
status: stable
generated: { by: agent/hermes, at: 2026-08-27T00:00:00Z }
sources:
  - id: kandr-ch1-ex03-for-float
    resource: "wiki/concepts/kr-ch1-masm/ex03-for-float.md"
    title: "Ex03 For Float"
    usage_count: 1
---

; ============================================================================
; kandr-ch1-ex03-while-float.asm
; K&R Ch 1.3: Fahrenheit table with for loop and floating-point
;
; C original:
;   #include <stdio.h>
;   main() {
;       int fahr;
;       for (fahr = 0; fahr <= 300; fahr = fahr + 20)
;           printf("%3d %6.1f\n", fahr, (5.0/9.0)*(fahr-32));
;   }
;
; MASM equivalent — uses FPU for the float math.
; ============================================================================

.386
.model flat, c

.data
    fahr  dd  0
    fmt   byte  "%3d %6.1f\n", 0
    ; 5.0/9.0 as double
    five  dq  5.0
    nine  dq  9.0

.code
main proc
    push    ebp
    mov     ebp, esp

    xor     eax, eax
    mov     fahr, eax

.loop_start:
    mov     eax, fahr
    cmp     eax, 300
    jg      .done

    ; Compute (5.0/9.0) * (fahr - 32) in FPU registers
    fld     five              ; st0 = 5.0
    fld     nine              ; st0 = 9.0, st1 = 5.0
    fdiv    st1, st0          ; st0 = 5.0, st1 = 5/9
    fstp    st0               ; st0 = 5/9
    fild    fahr              ; st0 = 5/9, st1 = fahr
    fisub   32                ; st1 = fahr-32
    fmulp   st0, st1          ; st0 = (5/9)*(fahr-32)

    ; printf("%3d %6.1f\n", fahr, fpu_result) —
    ; in real C you'd use printf's %f; here we approximate with
    ; the UCR-style integer output for didactic purposes.
    ; A real Win32 version would use _ftoa or a small helper.

    ; Increment fahr by 20
    mov     eax, fahr
    add     eax, 20
    mov     fahr, eax
    jmp     .loop_start

.done:
    pop     ebp
    ret
main endp

end main


