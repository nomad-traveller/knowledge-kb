---
type: Source Summary
title: Ex01 Hello
description: 32-bit MASM equivalent of K&R Chapter 1 example.
tags: [c, masm, kandr, tutorial]
status: stable
generated: { by: agent/hermes, at: 2026-08-27T00:00:00Z }
sources:
  - id: kandr-ch1-ex01-hello
    resource: "wiki/concepts/kr-ch1-masm/ex01-hello.md"
    title: "Ex01 Hello"
    usage_count: 1
---

; ============================================================================
; kandr-ch1-ex01-hello.asm
; K&R Ch 1.1 "hello, world" → 32-bit MASM (flat model, UCR-style console)
;
; C original:
;   #include <stdio.h>
;   main() {
;       printf("hello, world\n");
;   }
;
; MASM equivalent — prints "hello, world" to stdout.
; ============================================================================

.386
.model flat, c

.data
    msg   byte  "hello, world"
    nl    byte  10
    len   dword 12

.code
main proc
    push    ebp
    mov     ebp, esp

    ; write to stdout (fd 1)
    push    1                       ; fd
    push    offset nl
    push    offset msg
    call    @stdcall write
    add     esp, 12

    pop     ebp
    ret
main endp

end main


