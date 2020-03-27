---
layout: post
title: "if-else 문"
parent: C
grand_parent: Programming Language
nav_order: 6
---

# if-else 문

if-else문은 프로그램 흐름을 결정하기 위해 쓰이는데 그 구문은 다음과 같다.  
```
if (expression)
    statement1
else
    statement2
```
여기에서 else 부분은 필요에 따라 있을 수도 있고 없을 수도 있다. 제일 먼저 수식(expression)이 계산되고, 그 계산이 참이면(즉, 그 수식 값이 **0이 아니면**) 문장(statement)1이 수행되며, 그 계산 값이 거짓(수식 값이 0)이고 else 부분이 있으면 문장2가 수행된다.  
  
if 문은 **수식의 값만을 검사**하기 때문에 프로그램을 간략화할 수 있다. 즉,
```
if (expression)
```
라고 쓰는 것이  
```
if (expression != 0)
```
라고 쓰는 것보다 훨씬 그 뜻을 명확하게 나타내 준다.  
경우에 따라서는 후자의 표현이 자연스러울 경우도 있으나 일반적으로 잘 사용하지 않는다.  
  
if-else 구문에서 여러 개의 if문이 나타난 경우에 else 문이 생략되면 의미가 불분명해질 수 있다. 이런 else는 **가장 가까운 if문의 else**로 생각함으로써 명확히 구분할 수 있다. 즉,
```
if (n > 0)
    if (a > b)
        z = a;
    else
        z = b;
```
이 경우 else는 안쪽의 if와 쌍을 이룬다. 만일 안쪽의 if와 쌍을 이루려는 의도가 아니라면 중괄호를 사용하여 뜻을 명확히 해야 한다. 즉,  
```
if (n > 0) {
    if (a > b)
        z = a;
}
else
    z = b;
```
  
다음의 예와 같이 else의 불분명한 사용이 엉뚱한 결과를 가져오기도 한다.  
if (n >= 0)
    for (i = 0; i < n; i++)
        if (s[i] > 0) {
            printf("...");
            return i;
        }
else /* WRONG */
    printf("error - - n is negative\n");
```
위 프로그램에서 프로그래머는 시각적으로 if와 else를 연결시키려 했지만, 컴파일러가 이 의도를 알 수 없으므로 else를 가장 안쪽의 if와 연관시키게 된다. 이런 종류의 실수는 무척 발견하기 힘들기 때문에 처음부터 주의해서 프로그램을 작성해야 한다. 중괄호를 적절히 사용하는 것도 이러한 실수를 줄이는 좋은 방법이다.  
```
  
<br>

```
if (a > b)
    z = a;
else
    z = b;
```
위의 예에서 z = a 뒤에 세미콜론이 있는 것에 유의해야 한다. if 뒤에는 항상 문장이 와야 하고, `z = a`와 같은 수식 뒤에는 반드시 세미콜론이 와야 한다는 문법 때문이다.
