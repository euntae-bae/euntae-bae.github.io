---
layout: post
title: "전역 변수의 선언"
parent: C
grand_parent: Programming Language
nav_order: 2
---

# 전역 변수의 선언
### (p.42)
프로그램을 작성하다 보면 여러 함수에서 공통으로 사용되는 변수가 필요한 경우가 있다. 이런 변수를 전역(global)변수라 하고 전역 변수를 정의할 때 extern이라는 명령어를 사용한다.
```c
#include <stdio.h>

#define MAXLINE 1000

int max;
char line[MAXLINE];
char longest[MAXLINE];

int my_getline(void);
void copy(void);

int main(void)
{
    int len;
    extern int max;
    extern char longest[];
    max = 0;
    while ((len = my_getline()) > 0)
        if (len > max) {
            max = len;
            copy();
        }
    if (max > 0)
        printf("%s", longest);
    return 0;
}

int my_getline(void)
{
    int c, i;
    extern char line[];

    for (i = 0; i < MAXLINE - 1 && (c = getchar()) != EOF && c != '\n'; ++i)
        line[i] = c;
    if (c == '\n') { // 입력된 문자가 개행문자일 경우 문자열의 끝에 개행문자를 덧붙인다.
        line[i] = c;
        ++i;
    }
    line[i] = '\0';
    return i;
}

void copy(void)
{
    int i;
    extern char line[], longest[];
    
    i = 0;
    while ((longest[i] = line[i]) != '\0')
        ++i;
}
```
전역변수를 사용하는 함수가 전역변수 선언과 같은 파일에 들어 있는 경우에는 함수 내에서 extern 선언을 해 주지 않아도 된다. 그러므로 위 프로그램의 함수 내에 들어 있는 extern 선언들은 생략할 수 있다. 그런데 만약 copy 함수가 다른 파일에 있다면 copy 함수 내의 extern 선언은 꼭 있어야 한다.