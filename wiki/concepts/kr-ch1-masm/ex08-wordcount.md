---
type: Source Summary
title: Ex08 Wordcount
description: 32-bit MASM equivalent of K&R Chapter 1 example.
tags: [c, masm, kandr, tutorial]
status: stable
generated: { by: agent/hermes, at: 2026-08-27T00:00:00Z }
sources:
  - id: kandr-ch1-ex08-wordcount
    resource: "wiki/concepts/kr-ch1-masm/ex08-wordcount.md"
    title: "Ex08 Wordcount"
    usage_count: 1
---

; ============================================================================
; kandr-ch1-ex08-wordcount.asm
; K&R Ch 1.5.4: Count lines, words, and characters
;
; C original:
;   #define IN   1
;   #define OUT  0
;   main() {
;       int c, nl, nw, nc, state;
;       state = OUT;
;       nl = nw = nc = 0;
;       while ((c = getchar()) != EOF) {
;           ++nc;
;           if (c == '
') ++nl;
;           if (c == ' ' || c == '
' || c == '	')
;               state = OUT;
;           else if (state == OUT) {
;               state = IN;
;               ++nw;
;           }
;       }
;       printf("%d %d %d\n", nl, nw, nc);;   }\n;
; MASM equivalent — same state machine with IN=1, OUT=0.
; ============================================================================

.386
.model flat, c

.data
IN      equ  1
OUT     equ  0

    ch    byte  ?
    nl    dd  0
    nw    dd  0
    nc    dd  0
    state dd  OUT

.code
main proc
    push    ebp
    mov     ebp, esp

    ; state = OUT
    mov     eax, OUT
    mov     state, eax

    ; nl = nw = nc = 0
    xor     eax, eax
    mov     nl, eax
    mov     nw, eax
    mov     nc, eax

.loop:
    ; c = getchar()
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

    ; if (c == '
') ++nl
    movzx   eax, ch
    cmp     al, 0Ah
    cmp     al, '
'
    jne     .check_ws
    ; fall through to ++nl
.nl_incr:
    mov     eax, nl
    inc     eax
    mov     nl, eax
    jmp     .check_ws

.check_ws:
    ; if (c == ' ' || c == '
' || c == '	') state = OUT;
    ; else if (state == OUT) { state = IN; ++nw; }
    movzx   eax, ch
    cmp     al, ' '
    je      .set_out
    cmp     al, '
'
    je      .set_out
    cmp     al, 9       ; tab
    je      .set_out

    ; state was not whitespace — check if we're entering a word
    mov     eax, state
    cmp     eax, IN
    je      .end_iter   ; already inside a word, do nothing
    ; entering a new word
    mov     eax, IN
    mov     state, eax
    mov     eax, nw
    inc     eax
    mov     nw, eax
    jmp     .end_iter

.set_out:
    mov     eax, OUT
    mov     state, eax

.end_iter:
    jmp     .loop

.done:
    pop     ebp
    ret
main endp

end main


