---
layout: post
title: "데이터 전송 간단 정리"
parent: Z80
grand_parent: CPU
nav_order: 3
---

# 데이터 전송 간단 정리

데이터 전송이란 레지스터와 레지스터, 레지스터와 메모리 사이에서 데이터를 주고 받는 연산을 의미합니다.  
여기에서 레지스터와 메모리를 잘 구분하는 것이 중요합니다. 레지스터와 메모리 모두 기억장치라는 점에서 동일하지만 속도와 크기 면에서는 꽤 차이가 있습니다.  
  
우리가 사용하는 범용 컴퓨터는 CPU와 메인 메모리가 분리돼 있는 **폰 노이만 구조**를 채택하고 있다는 사실을 기억해야 합니다. 일단 레지스터와 메모리를 간단히 언급하면서 넘어가볼까 합니다.
<br>

> 폰 노이만 구조라고 하는 것은 프로그램, 즉 수행하고자 하는 명령어들의 집합을 기억장치에 저장해두었다가 처리장치(프로세서)가 그것을 읽어서 처리하는 구조(프로그램 내장 방식)의 컴퓨터를 가리킵니다. 메모리는 CPU가 직접 접근할 수 있는 유일한 저장장치입니다. 프로그램이 실행되기 위해서 프로그램은 반드시 메모리 위에 올라와(load) 있어야 합니다. CPU는 메모리로부터 프로그램의  코드와 데이터를 인출(fetch)하고 인출한 명령어를 해독(decode) 및 실행(execution)하는 일련의 작업들을 수행합니다. 이를 두고 명령어 실행 사이클이라고 부릅니다.  
<br>

**레지스터(register)**는 CPU 내부에 있는 기억소자로, 기억장치 중에서는 접근 속도가 가장 빠릅니다. 대신 가격이 매우 비싸기 때문에 대용량으로 사용하기 어렵습니다. (설계된지 40년 넘는 8비트 CPU에는 해당사항이 아니겠지만) 덧붙여서 말씀드리자면, CPU를 설계하는 입장에서도 레지스터의 개수를 늘리는 것이 무조건적인 성능 향상 대책은 아닙니다. 오히려 레지스터의 개수가 너무 많은 경우에는 CPU의 크기도 비대해지고, 접근 속도가 느려질 수 있습니다.  
  
**메인 메모리(main memory)**는 우리가 흔히 램(RAM)이라고 부르는 장치를 말합니다. 메인 메모리는 주로 동적램(DRAM)을 이용하여 구현합니다. DRAM은 레지스터보다 집적도가 높은 장치입니다. 레지스터보다 단위 용량 당 가격이 훨씬 저렴하기 때문에(물론 과거에는 메모리도 아주 비싼 물건이었습니다) 상대적으로 대용량의 저장 장치라고 할 수 있죠. 물론 메모리는 레지스터보다 훨씬 느립니다. 애초에 메모리는 CPU 바깥에 존재하는 장치입니다. 그리고 이 둘은 시스템 버스(System bus)라는 전선으로 연결되어 있습니다. 오늘날의 컴퓨터들은 이런 메모리 접근 시간을 최대한 단축(회피)하기 위해 메모리와 CPU 사이에 고속의 캐시 메모리를 두고 자주 사용하는 데이터들을 저장해둡니다.  

> 메모리는 쉽게 말해서 하나의 긴 바이트 배열이라고 할 수 있습니다. 그리고 이 배열의 각 요소들에는 위치를 식별하기 위해 번호가 붙어있습니다. 이것을 우리는 메모리 주소(address)라고 부릅니다.
<br>

이번 시간에 다루는 데이터 전송 명령어는 아주 빈번하게 레지스터와 레지스터, 레지스터와 메모리 사이를 왔다갔다 하기 때문에 이 둘을 잘 구분하는 것이 중요합니다. 데이터 전송 명령어는 크게 8비트 데이터 전송과 16비트 데이터 전송 명령어로 나뉘어집니다.  
  
<br>

## 1. 8비트 데이터 전송
```
LD A, n
LD A, r
LD A, (rr)
LD A, I
LD A, R
LD A, (IX + d)
LD A, (IY + d)
LD A, (nHnL)
```
* r: A, B, C, D, E, H, L  
* rr: HL, BC, DE  
<br>


```
LD r, n
LD r, r
LD r, (HL)
LD r, (IX+d)
LD r, (IY+d)
LD (HL), n
LD (HL), r
LD (IX+d), n
LD (IX+d), r
LD (IY+d), n
LD (IY+d), r
```
* r: A, B, C, D, E, H, L  
<br>


```
LD I, A
LD R, A
LD (nHnL), A
LD (rr), A
```
* rr: HL, BC, DE  
<br>
  

## 2. 16비트 데이터 전송
```
LD rr, nHnL ; 즉시 주소지정방식
LD rr, (nHnL) ; 간접 주소지정방식
LD (nHnL), rr ; 직접 주소지정방식
```
* rr: BC, DE, HL, SP, IX, IY  
<br>

```
LD SP, HL
LD SP, IX
LD SP, IY
```
<br>

```
PUSH rr
POP rr
```
* rr: AF, BC, DE, HL, IX, IY  