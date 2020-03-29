---
layout: post
title: "명령어의 분류1 - 주소지정 방식"
parent: Z80
grand_parent: CPU
nav_order: 1
---

# 명령어의 분류1 - 주소지정 방식

주소지정 방식(addressing mode)이란 명령어가 필요로 하는 데이터, 즉 피연산자(operand)의 주소를 표현하는 방식들을 가리킨다. 다양한 종류의 주소지정 방식은 프로그래밍의 편의성과 다양한 프로그램 최적화(메모리 공간 절약, 클럭 사이클 절약) 방법을 제공한다. 하지만 주소지정 방식이 지나치게 많으면 CPU 설계가 복잡해지기 때문에 비용과 성능 측면에 불리하게 작용할 수 있다. CPU 설계자들은 컴퓨터 시스템의 목적에 따라 적절한 균형점을 잡아야 한다.  
  
Z80은 10 가지의 주소지정방식(addressing mode)를 제공한다.  
  

## 1. 즉시 주소지정방식(immediate addressing mode)
레지스터에  8비트 즉시값을 적재(load)하는 방식. Z80 어셈블리언어에서 즉시값을 표현할 때 별도의 기호는 필요 없다(6502 어셈블리언어가 즉시값을 표현할 때 # 기호를 사용하는 것과는 대조적이다).  
```
LD A, 12h
LD B, 0EFh
```
  
<br>

## 2. 확장 즉시 주소지정방식(immediate extended addressing mode)
레지스터쌍(Z80은 8비트 레지스터 두 개를 묶어 16비트 레지스터로 사용할 수 있다)에 16비트 즉시값을 적재하는 방식  
```
LD HL, 1234h
```
  
<br>

## 3. 직접 주소지정방식(direct addressing mode)
16비트 절대 주소(absolute address)를 피연산자의 주소로 지정하는 방식이다. Z80의 주소 공간을 전부 참조할 수 있지만, 16비트 주소를 명령어 피연산자 주소로 사용하기 때문에(즉, 주소지정에만 2바이트를 사용한다) 메모리 공간을 많이 차지한다. Z80의 절대 주소는 소괄호로 묶어서 표현한다. Z80에서 직접 주소지정 방식은 확장 주소지정 방식(extended addressing mode)이라고도 한다.  
```
LD A, (9000h)
LD HL, (2000h)
LD AB, (2010h)
LD (2020h), DE
```
  
<br>

## 4. 레지스터 주소지정방식(register addressing mode)
메모리 주소 대신 레지스터를 명령어의 피연산자로 지정하는 방법이다. 별도의 괄호나 기호 없이 레지스터 이름을 피연산자로 명시하면 된다.  
```
LD B, D
LD HL, SP
```
  
<br>

## 5. 레지스터 간접 주소지정방식(register indirect addressing mode)
레지스터를 피연산자 자체가 아니라 간접주소로 지정하는 방법이다. 16비트 레지스터 쌍에는 명령어의 피연산자 대신 피연산자의 주소 값이 담겨 있다.  
```
; A 레지스터에는 HL 레지스터의 값이 아니라, HL 레지스터에 저장된 메모리 주소가 가리키는 곳에 저장된 값이 저장된다.
LD A, (HL)​
```
<br>

## 6. 상대 주소지정 방식(relative addressing mode)
현재 프로그램 카운터(PC, Program Counter) 값에서 상대적인 변위(displacement)를 주소로 지정하는 방법. 일반적으로 상대 주소는 분기 명령어에서 사용된다. Z80의 경우에는 JR(Jump Relative) 명령어가 상대 주소를 사용한다. 상대 주소로 주어지는 변위(또는 오프셋)는 1바이트 부호 있는 정수 범위(-128~+127)로 한정되기 때문에 이 범위를 벗어나는 원거리 점프를 사용해야 하는 경우에는 절대 주소를 사용하는 JP 명령어를 사용해야 한다.  
  
상대 주소는 어셈블러가 계산하기 때문에 프로그래머가 직접 점프할 명령어의 상대적인 위치를 계산할 필요는 없다.  
```
start:
    LD A, 0
    ...
    JP start
```
  
<br>

## 7. 묵시(함축) 주소지정 방식(implied addressing mode)
이 방식의 명령어는 피연산자가 명령어 자체에 고정되어 있기 때문에, 별도의 명시적인 피연산자가 필요 없다. 이러한 방식을 사용하는 명령어의 예로는 EI, DI, CPL 등이 있다.  
  
<br>

## 8. 인덱스 주소지정 방식(indexed addressing mode)
16비트 인덱스 레지스터 IX, IY와 8비트 부호 있는 오프셋 값을 더하여 피연산자의 유효 주소(effective address)를 계산하는 방법이다. IX와 IY의 값은 베이스 주소(base address)로 사용된다. 다음 예제는 레지스터 간접 주소 지정과 인덱스 주소 지정의 사용을 둘 다 보여준다. 또한 이 예제에서 주의할 점은 레이블 num1이 $12라는 값이 아니라 $12가 저장된 메모리 주소라는 것이다. 따라서 LD IX, num1 명령어는 인덱스 레지스터 IX에 $12를 저장하는 것이 아니라, 16비트 절대 주소 $0218이라는 16비트 즉시값을 저장한다.  
```
    ORG $0200
    LD IX, num1
    LD HL, num1
    LD A, (HL)      ; register indirect, A <- $12
    LD A, (IX)      ; indexed, A <- $12
    LD A, (IX+1)    ; indexed, A <- $34
    LD A, (IX+2)    ; indexed, A <- $56
    LD IY, num1+2
    LD A, (IY+1)    ; indexed, A <- $78

num1: db $12
num2: db $34
num3: db $56
num4: db $78
```
  
<br>

## 9. 변형 페이지 제로 주소지정방식(modified page zero addressing mode)
Z80은 6502와 같이 제로 페이지 주소를 지정하기 위한 다양한 주소 지정 방식을 제공하지는 않는다. 대신에 약간 변형된 형태로 인터럽트 처리를 위해 사용되는데, Z80의 세 가지 인터럽트 모드 중 인터럽트 모드 0과 모드 1은 제로 페이지 영역($0000-$00FF)의 특정 위치로 점프하는 1바이트 명령어인 RST(Reset) 명령어를 제공한다(RST 명령어는 제로 페이지 주소 전체를 지정하는 것이 아니기 때문에, opcode 자체에 점프할 위치가 함축돼 있다). 자세한 내용은 다음 글을 참조하길 바란다.  
  
[Z80의 인터럽트](https://blog.naver.com/qodmsxo471/221810297254)
  
<br>

## 10. 비트 주소지정방식(bit addressing mode)
피연산자의 데이터를 비트 단위로 조작하는 방법이다. SET, RES, BIT 명령어가 이 주소 지정 방식을 사용한다.  
이 방식은 레지스터 또는 메모리상의 데이터를 비트 단위로 조작하며 레지스터 주소지정방식, 레지스터 간접주소지정방식, 인덱스 주소지정방식 중 어느 하나와 결합하여 사용한다.  
```
BIT 1, A
```
  
<br>

### 참고 문헌
- 《Z80 프로그래밍》, 남시병, 김성락, 두양사  
- Z80 CPU User Manual, Zilog  