---
type: Source Summary
title: Ex10 Power
description: 32-bit MASM equivalent of K&R Chapter 1 example.
tags: [c, masm, kandr, tutorial]
status: stable
generated: { by: agent/hermes, at: 2026-08-27T00:00:00Z }
sources:
  - id: kandr-ch1-ex10-power
    resource: "wiki/concepts/kr-ch1-masm/ex10-power.md"
    title: "Ex10 Power"
    usage_count: 1
---

; ============================================================================
; kandr-ch1-ex10-power.asm
; K&R Ch 1.7: power(base, n) — raise base to n-th power
;
; C original:
;   int power(int base, int n) {
;       int i, p;
;       p = 1;
;       for (i = 1; i <= n; ++i)
;           p = p * base;
;       return p;
;   }
;   main() {
;       int i;
;       for (i = 0; i < 10; ++i)
;           printf("%d %d %d\n", i, power(2,i), power(-3,i));;   }\n;
; MASM equivalent — CALL stack convention, cdecl, parameters right-to-left.
; ============================================================================

.386
.model flat, c

.code
; int power(int base, int n)
; cdecl: caller cleans the stack (add esp, 8)
power proc
    push    ebp
    mov     ebp, esp

    ; base = [ebp+8]
    ;   n  = [ebp+12]
    mov     eax, 1          ; p = 1
    mov     ecx, 0          ; i = 0

.loop:
    mov     edx, [ebp+12]   ; edx = n
    cmp     ecx, edx
    jg      .done           ; i > n → done

    mov     eax, eax        ; p
    imul    [ebp+8]         ; p *= base
    inc     ecx             ; ++i
    jmp     .loop

.done:
    pop     ebp
    ret
power endp

main proc
    push    ebp
    mov     ebp, esp

    ; Call power(2, i) and power(-3, i) for i = 0..9
    xor     eax, eax        ; i = 0

.loop_main:
    cmp     eax, 9
    jg      .done_main

    ; push n (i), push base (2 or -3) — right to left
    push    eax             ; n = i
    push    2               ; base = 2
    call    power
    add     esp, 8

    push    eax             ; n = i
    push    -3              ; base = -3
    call    power
    add     esp, 8

    inc     eax             ; ++i
    jmp     .loop_main

.done_main:
    pop     ebp
    ret
main endp

end main


