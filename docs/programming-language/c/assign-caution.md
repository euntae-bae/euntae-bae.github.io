---
layout: post
title: "대입문 사용시 주의해야 할 점"
parent: C
grand_parent: Programming Language
nav_order: 1
---

# 대입문 사용시 주의해야 할 점
우리는 때때로 함수로부터 반환된 값을 변수에 저장하는 동시에 특정 ㄱㅄ과 비교하는 코드를 (직접 작성하든 다른 사람이 작성한 코드를 읽게 되든)접하게 된다. 예를 들어 다음과 같은 코드는
```c
#include <stdio.h>

int main(void)
{
        int c;

        c = getchar();
        while (c != EOF) {
                putchar(c);
                c = getchar();
        }
        printf("EOF: %d\n", EOF);
        return 0;
}
```
다음과 같은 코드로 단축할 수 있다.
```c
#include <stdio.h>

int main(void)
{
        int c;
        while ((c = getchar()) != EOF) {
                putchar(c);
        }
        return 0;
}

```
`while ((c = getchar()) != EOF)` 와 같이 대입과 동시에 비교하는 코드는 매우 편리하지만 대입 연산자(=)보다 비교 연산자(`!=, ==, >, <, >=, <=`)가 우선순위가 높다는 점을 주의하지 않으면 엉뚱한 결과를 초래할 수 있다.  
  
방금 본 문장에서 괄호를 제거하여 `while (c = getchar() != EOF)` 라고 쓰면 = 연산자보다 != 연산자의 우선순위가 높기 때문에 `while (c = (getchar() != EOF))` 라고 해석된다. 이 코드에서 c에는 **getchar()의 반환값이 저장될 거라는 기대와 달리 getchar()의 반환값과 파일의 끝을 나타내는 상수 EOF를 비교한 결과가 저장**된다. 그래서 c에는 입력된 문자가 아니라 참과 거짓을 나타내는 1 또는 0이 저장된다.