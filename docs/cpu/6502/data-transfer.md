---
layout: post
title: "데이터 전송 명령어"
parent: 6502
grand_parent: CPU
nav_order: 5
---

# 데이터 전송 명령어

**피연산자 기호**  
**imm:** immediate, 즉시값  
**zp:** zero page, 제로 페이지 주소 ($0000~$00FF)  
**addr:** address, 16비트 주소 ($0000~$FFFF)  
  
*각 명령어 이름 다음에는 명령어가 상태 플래그에 미치는 영향을 표기했다. +로 표기된 플래그는 명령어에 영향을 받는다.*  
  
## 1. 적재 및 저장 명령어
### (1). 적재(load) 명령어
**LDA**  

| N | Z | C | I | D | V |
|:-:|:-:|:-:|:-:|:-:|:-:|
|\+ |\+ |\- |\- |\- |\- |

Load Accumulator with Memory; A(누산기) 레지스터에 즉시값 또는 메모리 데이터 적재  
  
```
LDA #imm
LDA zp
LDA zp, X
LDA addr
LDA addr, X
LDA addr, Y
LDA (zp, X)
LDA (zp), Y
```
<br>

**LDX**

| N | Z | C | I | D | V |
|:-:|:-:|:-:|:-:|:-:|:-:|
|\+ |\+ |\- |\- |\- |\- |

Load Index X with Memory; X 레지스터에 즉시값 또는 메모리 데이터 적재  
  
``` 
LDX #imm
LDX zp
LDX zp, Y
LDX addr
LDX addr, Y
```
<br>

**LDY**

| N | Z | C | I | D | V |
|:-:|:-:|:-:|:-:|:-:|:-:|
|\+ |\+ |\- |\- |\- |\- |

Load Index Y with Memory; Y 레지스터에 즉시값 또는 메모리 데이터 적재  
```
LDY #imm
LDY zp
LDY zp, X
LDY addr
LDY addr, X
```
<br>

### (2). 저장(store) 명령어
**STA**  

| N | Z | C | I | D | V |
|:-:|:-:|:-:|:-:|:-:|:-:|
|\- |\- |\- |\- |\- |\- | 

Store Accumulator in Memory; 메모리에 A 레지스터 값 저장  
```
STA zp
STA zp, X
STA addr
STA addr, X
STA addr, Y
STA (zp, X)
STA (zp), Y
```
<br>

**STX**  

| N | Z | C | I | D | V |
|:-:|:-:|:-:|:-:|:-:|:-:|
|\- |\- |\- |\- |\- |\- |

Store Index X in Memory; 메모리에 X 레지스터 값 저장  
```
STX zp
STX zp, Y
STX addr
```
<br>

**STY**
Store Index Y in Memory; 메모리에 Y 레지스터 값 저장  

| N | Z | C | I | D | V |
|:-:|:-:|:-:|:-:|:-:|:-:|
|\- |\- |\- |\- |\- |\- |

```
STY zp
STY zp, X
STY addr
```
<br>

## 2. 레지스터 간 데이터 전송 명령어
**TAX**  

| N | Z | C | I | D | V |
|:-:|:-:|:-:|:-:|:-:|:-:|
|\+ |\+ |\- |\- |\- |\- |

Transfer Accumulator to Index X; X 레지스터에 A 레지스터 값 전송  
<br>

**TAY** 

| N | Z | C | I | D | V |
|:-:|:-:|:-:|:-:|:-:|:-:|
|\+ |\+ |\- |\- |\- |\- |

Transfer Accumulator to Index Y; Y 레지스터에 A 레지스터 값 전송  
<br>

**TXA**  

| N | Z | C | I | D | V |
|:-:|:-:|:-:|:-:|:-:|:-:|
|\+ |\+ |\- |\- |\- |\- |

Transfer Index X to Accumulator; A 레지스터에 X 레지스터 값 전송  
<br>

**TYA**  

| N | Z | C | I | D | V |
|:-:|:-:|:-:|:-:|:-:|:-:|
|\+ |\+ |\- |\- |\- |\- |

Transfer Index Y to Accumulator; A 레지스터에 Y 레지스터 값 전송  
<br>

**TSX**

| N | Z | C | I | D | V |
|:-:|:-:|:-:|:-:|:-:|:-:|
|\+ |\+ |\- |\- |\- |\- |

Transfer Stack Pointer to Index X; X 레지스터에 스택 포인터(SP) 값 전송  
<br>

**TXS**

| N | Z | C | I | D | V |
|:-:|:-:|:-:|:-:|:-:|:-:|
|\- |\- |\- |\- |\- |\- |  

Transfer Index X to Stack Pointer; SP 레지스터에 X 레지스터 값 전송  
  
<br>

## 3. 스택 연산 명령어
**PHA**  

| N | Z | C | I | D | V |
|:-:|:-:|:-:|:-:|:-:|:-:|
|\- |\- |\- |\- |\- |\- |

Push Accumulator on Stack; 스택에 A 레지스터 값 Push  
<br>

**PHP**

| N | Z | C | I | D | V |
|:-:|:-:|:-:|:-:|:-:|:-:|
|\- |\- |\- |\- |\- |\- |

Push Processor Status on Stack; 스택에 상태 레지스터 값 Push  
<br>

**PLA**

| N | Z | C | I | D | V |
|:-:|:-:|:-:|:-:|:-:|:-:|
|\+ |\+ |\- |\- |\- |\- |

Pull Accumulator from Stack; 스택으로부터 A 레지스터 값 Pop  
<br>

**PLP**

| N | Z | C | I | D | V |
|:-:|:-:|:-:|:-:|:-:|:-:|
|from stack||||||

Pull Processor Status from Stack; 스택으로부터 상태 레지스터 값 Pop  
<br>

## 요약
### 적재 및 저장 명령어
* (1). 적재(load) 명령어: LDA, LDX, LDY  
  

* (2). 저장(store) 명령어: STA, STX, STY  
  

### 레지스터 간 데이터 전송 명령어
TAX, TAY, TXA, TYA, TSX, TXS  
  
### 스택 연산 명령어
PHA, PHP, PLA, PLP  
  
### 데이터 전송 명령어가 상태 레지스터에 미치는 영향
- 레지스터 -> 메모리 전송은 플래그에 영향을 미치지 않는다.  
- 메모리 -> 레지스터, 레지스터 -> 레지스터 전송은 N(Negative 또는 Sign) 플래그와 Z(Zero) 플래그에 영향을 미친다.  
  
<br>

### 참고자료
<https://www.masswerk.at/6502/6502_instruction_set.html>  
