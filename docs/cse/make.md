---
layout: post
title: "make 사용법"
parent: "Computer Science"
nav_order: 2
---

# make 사용법

## Make의 기본 예제
```
app.out: main.o foo.o bar.o
    gcc -o app.out main.o foo.o bar.o

main.o: foo.h bar.h main.c
    gcc -c -o main.o main.c

foo.o: foo.h foo.c
    gcc -c -o foo.o foo.c

bar.o: bar.h bar.c
    gcc -c -o bar.o bar.c
```

```bash
$ make
```


## 빌드 규칙(ruld) 블록
```
<target>: <prerequisites>
    <recipe>
```
- **타겟(target):** 빌드 대상 이름. 실행 파일, 목적 프로그램 등 프로그램에 의해 생성된 파일의 이름을 주로 가리킨다.  
- **prerequistites:** 빌드 대상이 의존하는 파일 목록. target을 생성할 때 입력으로 사용되는 파일들을 가리킨다.  
- **레시피(recipe):** 빌드 대상을 생성하는 명령. 여러 줄로 작성할 수 있으며, 각 줄 시작에 반드시 탭(Tab) 문자로 들여쓰기를 해주어야 한다.  
  
  
## Incremental Build(증분 빌드)

## 변수
### 내장변수
- CC: 컴파일러
- CFLAGS: 컴파일 옵션
- OBJS: 중간 산물인 목적(object) 파일 목록
- TARGET: 빌드 대상(실행 파일) 이름
- LDFLAGS: 링커 옵션
- LDLIBS: 링크 라이브러리

**내장 변수 목록 출력**  
```bash
$ make -p
```
  
### 자동 변수
- $@: 현재 Target 이름
- $^: 현재 Target이 의존하는 대상들의 전체 목록
- $%  
- $<
- $?
- $+
- $!
- $*

```
CFLAGS = -g
ALL_CFLAGS = -I. $(CFLAGS)
.c.o:
        $(CC) -c $(CPPFLAGS) $(ALL_CFLAGS) $<
```

### 가짜(Phony) 타겟
```
.PHONY: clean
clean:
    rm *.o temp
```

포니 타겟은 실제 파일 이름을 나타내는 타겟 이름이 아니다. 이는 명시적으로 make 요청을 하는 경우에 실행되는 명령을 위한 목적으로 사용된다. 포니 타겟을 사용하는 이유는 두 가지가 있는데, 첫째는 동일한 이름의 파일을 사용한 충돌을 피하기 위함이고, 둘째는 make 성능 향상을 위함이다.

.PHONY: clean
일단 이렇게 되면, make clean 명령은 clean 이라는 파일이 존재하는지 여부와 상관없이 명령을 수행할 것이다.
포니타겟으로 선언하는 것은 실제 파일이 존재하는 것을 신경쓰지 않아도 되기 때문에 좋은 성능을 보여 준다.

```
all: prog1 prog2 prog3
.PHONY: all

prog1: prog1.o utils.o
    cc -o prog1 prog1.o utils.o

prog2: prog2.o
    cc -o prog2 prog2.o

prog3: prog3.o sort.o utils.o
    cc -o prog3 pro3.o sort.o utils.o
```
