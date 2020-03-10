---
layout: post
title: "데이터 타입"
parent: Rust
grand_parent: Programming Language
nav_order: 4
---
* 변수
* 기본 타입
* 함수
* 주석
* 흐름 제어

1. 변수와 가변성
기본적으로 변수는 변경이 불가능하다. 안전하면서도 쉽게 동시성의 장점을 활용할 수 있는 코드를 작성하도록 돕기 위해 러스트가 제공하는 다양한 특징 중 하나다. 하지만 필요하다면 변수를 변경할 수 있게 선언할 수도 있다.

이러한 불변성에 따라 불변 변수는 한 번 값을 할당하면 값을 변경할 수 없다. 만약 값을 변경하려고 한다면 컴파일 단계에서 오류가 발생한다. 
```rust
fn main() {
    let x = 5;
    println("x의 값: {}", x);
    x = 6; // error!
    println("x의 값: {}", x);
}
```

가변 변수의 선언
```rust
fn main() {
    let mut x = 5;
    println("x의 값: {}", x);
    x = 6;
    println("x의 값: {}", x);
}
```