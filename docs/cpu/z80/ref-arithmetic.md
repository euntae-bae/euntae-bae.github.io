---
layout: post
title: "산술 연산 명령어"
parent: Z80
grand_parent: CPU
nav_order: 12
---

# 산술 연산 명령어

## 1. 덧셈

### (1). 8비트 덧셈
**ADD**  

```
ADD A, imm8

ADD A, reg8
ADD A, IXH
ADD A, IXL
ADD A, IYH
ADD A, IYL

ADD A, (HL)
ADD A, (IX+d)
ADD A, (IY+d)
```

**ADC**  

```
ADC A, imm8

ADC A, reg8
ADC A, IXH
ADC A, IXL
ADC A, IYH
ADC A, IYL

ADC A, (HL)
ADC A, (IX+d)
ADC A, (IY+d)
```

(2). 16비트 덧셈
**ADD**  

```
ADD HL, BC
ADD HL, DE
ADD HL, HL
ADD HL, SP

ADD IX, BC
ADD IX, DE
ADD IX, IX
ADD IX, SP

ADD IY, BC
ADD IY, DE
ADD IY, IY
ADD IY, SP
```
<br>

**ADC**  

```
ADC HL, BC
ADC HL, DE
ADC HL, HL
ADC HL, SP
```


## 2. 뺄셈
### (1). 8비트 뺄셈
**SUB**  

```
SUB imm8
SUB reg8

SUB (HL)

SUB(IX+d)
SUB(IY+d)
```

**SBC**  

```
SBC A, imm8
SBC A, reg8
SBC A, IXH
SBC A, IXL
SBC A, IYH
SBC A, IYL

SBC A, (HL)
SBC A, (IX+d)
SBC A, (IY+d)
```

(2). 16비트 뺄셈
Z80은 16비트 뺄셈 명령어로 SUB 명령어는 제공하지 않는다.  
  
**SBC**  

```
SBC HL, BC
SBC HL, DE
SBC HL, HL
SBC HL, SP
```

## 3. 증가와 감소
**INC**  

```
INC reg8
INC IXH
INC IXL
INC IYH
INC IYL

INC (HL)
INC (IX+d)
INC (IY+d)

INC reg16
INC SP
```

**DEC**  
```
DEC reg8
DEC IXH
DEC IXL
DEC IYH
DEC IYL

DEC (HL)
DEC (IX+d)
DEC (IY+d)

DEC reg16
DEC SP
```

## 4. 기타 산술 연산
**DAA**  
**CPL**  
**NEG**  

### 참고 문헌
