---
layout: post
title: "함수"
parent: Rust
grand_parent: Programming Language
nav_order: 5
---
# 러스트의 함수
러스트 코드는 함수와 변수의 이름에 스네이크 케이스(snake case)를 사용한다.
```rust
fn main() {
    println!("안녕하세요!");
    another_function();
}

fn another_function() {
    println!("또 다른 함수");
}
```
러스트에서 함수의 선언 순서는 중요하지 않으며 어디에 선언했는지가 중요하다.  
  
## 함수 매개변수
매개변수는 함수의 시그니처(signature)에 포함되는 특별한 변수다. 함수에 매개변수가 정의되어 있으면 이 매개변수에 구체적인 값(인수argument)을 전달할 수 있다. 다음은 매개변수를 사용하여 다시 작성한 예제다.
```rust
fn main() {
    another_function(5);
}

fn another_function(x: i32) {
    println!("x의 값: {}", x);
}
```
함수 시그니처에는 각 매개변수의 타입을 명시해야 한다. 이것은 러스트의 의도적인 디자인이다. 함수 정의에 타입 애노테이션(annotation)을 포함하도록 하면 컴파일러가 각 매개변수가 코드 내에서 어떻게 사용되는지 일일이 추적하지 않아도 그 타입을 정확히 확인할 수 있다.  
  
함수에 여러 개의 매개변수를 선언할 때는 각 매개변수를 쉼표로 구분하면 된다. 모든 매개변수가 반드시 같은 타입일 필요는 없다.
```rust
fn main() {
    another_function();
}

fn another_function(x: i32, y: i32) {
    println!("x의 값: {}", x);
    println!("y의 값: {}", y);
}
```

## 함수 본문의 구문(statement)과 표현식(expression)
함수 본문은 여러 개의 **구문(statements)**으로 구성되며, 선택적으로 **표현식(expression)**으로 끝나기도 한다. 러스트는 표현식 기반 언어여서 구문과 표현식을 구분하는 것은 매우 중요하다. 다른 언어는 이런 구분이 존재하지 않으므로 구문과 표현식이 각각 무엇이며, 함수의 본문에 미치는 영향은 어떻게 다른지 확인해볼 필요가 있다. 
  
**구문**은 어떤 동작을 실행하지만 값을 반환하지 않는 명령이다. 반면, **표현식**은 최종 결괏값으로 평가(evaluate)된다.  
`let`키워드를 이용해 변수를 생성하고 값을 대입하는 것은 구문이다. 다음 예제에 작성한 `let y = 6;`은 구문이다.  
```rust
fn main() {
    let y = 6;
}
```
함수 선언 역시 구문에 속한다. 따라서 위의 코드는 구문 안에 구문이 포함된 예이다. 구문은 값을 반환하지 않으므로 `let` 구문은 다른 변수에 대입할 수 없다. 만일 다음과 같은 코드를 작성했다면 컴파일 에러가 발생한다.
```rust
fn main() {
    let x = (let y = 6);
}
```
바로 이 점이 C나 루비 같은 언어와 다른 점이다. 이런 언어에서 `x = y = 6`과 같은 구문을 작성하면 x와 y 변수의 값이 모두 6이다. 그러나 러스트에서는 이런 결과는 얻을 수 없다.  
  
**표현식**은 어떤 값으로 평가된다. `5 + 6`처럼 간단한 산술 연산을 생각해 보자. 이는 표현식이므로 11이라는 값으로 평가된다. 표현식은 구문의 일부가 될 수 있다. 예를 들어 `let y = 6;` 구문에서 6이라는 값은 6으로 평가되는 표현식이다. **함수의 호출** 역시 표현식이다. 마찬가지로 **매크로의 호출**도 표현식이다. 새로운 범위를 선언하기 위한 **코드 블록({})** 역시 표현식이다.
```rust
fn main() {
    let x = 5;
    // 코드 블록의 선언: 코드 블록은 4라는 값으로 평가된다.
    let y = { // y에는 4가 대입된다.
        let x = 3;
        x + 1 // 표현식에는 세미콜론이 붙지 않는다.
    };
}
```
예제에 있는 코드 블록은 4라는 값으로 평가된다. 이 값은 let 구문에 의해 변수 y에 할당된다. 표현식은 마지막에 세미콜론을 포함하지 않는다는 점에 유의해야 한다. 만일 여기에 세미콜론을 추가하면 표현식이 구문으로 바뀌어 값을 반환하지 않는다.  
  
## 값을 반환하는 함수
함수는 자신을 호출한 코드에 값을 반환할 수 있다. 반환값에는 이름을 부여하지는 않지만, 반환할 값의 타입은 화살표(->) 다음에 지정해 주어야 한다. 러스트에서 함수의 반환값은 **함수 본문의 마지막 표현식의 값**이라고 생각하면 된다. 물론, 함수 본문의 실행이 완전히 끝나지 않은 부분에서도 `return` 키워드와 함께 특정한 값을 반환할 수 있다. 하지만 대부분 함수는 마지막 표현식의 결과를 반환한다.  
```rust
fn five() -> i32 {
    5
}

fn main() {
    let x = five();
    println!("x의 값: {}", x);
}
```
  
다른 예제를 살펴보자
```rust
fn main() {
    let x = plus_one(5);
    println!("x의 값: {}", x);
}

fn plus_one(x: i32) -> i32 {
    x + 1
}
```
이 코드를 실행하면 `x의 값: 6`이라는 결과가 출력된다. 하지만 `x + 1` 표현식 뒤에 세미콜론을 추가하면, 이 표현식이 구문으로 바뀌어 에러가 발생한다.
```rust
fn main() {
    let x = plus_one(5);
    println!("x의 값: {}", x);
}

fn plus_one(x: i32) -> i32 {
    x + 1; // error!
}
```
이 구문은 값으로 값으로 평가되지 않고 빈 튜플인 ()로 표현되기 때문에 '타입 불일치' 오류가 발생한다.  
```
   Compiling functions v0.1.0 (D:\projects\rust\functions)
error[E0308]: mismatched types
 --> src\main.rs:1:24
  |
1 | fn plus_one(x: i32) -> i32 {
  |    --------            ^^^ expected `i32`, found `()`
  |    |
  |    implicitly returns `()` as its body has no tail or `return` expression
2 |     x + 1;
  |          - help: consider removing this semicolon

error: aborting due to previous error

For more information about this error, try `rustc --explain E0308`.
error: could not compile `functions`.

To learn more, run the command again with --verbose.
```
  