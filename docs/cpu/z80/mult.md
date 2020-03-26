---
layout: post
title: "8비트 곱셈 프로그램"
parent: Z80
grand_parent: CPU
nav_order: 9
---

# 8비트 곱셈 프로그램 (for Z80)
6502 어셈블리어로 구현한 곱셈 프로그램을 Z80 버전으로 이식해봤습니다.  
사용 어셈블러: `tniASM`  
  
[mult.asm](https://github.com/euntae-bae/asmZ80/blob/master/mult.asm)  

```
    org $0200
start:
    call init

    ld a, 10
    ld (num1), a
    ld a, 5
    ld (num2), a
    call mult
    
    ld ix, resultArr
    ld b, 9
    ld d, 1
    ld e, 1
.outer:
.inner:
    call multr
    ld (ix), a
    inc ix
    inc e
    ld a, e
    cp 10
    jr nz, .inner
    ld e, 1
    inc d
    djnz .outer

    ;jr start
    halt

init:
    ld a, 0
    ld bc, 0
    ld de, 0
    ld hl, 0
    ld ix, 0
    ld iy, 0

    ld (num1), a
    ld (num2), a

    ld b, ARR_LENGTH
    ld ix, resultArr
.clrmem:
    ld (ix), a
    inc ix
    djnz .clrmem ; ARR_LENGTH번 반복한다.
    ret

; multiply register
; input: d, e
; output: a
multr:
    push bc
    ld a, 0
    ld b, e
.loop:
    add a, d
    djnz .loop
    pop bc
    ret

; multiply memory
; input: num1, num2
; output: result
mult:
    push af
    push de
    ld a, (num1)
    ld d, a
    ld a, (num2)
    ld e, a
    call multr
    ld (result), a
    pop de
    pop af
    ret

ARR_LENGTH: equ 81
num1:   db 0
num2:   db 0
result: db 0
resultArr: ds ARR_LENGTH
boundTest:  db $ab, $cd, $ef
```