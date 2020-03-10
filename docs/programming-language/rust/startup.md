---
layout: post
title: "러스트 시작하기"
parent: Rust
grand_parent: Programming Language
nav_order: 1
---
# 러스트 시작하기
## 1. 개발 환경
### 1.1 rustup 설치하기
러스트를 시작하기 위해서는 러스트의 버전과 관련된 도구들을 관리하는 프로그램인 **rustup**을 설치해야 한다. rustup은 다음 링크에서 구할 수 있다.  
<https://www.rust-lang.org/tools/install>  
  
### 1.2 rustup 명령어
rustup을 이용하면 러스트의 최신 버전으로 쉽게 업데이트 할 수 있다.
```bash
$ rustup update
```
  
rustup 도구와 러스트를 제거하는 명령어는 다음과 같다.
```bash
$ rustup self uninstall
```
  
rustc는 러스트 컴파일러이다. 러스트가 제대로 설치됐는지 확인하기 위해서는 다음과 같이 --version 옵션을 줘서 rustc를 실행하면 된다.
```bash
$ rustc --version
```
  
러스트를 설치하면 오프라인에서도 읽을 수 있는 러스트 API 문서도 같이 설치된다. 다음 명령어를 실행하면 로컬에 저장된 웹 문서를 읽을 수 있다.
```bash
$ rustup doc
```
  
  
## 2. 첫 예제
러스트 컴파일러인 rustc의 사용법은 gcc나 clang과 같은 여느 명령행 환경용 컴파일러와 유사하다. `$ rustc <file>`처럼 컴파일러에 소스 파일을 전달하면 컴파일 결과물(실행파일, 디버깅 정보)을 내보낸다.  
지금부터 예제를 위한 별도의 디렉토리를 생성할 것이다. 앞으로의 예제들은 기본적으로 이 디렉토리 안에서 진행할 것이다. 우선 본인이 접근하기 편한 경로를 하나 선정해서 그곳에 새로운 디렉토리를 하나 생성하자. 디렉토리 생성 명령어는 유닉스 계열 운영체제나 윈도우즈 파워셸에서는 `mkdir`을 사용한다. 윈도우즈 cmd(명령 프롬프트)에서는 `md`명령어를 사용한다.
```bash
$ mkdir project
```
생성한 디렉토리에 들어가거나 상위 디렉토리로 나가는 등 디렉토리를 이동하려면 `cd`명령어를 사용하면 된다. 현재 디렉토리나 상위 디렉토리는 각각 특수 기호`.`과 `..`으로 표현한다. 예를 들어 project 디렉토리에 들어갔다가 다시 상위 디렉토리로 나가려면 다음과 같이 입력하면 된다.
```bash
$ cd project
$ cd ..
```
  
우리가 처음 만들 예제는 터미널 화면에 Hello World!를 출력하는 것이다. project 디렉토리(이름이 반드시 project일 필요는 없다)에서 다시 Hello World 예제를 위한 디렉토리를 생성하자.
```bash
$ mkdir hello_world
$ cd hello_world
```
  
러스트 소스파일은 확장자로 .rs를 사용한다. 텍스트 편집기를 이용하여 `main.rs`라는 이름의 소스 파일을 하나 생성하자.  
```rust
// main.rs
fn main() {
    println!("Hello World!");
}
```
이 코드를 컴파일하고 실행해보기 앞서 잠시 이 예제를 통해 드러나는 러스트의 특징 몇 가지를 언급하고자 한다. 기존에 자신이 접했던 언어들과 공통점과 차이점이 있을 것이다.
* 러스트에서의 들여쓰기는 탭(\t)이 아니라 공백 문자 4개를 사용한다.
* println!은 **러스트 매크로**이다. ! 기호가 뒤에 붙으면 함수가 아니라 매크로다.
* 각 구문은 세미콜론(;)으로 끝난다.
  
러스트 컴파일러를 이용하여 main.rs를 컴파일 하려면 다음과 같이 입력하면 된다.
```bash
$ rustc main.rs
```
컴파일 결과물로 실행 파일인 main.exe와 윈도우즈 디버깅 정보인 main.pdb가 새로 생성된다.  
  
  
## 3. Cargo
카고(Cargo)는 러스트의 빌드 시스템이자 패키지 관리자이다. 카고는 코드의 빌드, 의존 라이브러리(dependencies)의 다운로드, 라이브러리의 빌드 등 다양한 작업을 대신 처리해 준다. 러스트를 설치하면 카고도 자동으로 설치된다. 만약 카고의 설치 여부를 점검하고 싶다면 다음과 같이 버전 확인 명령어를 사용하면 된다.
```bash
$ cargo --version
```
만약 이 명령어가 실행되지 않는다면 카고를 따로 설치하는 방법을 찾아보길 바란다.  
  
### 3.1 카고를 이용해 프로젝트 생성하기
```bash
$ cargo new <project_name>
```  
  
처음에 생성했던 Hello, world! 프로젝트를 카고를 이용해 다시 생성해보자.
```bash
$ cargo new hello_cargo
```
이 명령어는 `hello_cargo`라는 새로운 디렉토리를 생성한다. 프로젝트 이름을 `hello_cargo`라고 지정했으므로 카고는 필요한 파일을 프로젝트의 이름과 같은 디렉토리에 생성한다.  
  
hello_cargo 디렉토리로 들어가 파일의 목록을 살펴보자. 그러면 카고가 main.rs 파일이 보관된 src 디렉토리와 Cargo.toml 파일을 생성해 준 것을 확인할 수 있다. 또한, .gitignore 파일과 함께 해당 디렉토리가 새로운 깃(Git) 저장소로 초기화 된 것도 알 수 있다.

![hello_cargo 디렉토리](/image/rust-startup-1.png)
  
![hello_cargo/src 디렉토리](/image/rust-startup-2.png)
  
Cargo.toml은 카고의 설정 파일이다. 만약 텍스트 편집기를 이용해 연다면 다음과 같은 모습을 하고 있을 것이다.
```toml
[package]
name = "hello_cargo"
version = "0.1.0"
authors = ["작성자이름 <메일주소>>"]
edition = "2018"

# See more keys and their definitions at https://doc.rust-lang.org/cargo/reference/manifest.html

[dependencies]
```
첫 번째 줄의 `[package]`는 패키지 설정을 관리하기 위한 구문들이 시작됨을 의미하는 섹션의 제목이다. 이 파일에 더 많은 정보를 추가할수록 다른 섹션들이 더 추가된다.  
  
섹션 제목 다음의 네 줄은 카고가 프로그램을 컴파일할 때 필요한 이름, 버전 및 작성자, 그리고 러스트가 사용할 에디션 등의 설정 정보를 지정하는 코드다. 카고는 현재 시스템 환경에서 작성자의 이름과 메일 주소를 읽기 때문에 이 정보가 올바르지 않다면 해당 정보를 지금 수정하고 파일을 저장하도록 하자.  
  
마지막 줄의 `[dependencies]`는 프로젝트의 의존 라이브러리 목록을 관리하는 섹션이 시작하는 부분이다. 러스트에서 코드의 패키지는 '크레이트(crate)'라고 부른다. 이 프로젝트는 아직 별도의 크레이트가 필요하지 않다.  
  
src/main.rs를 열어보면 다음과 같은 코드가 자동으로 생성되어 있는 것을 확인할 수 있다. 다음 절에는 이 코드를 직접 빌드해서 실행해 볼 것이다.
```rust
fn main() {
    println!("Hello, world!");
}
```
  
### 3.2 프로젝트 빌드
프로젝트를 빌드하려면 다음과 같이 `cargo build` 명령어를 사용하면 된다.
```bash
$ cargo build
```
이 명령을 실행하면 현재 디렉토리가 아니라 `target/debug/hello_cargo`경로에 실행 파일이 생성된다.  
cargo build 명령을 처음 실행하면 카고는 최상위 디렉토리에 `Cargo.lock`이라는 파일을 생성한다. 이 파일은 프로젝트에 필요한 의존 패키지의 정확한 버전을 추적하기 위한 파일이다. 이 파일은 우리가 직접 관리하는 파일이 아니라 카고가 알아서 관리한다.  
  
카고를 이용하여 하나의 명령어로 코드를 컴파일하고 실행하는 방법은 다음과 같다.
```bash
$ cargo run
```
`cargo run` 명령어를 실행하면 다음과 같이 출력된다.
```
> cargo run
    Finished dev [unoptimized + debuginfo] target(s) in 0.06s
     Running `target\debug\hello_cargo.exe`
Hello, world!
```
카고는 소스 파일이 변경되지 않았음을 탐지하고 곧바로 바이너리를 실행했기 때문에 컴파일을 실행했다는 결과가 출력되지 않는다. 반면 소스 코드를 수정하고 다시 `cargo run` 명령을 실행하면 다음과 같이 출력된다.
```
> cargo run
   Compiling hello_cargo v0.1.0 (D:\projects\rust\hello_cargo)
    Finished dev [unoptimized + debuginfo] target(s) in 1.25s
     Running `target\debug\hello_cargo.exe`
Hello, world!
```
  
카고는 `cargo check`라는 명령어 또한 지원한다. 이 명령은 코드의 컴파일 여부를 신속하게 검사하지만 실행 파일은 생성하지 않는다. 통상적으로 cargo check 명령은 실행 파일을 생성하는 과정을 생략하므로 cargo build 명령보다 훨씬 빠르게 실행된다. 따라서 코드를 작성하는 동안 작업 결과에 오류가 없는지를 계속 확인하려면 cargo check 명령을 이용하는 편이 훨씬 빠르다.
```bash
$ cargo check
```  
  
### 3.3 릴리즈를 위한 빌드
프로젝트를 릴리즈할 준비가 되면 `cargo build --release`를 이용해서 최적화된 컴파일을 실행할 수 있다. 이 명령은 `target/debug`가 아닌 `target/release` 경로에 실행 파일을 생성한다. 이때 실행되는 최적화 덕분에 러스트 코드는 더 빠르게 실행되지만, 프로그램을 컴파일하는 시간은 더 길어진다. 더 빨리 자주 컴파일하기 위한 개발용 프로필과, 최종 완성된 프로그램을 사용자에게 제공하기 위해 최대한 빠르게 실행될 수 있도록 컴파일하기 위한 프로필이 별개로 분리된 이유는 바로 이 때문이다. 코드의 실행 시간을 벤치마킹해 보려면 cargo build --release 명령을 이용해 빌드한 후 target/release 경로의 실행 파일을 이용해 벤치마킹을 실행하기 바란다.
  