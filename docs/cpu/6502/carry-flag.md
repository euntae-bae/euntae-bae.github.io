---
layout: post
title: "Carry 플래그에 대한 이해를 돕기 위해"
parent: 6502
grand_parent: CPU
nav_order: 12
---

# Carry 플래그에 대한 이해를 돕기 위해
6502의 Carry 플래그는 덧셈 연산(ADC)에서 자리 올림을, 뺄셈 연산(SBC)에서 자리 내림(borrow)을 반영한다.  
  
6502에서는 ADD나 SUB 명령어를 따로 제공하지 않기 때문에 덧셈이나 뺄셈 연산을 할 때는 Carry 비트가 반영되는 ADC, SBC 명령어를 사용할 수밖에 없는데, 따라서 원하는 덧셈 또는 뺄셈 결과를 얻기 위해서는 Carry의 값에 유의하며 코딩해야 한다.  
  
​이를테면 C=0일 때 다음 연산의 결과로 A 레지스터에는 15가 저장된다.  
```
LDA #5
ADC #10
```

그러나 C=1일 때는 A 레지스터에 16이 저장된다.  
이런 문제를 해결하기 위해서 프로그래머는 덧셈이나 뺄셈 연산 이전에 CLC, SEC 명령어를 사용하여 Carry 비트를 제어해야 한다.  
  
한편, 6502의 자리 내림이 Carry 비트의 역(inverse)이라는 사실에 주의해야 한다. 다시 말해, 6502에서는 자리 내림이 발생하면 Carry=0으로 클리어되고 자리 내림이 발생하지 않으면 Carry=1로 세트된다.  

또한 SBC 명령어는 이러한 점을 반영하여 C=1일 때(자리 내림 없음),  
`A <- A - oper`라고 연산하고, C=0일 때(자리 내림 발생), `A <- A - oper - 1` 이라고 연산한다.  
  
```
LDA #10
SBC #5
```
  
그렇기 때문에 위의 연산 결과가 5가 되기를 원한다면 뺄셈 명령어 앞에 (ADC와 다르게)CLC가 아니라 SEC 명령어를 추가해야 한다.  
  
```
SEC
LDA #10
SBC #5
```
<br>
  
​지금까지의 설명에 대한 이해를 돕기 위해 예제를 준비했다. 명령어를 행 단위로 실행시켜가며 플래그 비트의 변화와 연산 결과 값을 주의깊게 확인해보길 바란다. 어셈블러는 asm6를 사용했다.  
  
[carry2.asm](https://github.com/euntae-bae/asm6502/blob/master/carry2.asm)

```
    .org $0200
start:
    jsr clrMem

    clc         ; C=0
    lda #$10
    adc #$20    ; A=$30, C=0
    sta add1
    
    sec         ; C=1
    lda #$10
    adc #$20    ; A=$31, C=0
    sta adc1

    clc         ; C=0
    lda #$f0
    adc #$30    ; A=$20, C=1
    sta add2

    sec         ; C=1
    lda #$f0
    adc #$30    ; A=$21, C=1
    sta adc2

    sec         ; C=1
    lda #$a
    sbc #$5     ; A=$5, C=1
    sta sub1

    clc         ; C=0
    lda #$a
    sbc #$5     ; A=$4, C=1
    sta sbc1

    sec         ; C=1
    lda #$5
    sbc #$a     ; A=$fb, C=0
    sta sub2

    clc         ; C=0
    lda #$5
    sbc #$a     ; A=$fa, C=0
    sta sbc2

    jmp start

clrMem:
    pha
    txa
    pha
    lda #0
    ldx #(sbc2-add1) ; A2 07
@loop:
    sta add1, x
    dex
    bpl @loop
    pla
    tax
    pla
    rts ; 60

add1 .db $ff
adc1 .db $ff
add2 .db $ff
adc2 .db $ff
sub1 .db $ff
sbc1 .db $ff
sub2 .db $ff
sbc2 .db $ff
```