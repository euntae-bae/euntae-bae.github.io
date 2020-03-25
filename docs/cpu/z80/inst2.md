---
layout: post
title: 명령어의 분류2 - 명령어 길이
parent: Z80
grand_parent: CPU
nav_order: 2
---

# 명령어의 분류2 - 명령어 길이

명령어는 주소지정방식(addressing mode)에 따라 분류할 수도 있지만 명령어 길이를 기준으로도 분류할 수 있다. Z80은 가변 길이 명령어를 제공하는 프로세서로, 명령어의 길이는 1바이트부터 4바이트까지 다양하다.  

## 1바이트 명령어
![1바이트 명령어](/image/z80-1byteinst.png)  
예) `LD A, B ; $78`  
<br>

## 2바이트 명령어
![2바이트 명령어1](/image/z80-2byteinst1.png)  
예) `LD A, I ; $ED $57`  
  
![2바이트 명령어2](/image/z80-2byteinst2.png)  
예) `LD A, 55h ; $3E $55`  
<br>
  
## 3바이트 명령어
![3바이트 명령어1](/image/z80-3byteinst1.png)  
예) `LD A, (9000h) ; $3A $00 $90`  
  
![3바이트 명령어2](/image/z80-3byteinst2.png)  
예) `LD A, (IX + 2); $DD $7E $02`  
<br>
  
## 4바이트 명령어
![1바이트 명령어](/image/z80-4byteinst1.png)  
예) `RLC (IX + 1) ; $DD $CB $01 $06`  
  
![1바이트 명령어](/image/z80-4byteinst2.png)  
예) `LD BC, (9000h) ; $ED $4B $00 $90`
  
