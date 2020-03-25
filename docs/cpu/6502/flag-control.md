---
layout: post
title: "플래그 제어 명령어"
parent: 6502
grand_parent: CPU
nav_order: 8
---

# 플래그 제어 명령어

**SEC**  

| N | Z | C | I | D | V |
|:-:|:-:|:-:|:-:|:-:|:-:|
|\- |\- |\1 |\- |\- |\- |

Set Carry Flag; Carry 플래그를 1로 세트한다.  
<br>

**CLC**  

| N | Z | C | I | D | V |
|:-:|:-:|:-:|:-:|:-:|:-:|
|\- |\- |\0 |\- |\- |\- |

Clear Carry Flag; Carry 플래그를 0으로 클리어한다.  
<br>

**SED**  

| N | Z | C | I | D | V |
|:-:|:-:|:-:|:-:|:-:|:-:|
|\- |\- |\- |\- |\1 |\- |

Set Decimal Flag; Decimal 플래그를 1로 세트한다.  
<br>

**CLD**  

| N | Z | C | I | D | V |
|:-:|:-:|:-:|:-:|:-:|:-:|
|\- |\- |\- |\- |\0 |\- |

Clear Decimal Flag: Decimal 플래그를 0으로 클리어한다.  
<br>

**SEI**  

| N | Z | C | I | D | V |
|:-:|:-:|:-:|:-:|:-:|:-:|
|\- |\- |\- |\1 |\- |\- |

Set Interrupt Disable Status; Maskable 인터럽트의 사용을 불허한다.  
<br>

**CLI**

| N | Z | C | I | D | V |
|:-:|:-:|:-:|:-:|:-:|:-:|
|\- |\- |\- |\0 |\- |\- |

Clear Interrupt Disable Status; Maskable 인터럽트의 사용을 허가한다.  
<br>

**CLV**  

| N | Z | C | I | D | V |
|:-:|:-:|:-:|:-:|:-:|:-:|
|\- |\- |\- |\- |\- |\0 |

Clear Overflow Flag; 오버플로우 플래그를 0으로 클리어한다.  
<br>
  

## 요약
- 플래그 제어 명령어는 SEC, CLC, SED, CLD, SEI, CLI, CLV로 구성된다.  
<br>

### 참고자료
<https://www.masswerk.at/6502/6502_instruction_set.html>