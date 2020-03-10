---
layout: post
title: "흐름 제어"
parent: Rust
grand_parent: Programming Language
nav_order: 6
---
# 흐름제어
## if 표현식
```rust
fn main() {
    let number = 3;
    
    if number < 5 {
        println!("조건이 일치합니다.");
    } else {
        println!("조건이 일치하지 않습니다.");
    }
}
```
  
한 가지 중요한 점은 if 문의 조건은 반드시 불리언 타입 중 하나를 반환해야 한다. 조건이 불리언을 반환하지 않으면 에러가 발생한다. 예를 들어 다음 코드를 실행해 보자.
```rust
fn main() {
    let number = 3;
    
    if number {
        println!("변수에 저장된 값은 3입니다.");
    }
}
```
이번에는 if 조건의 결과가 3이라는 값으로 평가되므로 러스트는 다음과 같은 에러를 발생한다.
```
   Compiling branches v0.1.0 (D:\projects\rust\branches)
error[E0308]: mismatched types
  --> src\main.rs:15:5
   |
15 |     if number {
   |        ^^^^^^ expected `bool`, found integer

error: aborting due to previous error

For more information about this error, try `rustc --explain E0308`.
error: could not compile `branches`.
```
에러 메시지를 보면 러스트는 불리언 타입의 결과를 원했지만(exprected \`bool\`, found integer), 정수 타입의 결과가 반환되었다고 한다. 루비나 자바스크립트 같은 언어와 달리 러스트는 불리언이 아닌 값을 불리언으로 **자동으로 변환하지 않는다. 그래서 반드시 if 표현식의 조건을 불리언으로 제공해야 한다.** 예를 들어, if 코드 블록을 number 변수의 값이 0이 아닐 때만 실행하려면 if 표현식을 다음처럼 작성한다.
```rust
fn main() {
    let number = 3;
    
    if number != 0 {
        println!("변수에 저장된 값은 0이 아닙니다.");
    }
}
```
  
### (1) else if를 이용해 여러 조건을 처리하기
```rust
fn main() {
    let number = 6;
    
    if number % 4 == 0 {
        println!("변수가 4로 나누어떨어집니다.");
    } else if number % 3 == 0 {
        println!("변수가 3으로 나누어떨어집니다.");
    } else if number % 2 == 0 {
        println!("변수가 2로 나누어떨어집니다.");
    } else {
        println!("변수가 4, 3, 또는 2로 나누어떨어지지 않습니다.");
    }
}
```
이 프로그램은 if 표현식을 차례대로 평가해서 조건이 처음으로 일치하는 표현식의 본문을 실행한다. 6이라는 값은 2로도 나누어 떨어지지만, 두 번째 조건이 일치했기 때문에 그 아래의 조건들은 평가되지 않고 넘어간다.
```
> cargo run
   Compiling branches v0.1.0 (D:\projects\rust\branches)
    Finished dev [unoptimized + debuginfo] target(s) in 0.71s
     Running `target\debug\branches.exe`
변수가 3으로 나누어떨어집니다.
```
  
else if 표현식을 너무 많이 사용하면 코드가 지저분해 보이므로 둘 이상의 else if 표현식이 필요할 때는 코드를 리팩토링(refactoring)해야 한다. 이에 대한 자세한 내용은 match 구조에서 다룰 것이다.  
  
### (2) let 구문에서 if 표현식 사용하기
if는 표현식(expression)이므로 다음과 같이 let 구문 오른쪽에 사용할 수도 있다.
```rust
fn main() {
    let condition = true;
    let number = if condition {
        5
    } else {
        6
    };
    
    println!("number의 값: {}", number);
}
```
이 예제에서 number 변수에는 if 표현식의 결과가 대입된다.
```
> cargo run
   Compiling branches v0.1.0 (D:\projects\rust\branches)
    Finished dev [unoptimized + debuginfo] target(s) in 0.88s
     Running `target\debug\branches.exe`
number의 값: 5
```
코드 블록의 결과는 마지막 표현식의 값을 평가하며 숫자 자체도 하나의 표현식임을 기억하자. 이때 if 표현식 전체의 결과는 어떤 코드 블록이 실행되는가에 따라 달라진다. 따라서 if 구문의 각 가지가 반환하는 결과는 모두 같은 타입이어야 한다. 위의 예제의 경우 if와 else 표현식의 코드 블록 모두 i32 정수를 반환하기 때문에 문제 없이 실행된다. 그러나 다음 예제처럼 타입이 일치하지 않으면 컴파일 에러가 발생한다.
```rust
fn main() {
    let condition = true;
    let number = if condition {
        5
    } else {
        "six"
    };
    println!("number의 값: {}", number);
}
```
  
```
> cargo run
   Compiling branches v0.1.0 (D:\projects\rust\branches)
error[E0308]: if and else have incompatible types
  --> src\main.rs:53:9
   |
50 |       let number = if condition {
   |  __________________-
51 | |         5
   | |         - expected because of this
52 | |     } else {
53 | |         "six"
   | |         ^^^^^ expected integer, found `&str`
54 | |     };
   | |_____- if and else have incompatible types

error: aborting due to previous error

For more information about this error, try `rustc --explain E0308`.
error: could not compile `branches`.
```
러스트는 number 변수를 사용하는 모든 코드의 유효성을 검사하기 위해 **컴파일 시점에** number 변수의 타입이 무엇인지를 알아야 한다. number 변수의 타입이 런타임에 결정된다면 러스트는 이런 유효성 검사를 수행할 수 없다. 그러면 컴파일러의 구조가 더 복잡해질뿐더러 변수의 타입 변경을 추적해야 한다면 컴파일러는 지금만큼 코드의 실행의 보장할 수 없다.  
  
  
## 루프를 이용한 반복
러스트는 `loop`, `while`, `for`라는 세 가지 종류의 루프를 제공한다. 지금부터 하나씩 살펴보기로 하자.  
  
 
### (1) loop를 이용한 반복 실행
`loop` 키워드는 루프를 중지하라고 명시적으로 설정하지 않는 한, 코드 블록을 무한으로 반복해서 실행한다. 러스트는 루프에서 탈출하기 위한 방법으로 `break` 키워드를 제공한다.
```rust
fn main() {
    let mut count = 0;
    loop {
        println!("count: {}", count);
        count += 1;
        if count >= 5 {
            break;
        }
    }
}
```
  
### (2) 루프에서 값 반환하기
루프를 이용하는 방법 중 하나는 스레드가 작업을 완료했는지 여부를 확인하는 등 실패할 가능성이 있는 작업을 재시도하는 경우다. 하지만 작업의 결과를 다른 코드에 전달해야 할 수도 있다. 그러려면 루프를 중단하는 break **표현식** 다음에 반환하고자 하는 값을 추가하면 된다. 다음 예제에서 확인할 수 있듯이 이 값은 루프 외부로 반환되어 나머지 코드에서 사용할 수 있다.
```rust
fn main() {
    let mut counter = 0;
    
    let result = loop {
        counter += 1;
        if counter == 10 {
            break counter * 2;
        }
    };
    
    println!("The result is {}", result);
}
```
  
### (3) while을 이용한 조건 루프
간혹 조건식의 평가 결과에 따라 루프를 실행해야 할 때가 있다. 이런 종류의 반복문은 loop, if, else, break 키워드를 조합해서 만들 수도 있지만 `while` 루프를 사용하는 것이 일반적이다.
```rust
fn main() {
    let mut number = 3;

    while number != 0 {
        println!("{}!", number);
        number = number - 1;
    }
    println!("발사!");
}
```
  
### (4) for를 이용해 컬렉션을 반복 처리하기
while 구문은 배열 같은 컬렉션의 각 요소를 반복 처리할 때도 사용할 수 있다.
```rust
fn main() {
    let a = [10, 20, 30, 40, 50];
    let mut index = 0;

    while index < 5 {
        println!("요소의 값: {}", a[index]);
        index += 1;
    }
}
```
하지만 이 방법은 에러가 발생할 확률이 높다. 즉, 배열의 길이를 잘못 지정하면 프로그램은 패닉 상태에 빠져 종료된다. 또한, 루프를 반복할 때마다 컴파일러가 조건을 검사하는 런타임 코드를 추가로 삽입해야 하므로 속도도 느리다. 더 손쉬운 방법은 for 구문을 이용해 컬렉션 내의 요소들을 반복해서 처리하는 것이다.
```rust
fn main() {
    let a = []10, 20, 30, 40, 50;

    for element in a.iter() {
        println!("요소의 값: {}", element);
    }
}
```
이 예제는 while을 사용했을 때보다 안정성이 더 높으며, 배열의 길이를 잘못 지정해서 배열의 끝을 넘어서거나 일부 요소를 처리하지 못하는 버그를 사전에 방지할 수 있다.  
  
for 루프는 그 안전성과 간결함 덕분에 러스트에서 가장 많이 사용된다. 다음 예제처럼 일정 횟수만 반복하고자 할 때도 for 루프를 사용한다. 그 방법은 표준 라이브러리에 포함되어 있으며, 한 숫자에서 다른 숫자 사이에 존재하는 모든 숫자를 생성해 주는 `Range` 타입을 이용한다. for 구문과 더불어 아직 살펴보지 않았지만 범위를 뒤집어서 생성하는 `rev` 메서드를 혼합해서 카운트다운 예제를 다시 작성해 보자.
```rust
fn main() {
    for number in (1..4).rev() {
        println!("{}!", number);
    }
    println!("발사!");
}
``` 
  
```
> cargo run
   Compiling loops v0.1.0 (D:\projects\rust\loops)
    Finished dev [unoptimized + debuginfo] target(s) in 0.57s
     Running `target\debug\loops.exe`
3!
2!
1!
발사!
```
