---
layout: post
title: "입출력 명령어"
parent: Z80
grand_parent: CPU
nav_order: 16
---

# 입출력 명령어
**port:** 8비트 포트 주소  

## 데이터 입출력 명령어

```
IN A, (port)
IN r, (reg8)
```

```
OUT (port), A
OUT (reg8), reg8
```

## 블록 단위 데이터 입출력
**INI**   
**IND**  
**INIR**  
**INDR**  
**OUTI** 
**OUTD**  
**OUTIR**  
**OUTDR**  