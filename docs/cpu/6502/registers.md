---
layout: post
title: "6502의 레지스터"
parent: 6502
grand_parent: CPU
nav_order: 1
---
# 6502의 레지스터
## 서론
6502는 1975년 출시된 8비트 프로세서다.  

MOS 65계열 CPU들은 동시대에 나온 프로세서들에 비해 단순한 구조가 특징이다. CPU의 레지스터는 크게 범용 레지스터(General Purpose Register)와 특수 목적 레지스터(Special Purpose Register)로 나뉘는데, 6502의 범용 레지스터는 누산기 레지스터 A와 인덱스 레지스터 X, Y 뿐이다. 비슷한 시기에 출시된 Z80는 범용 레지스터가 A, B, C, D, E, H, L로 구성된데다가(게다가 BC, DE, HL은 붙여서 16비트 레지스터로 쓸 수 있다) 16비트 인덱스 레지스터 IX, IY를 별도로 제공했다는 점과 비교해 보면 6502가 지나치게 단순해 보일 수 있으나 이러한 단순한 구조와 저렴한 가격 덕분에 6502는 Z80과 함께 8비트 컴퓨터 시장에서 양대산맥을 이루는 CPU가 됐다.  
  

## 6502의 레지스터
  
| 범용 레지스터(General Purpose Register) | 특수 목적 레지스터(Special Purpose Register)                              |
|:---------------------------------------:|:-------------------------------------------------------------------------:|
| A, X, Y (8비트)                         | SP(S), PC, Processor Status Register(P) (16비트 PC를 제외하고 모두 8비트) |


레지스터는 CPU 내부에 있는 기억 장치다. 레지스터는 플립플롭이라고 하는 소자로 구현되고, DRAM이나 하드디스크랑 비교했을 때 단위 용량 당 가격이 가장 비싸다. 그래서 대체로 크기가 작지만(또한 레지스터가 지나치게 많아도 오버헤드가 커진다) 대신에 가장 빠르다. 레지스터는 CPU 클럭 한 사이클 이내로 접근이 가능하지만 메인 메모리인 DRAM에 접근하기 위해서는 적어도 수십 사이클이 소모된다.  

​레지스터는 크게 **범용 레지스터**와 **특수 목적 레지스터**로 나뉜다. 범용 레지스터는 프로그래머가 임의로 조작할 수 있는 레지스터다. 즉, 프로그램 코드(명령어)에 의해 명시적으로 값이 변경될 수 있다. 6502의 범용 레지스터는 누산기 레지스터인 A(Accumulator)와 인덱스 레지스터 X, Y로 구성된다. 물론 이 세 레지스터는 특수한 목적이 있다고도 할 수 있다. 누산기는 ALU(산술 논리 연산장치)의 연산 결과가 저장되는 레지스터이고, 인덱스 레지스터는 주소지정용으로 사용되기 때문이다.  

[6502의 주소지정 방식](/docs/cpu/6502/addressing-mode)

하지만 그럼에도 범용 레지스터다. 이 셋은 프로그래머가 원하는 임의의 값을 쓰거나 읽을 수 있기 때문이다. 예를 들어 LDA, LDY, LDX는 지정한 즉시(immediate)값이나 메모리 데이터를 레지스터에 적재(Load)하는 명령어들이다. 또한 INX, INY, DEX, DEY 등의 명령어는 X, Y 레지스터를 증감시키고, TAX, TXA, TAY, TYA는 레지스터 간 데이터 전송 명령어다.  

범용 레지스터와 상대되는 개념으로는 특수 목적 레지스터가 있다. 특수 목적 레지스터는 이름 그대로 특수한 목적을 위해 사용되는 레지스터다. 특수 목적 레지스터는 시스템이 특정 연산을 수행하기 위한 값들을 저장하기 때문에 프로그래머의 접근은 상당히 제한적이다. 6502의 특수 목적 레지스터는 스택 포인터인 SP, 프로그램 카운터인 PC, 상태 레지스터인 P로 구성된다. 16비트 길이를 가지는 PC 레지스터를 제외하면 전부 8비트 레지스터다.  

​
### (1). 범용 레지스터
**A: Accumulator, 누산기**  
ALU의 연산 결과를 저장하는 8비트 레지스터. 일반적인 데이터 레지스터로도 사용한다.  
  
**​X, Y: 인덱스(index) 레지스터**  
인덱스 주소지정(indexed addressing)에 사용되는 8비트 레지스터. A와 마찬가지로 데이터 레지스터로도 사용한다.  

인덱스 주소지정이란 메모리 피연산자가 존재하는 유효 주소(effective address)를 구할 때 베이스 주소와 인덱스 레지스터 값을 더해서 구하는 방식을 말한다. 자세한 내용은 링크로 걸어둔 '6502의  주소지정방식'글을 참조하길 바란다.  

​
### (2). 특수 목적 레지스터
**SP(S): Stack Pointer, 스택 포인터**  
스택의 Top(최상위)을 가리키는 8비트 레지스터. **6502는 주소 버스의 길이가 16비트이지만, 스택 영역이 메모리상의 페이지 1($0100-$01FF)로 고정돼 있기 때문에, 스택 포인터는 8비트 레지스터다.**  
후입선출(LIFO) 방식의 자료구조인 (하드웨어적 의미의)스택은 데이터가 저장될 때 메모리상에서 거꾸로, 즉 높은 주소에서 낮은 주소로 성장한다. 예를 들어, 스택 포인터가 $FF일 때 PHA 명령어로 A 레지스터의 값을 스택에 저장하면, $01FF에 A의 값이 저장되고 스택 포인터가 $FE로 감소한다. 반대로 PLA 명령어로 스택에 있는 데이터를 A레지스터에 저장하면, 스택 포인터는 $FF로 증가한다.  
  
​**PC: Program Counter, 프로그램 카운터**  
다음에 실행될 명령어의 주소를 저장하는 **16비트 레지스터**. x86 계열의 CPU에서는 PC를 IP(Instruction Pointer)라고 부르기도 한다.  
프로그램 카운터는 프로그램의 현재 흐름을 나타내는 것이기 때문에, 분기 명령어나 서브루틴 호출, 인터럽트는 PC와 깊게 연관돼 있다.  
  
**Processor Status Register(P): 상태 레지스터**  
CPU의 연산 결과를 반영하는 **상태 플래그**와 CPU 제어를 위한 **모드 비트**를 저장하는 8비트 레지스터.  
총 8비트 중 **7개의 비트**를 이용하여 플래그를 나타내고, 나머지 하나는 사용되지 않는다(Unused, Reserved). x86 계열의 CPU에서는 이런 상태 레지스터를 플래그 레지스터(Flag Register)라고도 한다.
  
| 7 | 6 | 5 | 4 | 3 | 2 | 1 | 0 |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| N | V | - | B | D | I | Z | C |

7개의 비트 중 N, V, Z, C는 연산 결과를 나타내는 상태 플래그(Status Flag)로, 조건 분기(conditional branch) 명령어는 이러한 상태 플래그의 값을 검사해서 분기 여부를 결정한다. 6502는 V, C 비트를 클리어하거나 세트할 수 있는 CLV, SEC, CLC 명령어를 제공한다. BRK 명령어의 실행 여부를 나타내는 B 역시 CPU의 상태를 나타내는 플래그 비트다. BRK 명령어는 일종의 소프트웨어 인터럽트이다.  
  
D나 I 비트는 CPU의 상태를 제어할 때 사용한다. D는 Decimal로, BCD 연산을 수행할 때 사용하고 I는 Interrupt Disable로, Maskable 인터럽트의 허가 여부를 나타낸다.  
  
**N: Negative(음수) 또는 Sign(부호)**  
부호비트를 나타낸다. 연산 결과의 최상위 비트인 8번째 비트가 여기에 저장된다. 1이면 음수, 0이면 양수를 의미한다.  
  
**V: oVerflow**  
연산 결과로 오버플로우가 발생하면 1로 세트된다. V 비트를 제어하는 명령어로는 CLV가 있다.  
  
​**B: Break Command**  
소프트웨어 인터럽트인 BRK 명령어가 실행되면 1로 세트된다.  
  
​**D: Decimal**  
이 비트가 설정됐을 경우 BCD(Binary-coded decimal)로 산술연산을 수행한다.  
D 비트를 제어하는 명령어로는 SED, CLD가 있다.  
  
**I: Interrupt Disable**
Maskable 인터럽트(IRQ, BRK)의 허가 여부를 나타낸다. 비트가 1로 설정됐을 경우 Maskable 인터럽트 요청이 들어왔을 때 무시된다.  
I 비트를 제어하는 명령어로는 SEI, CLI가 있다.  
  
**Z: Zero**  
연산 결과가 0일 때 1로 세트된다. 0인지, 0이 아닌지를 나타내기 때문에 두 수의 일치 여부를 비교할 때(예를 들어 CMP, CPX, CPY, BEQ, BNE 명령어 등) 자주 사용된다.  
  
​**C: Carry**  
연산 결과로 자리올림(Carry)이 발생하면 1로 세트된다. 6502에서 자리내림(Borrow)은 Carry의 역(inverse)이다. 뺄셈 연산에서 자리내림이 발생하면 0으로 클리어되고, 자리내림이 발생하지 않으면 1로 세트됩니다.  
C 비트를 제어하는 명령어로는 SEC, CLC가 있다. 6502의 덧셈과 뺄셈 명령어인 ADC, SBC는 반드시 Carry 비트의 값이 연산 결과에 포함되기 때문에 SEC와 CLC 명령어의 사용도 알아둘 필요가 있다.  
  
[Carry 플래그에 대한 이해를 돕기 위해](/docs/cpu/6502/carry-flag)