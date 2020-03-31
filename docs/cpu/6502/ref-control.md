---
layout: post
title: "기타 제어 명령어"
parent: 6502
grand_parent: CPU
nav_order: 11
---

# 기타 제어 명령어

**NOP**  

| N | Z | C | I | D | V |
|:-:|:-:|:-:|:-:|:-:|:-:|
|\- |\- |\- |\- |\- |\- |

No Operation; 무연산  
<br>

**SEI**  

| N | Z | C | I | D | V |
|:-:|:-:|:-:|:-:|:-:|:-:|
|\- |\- |\- | 1 |\- |\- |

Set Interrupt Disable Status; Maskable 인터럽트의 사용을 불허한다.  
<br>

**CLI**  

| N | Z | C | I | D | V |
|:-:|:-:|:-:|:-:|:-:|:-:|
|\- |\- |\- | 0 |\- |\- |

Clear Interrupt Disable Status; Maskable 인터럽트의 사용을 허가한다.  
<br>

**BRK**  

| N | Z | C | I | D | V |
|:-:|:-:|:-:|:-:|:-:|:-:|
|\- |\- |\- | 1 |\- | 1 |

Force Break; 소프트웨어 인터럽트, 스택에 복귀 주소와 상태 레지스터 값을 저장한다.  
<br>

**RTI**  

| N | Z | C | I | D | V |
|:-:|:-:|:-:|:-:|:-:|:-:|
|from stack||||||

Return from Interrupt; ISR을 종료하고 스택으로부터 복귀 주소와 상태 레지스터 값을 꺼내 복원한다.  
<br>
  
### 참고 자료
<https://www.masswerk.at/6502/6502_instruction_set.html>