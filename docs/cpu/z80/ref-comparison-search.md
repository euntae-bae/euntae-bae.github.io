---
layout: post
title: "비교 및 검색"
parent: Z80
grand_parent: CPU
nav_order: 14
---

# 비교 및 검색
**CP**
Compare
```
CP imm8
CP reg8
CP IXH
CP IXL
CP IYH
CP IYL

CP (HL)
CP (IX+d)
CP (IY+d)
```

**부호가 없는 정수의 비교**
* if A == N then Z 플래그는 세트된다.
* if A != N then Z 플래그는 리셋된다.
* if A < N then C 플래그는 세트된다.
* if A >= N then C 플래그는 리셋된다.
  
**부호가 있는 정수의 비교**
* if A == N then Z 플래그는 세트된다.
* if A != N then Z 플래그는 리셋된다.
* if A < N then S와 P/V 플래그는 서로 다르다.
* if A >= N then S와 P/V 플래그는 서로 같다.
  
**CPI**
**CPD**
**CPIR**
**CPDR**