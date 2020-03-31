---
layout: post
title: "점프 명령어"
parent: Z80
grand_parent: CPU
nav_order: 7
---

# 점프 명령어
점프 명령어는 지정한 메모리 번지로 프로그램의 제어를 옮기는 명령어로, 하드웨어적으로는 PC의 값을 변경하는 것이다.  
  
Z80에서 점프 명령어는 크게 주소지정방식에 따라 절대 점프인 JP 명령어와 상대 점프인 JR이 존재하며, 이 둘은 각각 무조건(unconditional) 점프와 조건부(conditional) 점프로 다시 분류된다. 점프 명령어는 상태 레지스터에 영향을 미치치 않는다.  
<br>
  
## 절대 점프 명령어: JP(Jump)
절대 점프 명령어는 점프 주소가 16비트 절대 주소로 주어지기 때문에 모든 메모리 영역을 가리킬 수 있다.

### 1. 무조건 점프
```
; 직접 주소지정
JP nHnL
; 레지스터 간접 주소지정
JP (HL)
JP (IX)
JP (IY)
```
<br>
  
### ​2. 조건부 점프
조건부 점프는 상태 레지스터의 플래그 비트에 따라 점프 여부를 결정할 수 있는 점프 명령어이다.  
```
JP con, nHnL
```
**con:** NC(Not Carry), C(Carry), PO(Perity Odd), PE(Perity Even), NZ(Not Zero), Z(Zero), P(Plus, Positive), M(Minus, Negetive)  
**C(Carry):** NC, C  
**P/V(Parity/Overflow):** PO, PE  
**Z(Zero):** NZ, Z  
**S(Sign):** P, M  
<br>
  

## 상대 점프 명령어: JR(Jump Relative)
상대 점프 명령어인 JR은 JP 명령어와 달리 16비트 주소가 아니라 8비트 변위(displacement, offset)가 주어지는 2바이트 명령어이다. 즉, 피연산자로 메모리의 특정 위치가 아니라 PC(Program Counter)의 값을 기준으로 점프할 주소의 상대적인 위치를 전달한다. PC 상대 주소는 8비트(-128~+127)로 주어지기 때문에 근거리 점프만 가능하지만 코드가 차지하는 메모리 공간을 절약할 수 있다는 장점이 있다.  
  
### 1. 무조건 점프
```
JR d
```
​<br>
  
### 2. 조건 점프
```
JR con, d
```
**con:** NZ, Z, NC, C  
  
<br>
  
## +) 조건부 반복실행 명령어
Z80는 DJNZ(Decrement and Jump if Not Zero)라는 반복 실행 명령어를 제공한다. 이 명령어는 특정 횟수를 반복해야 할 때 매우 편리하다. 루프 카운터는 B 레지스터로 고정되어 있다. B 레지스터가 양수일 때 이 명령어가 실행되면 지정한 주소로 점프하고 B 레지스터의 값은 1 감소한다. DJNZ 명령어는 JR 명령어와 같이 8비트 상대 주소를 피연산자로 지정한다.  
  
```
DJNZ d
```
