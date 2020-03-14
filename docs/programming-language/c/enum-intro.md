---
layout: post
title: "열거형 소개"
parent: C
grand_parent: Programming Language
nav_order: 3
---

# 열거형 소개
상수에는 열거(enumeration) 상수라는 형식이 있다. 열거란 다음과 같은 정수형 상수의 나열이다.
```c
enum boolean { NO, YES };
```
따로 지정되지 않으면 집합 안 첫 번째 이름의 값은 0, 1, 2 등의 값을 차례로 갖는다. 값이 지정되지 않은 것은 앞의 것보다 1 큰 값을 갖게 된다.
```c
enum escape { BELL = '\a', BACKSPACE = '\b', TAB = '\t',
     NEWLINE = '\n', VTAB = '\v', RETURN = '\r' };
enum months { JAN = 1, FEB, MAR, APR, MAY, JUN, JUL, AUG, SEP, OCT, NOV, DEC };
```
  
열거 내에서 상수의 이름은 모두 달라야 하지만 값은 같을 수도 있다.  
`enum`을 사용하면 `#define`으로 상수를 하나하나 지정해 주는 것보다 편리하게 여러 개의 상수를 지정할 수 있다. **컴파일러는 열거형 변수가 맞게 사용되었는지를 확인하지 않으므로** 프로그래머가 잘 확인해야 한다. 열거형 변수의 값을 확인하기 위해서는 디버거를 사용해야 한다.  
  
