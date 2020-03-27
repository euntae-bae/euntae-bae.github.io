---
layout: post
title: "순환문: while과 for"
parent: C
grand_parent: Programming Language
nav_order: 7
---

이미 앞에서 다음과 같은 while 문이나 for 문을 보았다.  

```c
while (expression)
    statement
```

수식을 계산하여, 0이 아니면 문장이 수행되고 수식을 다시 계산하게 된다. 이와 같은 과정은 수식이 0이 될 때까지 계속 반복하게 된다.  
  
for 문은  

```c
for (expression1; expression2; expression3)
    statement
```

의 구조를 가지며 이것은  

```c
expression1;
while (expression2) {
    statement;
    expression3;
}
```

와 같은 구조이다.  
  
문법적으로 for 문의 세 가지 요소, 즉 수식1, 수식2, 수식3이 모두 수식(expression)이어야 된다. 보통은 수식1과 수식3은 지정문(assignment)이거나 함수호출이고 수식2는 관계식(relational expression)이다. 위의 세 가지 요소 중 어느 것이라도 생략은 가능하지만 세미콜론은 남겨 두어야 한다. 비교를 수행하는 수식2가 존재하지 않으면 무한 루프를 돌게 된다. 즉,  

```c
for (;;) {
    ...
}
```

이것은 `break`나 `return` 등에 의해서만 동작을 중지시킬 수 있다.  
<br>

while 문을 사용할 것인가, for 문을 사용할 것인가는 프로그래머의 기호나 문제의 성격에 따라서 좌우된다. 즉,  

```c
while ((c = getchar()) == ' ' || c == '\n' || c == '\t')
    ; /* skip white space characters */
```

에서는 초깃값 설정이 필요 없으므로 while 문이 더 적합할 것이다.  
for 문은 루프 제어를 루프의 시작 부분에서 제어할 수 있기 때문에 초깃값 설정이 필요할 때는 while보다 편리하다. 즉,  

```c
for (i = 0; i < n; i++)
    ...
```

위의 예는 FORTRAN의 do 문이나 PASCAL의 for 문과 같은 기능을 가진 C의 구문이다. 다른 점은 C에서는 한계치(위 예의 n)를 루프 내에서 변경시킬 수 있다는 것과 세 번째 부분(위 예의 i++)은 어떤 수식이라도 가능하다는 것이다. 즉 정해진 만큼의 증가나 감소만 할 수 있는 것이 아니라 수식으로 정해 줄 수 있다는 것이다. 그렇지만 루프와 관계없는 계산을 루프 안으로 끌어들이는 것은 좋지 않다. 예를 들어 문자를 그와 동일한 수치의 값으로 변환하는 atoi 함수의 다른 형식의 프로그램을 보자.  
  
프로그램의 기본 구조는 다음과 같다.  
1. 공백이 있으면 무시하고
2. 부호가 있으면 읽고
3. 정수를 읽어서 문자로 변환
  
각 행에 나타난 명령은 각각의 정해진 일을 하며, 다음 처리에 대비해서 입력된 문자를 변환되지 않은 상태로 둔다.  
  
```c
#include <ctype.h>

int atoi(char s[])
{
    int i, n, sign;

    for (i = 0; isspace(s[i]; i++)) /* skip white space */
        ;
    sign = (s[i] == '-') ? -1 : 1;
    if (s[i] == '+' || s[i] == '-') /* skip sign */
        i++;
    for (n = 0; isdigit(s[i]); i++)
        n = 10 * n + (s[i] - '0');
    return sign * n;
}
```
<br>

for 문에서 자주 사용되는 콤마(,)도 C의 연산자이다. 콤마에 의해 분리된 두 수식은 왼쪽에서 오른쪽으로 계산되며 자료형과 계산 결과의 자료형은 오른쪽 연산자의 자료형을 갖게 된다. 따라서 for 문에 있어서 세 가지 구성요소 중의 어느 한 요소를 다중 수식(multiple expression)으로 나타낼 수 있어, 두 개의 변수를 함께 바꾸어 가면서 어떤 루프를 수행할 수 있다. 이것은 다음의 예제인 reverse 함수에 잘 나타나 있다. 이 reverse(s) 함수는 문자열 s를 그 역순으로 만드는 기능을 수행한다.  
  
```c
#include <string.h>

void reverse(char s[])
{
    int c, i, j;

    for (i = 0, j = strlen(s) - 1; i < j; i++, j--) {
        c = s[i];
        s[i] = s[j];
        s[j] = c;
    }
}
```
<br>

함수 인자(매개변수)에서의 콤마나 선언문에서 변수를 구별하는 콤마는 연산자가 아니므로 왼쪽에서 오른쪽으로의 연산을 보장하지는 않는다. 콤마 연산자는 일반적으로 잘 사용하지 않는다. reverse 프로그램의 for 루프와 같이 서로 연관이 깊은 구조를 요할 때나 매크로 구조 내에서 가끔 사용되고 있다. 콤마 연산자를 사용하여 앞의 예제를 조금 수정하면 다음과 같다.  

```c
for (i = 0, j = strlen(s) - 1; i < j; i++, j--)
    c = s[i], s[i] = s[j], s[j] = c;
```
