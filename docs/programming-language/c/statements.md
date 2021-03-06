---
layout: post
title: "문장과 블록"
parent: C
grand_parent: Programming Language
nav_order: 5
---

# 문장과 블록
`x=0`또는 `i++`, `printf(...)` 같은 것은 **수식(expression)**이라 하며, 이것들이 세미콜론(;)으로 끝나면 **문장(statement)**이 되는데 다음은 그 예이다.
```c
x = 0;
i++;
printf(...);
```
C언어에서 세미콜론은 문장의 끝을 나타내며, PASCAL과 같은 종류의 언어에서 세미콜론은 문장을 분리하는 역할을 한다. 
  
중괄호 `{ }`는 여러 개의 선언문이나 문장을 모아서 복합문(compound statement)이나 블록을 구성하는 데 쓰인다. 따라서 **중괄호로 묶인 복합문은 구문상으로 단일문장과 동일한 기능을 수행한다**. 
함수의 시작을 나타내는 \{와 끝을 나타내는 \}가 좋은 예이다. 이 밖에 if, else, while, for 등의 여러 문장을 둘러싸고 있는 중괄호가 있다. 블록을 끝내는 것을 나타내는 오른쪽 중괄호(\}) 뒤에는 세미콜론(;)이 올 수 없음에 유의해야 한다.