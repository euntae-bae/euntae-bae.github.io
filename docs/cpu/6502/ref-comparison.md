---
layout: post
title: "비교 명령어"
parent: 6502
grand_parent: CPU
nav_order: 6
---

# 비교 명령어

**피연산자 기호**  
**imm:** immediate, 즉시값  
**zp:** zero page, 제로 페이지 주소 ($0000~$00FF)  
**addr:** address, 16비트 주소 ($0000~$FFFF)  

*각 명령어 이름 다음에는 명령어가 상태 플래그에 미치는 영향을 표기했다. +로 표기된 플래그는 명령어에 영향을 받는다.*  
*비교의 원리는 기본적으로 **뺄셈**이다. 다만 뺄셈 연산은 레지스터 값에 연산을 미치지 않고 상태 플래그에만 영향을 미친다.*  
  

**CMP**  

| N | Z | C | I | D | V |
|:-:|:-:|:-:|:-:|:-:|:-:|
|\+ |\+ |\+ |\- |\- |\- |

Compare Memory with Accumulator; 메모리 데이터와 누산기 레지스터 A의 값 비교  
```
CMP #imm
CMP zp
CMP zp, X
CMP addr
CMP addr, X
CMP addr, Y
CMP (zp, X)
CMP (zp), Y
```
<br>

**CPX**  

| N | Z | C | I | D | V |
|:-:|:-:|:-:|:-:|:-:|:-:|
|\+ |\+ |\+ |\- |\- |\- |

Compare Memory and Index X; 메모리 데이터와 X 레지스터의 값 비교  
```
CPX #imm
CPX zp
CPX addr
```
<br>

**CPY**  

| N | Z | C | I | D | V |
|:-:|:-:|:-:|:-:|:-:|:-:|
|\+ |\+ |\+ |\- |\- |\- |

Compare Memory and Index Y; 메모리 데이터와 Y 레지스터의 값 비교  
```
CPY #imm
CPY zp
CPY addr
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


## 요약
- 비교 명령어는 레지스터와 피연산자의 뺄셈 연산의 결과를 상태 레지스터에 반영한다.  
- 비교 연산은 N(Negative or Sign), Z(Zero), C(Carry) 플래그에 영향을 미친다.  
  
<br>

### 참고자료
<https://www.masswerk.at/6502/6502_instruction_set.html>