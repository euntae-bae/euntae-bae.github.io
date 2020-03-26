---
layout: post
title: "블록 전송 명령어"
parent: Z80
grand_parent: CPU
nav_order: 5
---

# 블록 전송 명령어
블록 전송 명령어는 메모리의 한 영역에서 다른 영역으로 최대 64KB까지의 데이터를 블록으로 전송할 수 있는 강력한 명령어이다. 
블록 전송 명령어들은 다음 세 가지 레지스터쌍을 특수한 용도로 사용한다.  
  

|레지스터|용도                           |
|:----:|:----------------------------:|
|HL    |근원지 주소(Source Address)     |
|DE    |목적지 주소(Destination Address)|
|BC    |전송 바이트 개수                 |

  

**LDI(Load and Increment)**  
HL 레지스터가 가리키는 메모리 영역의 내용을 DE 레지스터가 가리키는 메모리 영역으로 전송한다.  
(LD (DE), (HL)라는 명령어가 존재한다고 가정하면 된다.)  
전송 후 자동으로 HL, DE의 값은 1 증가하고 BC의 값은 1 감소한다. 만약 BC 레지스터가 0이 되면 P/V 플래그가 1에서 0으로 리셋된다.  
  
**LDIR(Load and Increment and Repeat)**  
LDI 명령어와 같은 기능을 수행하지만 BC 레지스터가 0이 될 때까지 반복한다는 점에서 차이가 있다. LDI 명령어를 특정 개수만큼 반복하기 위해서는 별도의 점프 명령이 필요했지만 LDI 명령어는 그렇지 않다.  
  
​**LDD(Load and Decrement)**  
LDD 명령어는 LDI 명령어와 같이 HL이 가리키는 메모리 내용을 DE가 가리키는 메모리 내용으로 전송한다. 차이점은 LDD는 LDI와 달리 HL, DE 레지스터의 값을 1 증가가 아니라 감소시킨다는 점이다.  
  
​**LDDR(Load and Decrement and Repeat)**  
LDDR 명령어는 LDD 명령어와 같은 기능을 수행하지만 BC 레지스터가 0이 될 때까지 반복하고 자동으로 종료한다는 점에서 차이가 있다.  