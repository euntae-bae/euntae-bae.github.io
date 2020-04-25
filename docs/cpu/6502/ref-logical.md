---
layout: post
title: "논리 연산 명령어"
parent: 6502
grand_parent: CPU
nav_order: 10
---

# 논리 연산 명령어

**피연산자 기호**  
**imm:** immediate, 즉시값  
**zp:** zero page, 제로 페이지 주소 ($0000~$00FF)  
**addr:** address, 16비트 주소 ($0000~$FFFF)  

<br>

## 1. 논리 연산
**AND**  

| N | Z | C | I | D | V |
|:-:|:-:|:-:|:-:|:-:|:-:|
|\+ |\+ |\- |\- |\- |\- |

AND Memory with Accumulator; 메모리 데이터와 누산기 레지스터 A의 AND 연산  
```
AND #imm
AND zp
AND zp, X
AND addr
AND addr, X
AND addr, Y
AND (zp, X)
AND (zp), Y
```
<br>

**ORA**  

| N | Z | C | I | D | V |
|:-:|:-:|:-:|:-:|:-:|:-:|
|\+ |\+ |\- |\- |\- |\- |

OR Memory with Accumulator; 메모리 데이터와 누산기 레지스터 A의 OR 연산  
```
ORA #imm
ORA zp
ORA zp, X
ORA addr
ORA addr, X
ORA addr, Y
ORA (zp, X)
ORA (zp), Y
```
<br>

**EOR**  

| N | Z | C | I | D | V |
|:-:|:-:|:-:|:-:|:-:|:-:|
|\+ |\+ |\- |\- |\- |\- |

Exclusive-OR Memory with Accumulator; 메모리 데이터와 누산기 레지스터 A의 XOR 연산  
```
EOR #imm
EOR zp
EOR zp, X
EOR addr
EOR addr, X
EOR addr, Y
EOR (zp, X)
EOR (zp), Y
```
<br>

**BIT**  

| N | Z | C | I | D | V |
|:-:|:-:|:-:|:-:|:-:|:-:|
|M7 |\+ |\- |\- |\- |M6 |

Test Bits in Memory with Accumulator;  
(메모리) 피연산자의 비트7과 비트6은 상태 레지스터의 비트 7과 6(N, V)으로 전송된다.  
Zero 플래그는 피연산자와 A 레지스터의 값을 AND 연산한 결과를 반영한다.  
  
```
A AND M -> Z
M7 -> N
M6 -> V
```
  
```
BIT zp
BIT addr
```

<br>

## 2. 비트 시프트 연산
**ASL**  

| N | Z | C | I | D | V |
|:-:|:-:|:-:|:-:|:-:|:-:|
|\+ |\+ |\+ |\- |\- |\- |

Shift Left One Bit (Memory or Accumulator); 메모리 또는 누산기 레지스터 A를 왼쪽으로 1비트 산술 시프트  
```
ASL A
ASL zp
ASL zp, X
ASL addr
ASL addr, X
```
<br>

**LSR**  

| N | Z | C | I | D | V |
|:-:|:-:|:-:|:-:|:-:|:-:|
|0  |\+ |\+ |\- |\- |\- |

Shift One Bit Right (Memory or Accumulator); 메모리 또는 누산기 레지스터 A를 오른쪽으로 1비트 논리 시프트  
```
LSR A
LSR zp
LSR zp, X
LSR addr
LSR addr, X
```
<br>

**ROL**  

| N | Z | C | I | D | V |
|:-:|:-:|:-:|:-:|:-:|:-:|
|\+ |\+ |\+ |\- |\- |\- |

Rotate One Bit Left (Memory or Accumulator); 메모리 또는 누산기 레지스터 A를 왼쪽으로 1비트 회전  
```
C <- [76543210] <- C
```
  
```
ROL A
ROL zp
ROL zp, X
ROL addr
ROL addr, X
```
<br>

**ROR**  

| N | Z | C | I | D | V |
|:-:|:-:|:-:|:-:|:-:|:-:|
|\+ |\+ |\+ |\- |\- |\- |

Rotate One Bit Right (Memory or Accumulator); 메모리 또는 누산기 레지스터 A를 오른쪽으로 1비트 회전  
```
C -> [76543210] -> C
```
  
```
ROR A
ROR zp
ROR zp, X
ROR addr
ROR addr, X
```
<br>

## 요약
### 논리 연산
- AND, ORA, EOR, BIT  
  
### 비트 시프트 연산
- ASL, LSR, ROL, ROR  

<br>

### 참고자료
<https://www.masswerk.at/6502/6502_instruction_set.html>