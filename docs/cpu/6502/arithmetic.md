---
layout: post
title: "산술 연산 명령어"
parent: 6502
grand_parent: CPU
nav_order: 9
---

# 산술 연산 명령어
**피연산자 기호**
**imm:** immediate, 즉시값  
**zp:** zero page, 제로 페이지 주소 ($0000~$00FF)  
**addr:** address, 16비트 주소 ($0000~$FFFF)

*6502의 Borrow(자리내림, 빌림)은 Carry의 역이다. 가령 어떤 뺄셈 연산의 결과로 Carry 플래그가 0으로 클리어 됐을 때 이것은 자리내림이 발생했음을 가리킨다. 반대로 자리내림이 발생하지 않았을 경우 Carry는 1로 세트된다.*  

## 1. 덧셈과 뺄셈
**ADC**  

| N | Z | C | I | D | V |
|:-:|:-:|:-:|:-:|:-:|:-:|
|\+ |\+ |\+ |\- |\- |\+ |

Add Memory to Accumulator with Carry; 메모리 데이터와 Carry를 누산기 레지스터 A와 덧셈  
```
ADC #imm
ADC zp
ADC zp, X
ADC addr
ADC addr, X
ADC addr, Y
ADC (zp, X)
ADC (zp), Y
```
<br>

**SBC**  

| N | Z | C | I | D | V |
|:-:|:-:|:-:|:-:|:-:|:-:|
|\+ |\+ |\+ |\- |\- |\+ |

Subtract Memory from Accumulator with Borrow; 메모리 데이터와 Borrow(Carry의 역)를 누산기 레지스터 A와 뺄셈  
```
SBC #imm
SBC zp
SBC zp, X
SBC addr
SBC addr, X
SBC addr, Y
SBC (zp, X)
SBC (zp), Y
```

<br>
  
## 2. 증가와 감소
**INC**  

| N | Z | C | I | D | V |
|:-:|:-:|:-:|:-:|:-:|:-:|
|\+ |\+ |\- |\- |\- |\- |

Increment Memory by One; 메모리 데이터를 1 증가  
```
INC zp
INC zp, X
INC addr
INC addr, X
```
<br>

**INX**  

| N | Z | C | I | D | V |
|:-:|:-:|:-:|:-:|:-:|:-:|
|\+ |\+ |\- |\- |\- |\- |

Increment Index X by One; X 레지스터를 1 증가  
<br>

**INY**  

| N | Z | C | I | D | V |
|:-:|:-:|:-:|:-:|:-:|:-:|
|\+ |\+ |\- |\- |\- |\- |

Increment Index Y by One; Y 레지스터를 1 증가  
<br>

**DEC**  

| N | Z | C | I | D | V |
|:-:|:-:|:-:|:-:|:-:|:-:|
|\+ |\+ |\- |\- |\- |\- |

Drcrement Memory by One; 메모리 데이터를 1 감소  
```
DEC zp
DEC zp, X
DEC addr
DEC addr, X
```
<br>

**DEX**  

| N | Z | C | I | D | V |
|:-:|:-:|:-:|:-:|:-:|:-:|
|\+ |\+ |\- |\- |\- |\- |

Decrement Index X by One; X 레지스터를 1 감소  
<br>

**DEY**  

| N | Z | C | I | D | V |
|:-:|:-:|:-:|:-:|:-:|:-:|
|\+ |\+ |\- |\- |\- |\- |

Decrement Index Y by One; Y 레지스터를 1 감소  
<br>

## 요약
### 덧셈과 뺄셈
- ADC, SBC  
  
### 증가와 감소
- INC, INX, INY, DEC, DEX, DEY  
  

- Borrow는 Carry 플래그의 역이다.  
- ADC 명령어의 연산 결과에 Carry 비트가 반영되지 않도록 하려면 CLC 명령어를 미리 실행해야 한다.  
- SBC 명령어의 연산 결과에 Carry 비트가 반영되지 않도록 하려면 SEC 명령어를 미리 실행해야 한다.  

<br>

### 참고자료
<https://www.masswerk.at/6502/6502_instruction_set.html>