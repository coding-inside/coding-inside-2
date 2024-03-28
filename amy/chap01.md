###### date | 2024.03.11 ~ 2024.03.16

###### week | 2nd week

<hr />
<br />

## 01. 디자인 패턴

프로그램을 설계할 때 발생했던 문제점들을 해결할 수 있도록 하나의 **규약** 형태로 만들어 놓은 것

### 싱글톤 패턴

###### singleton pattern

<p align="center">
<img width="70%"  src="https://github.com/inside-coding/cs-note/assets/134191817/ac3c6024-3b28-47c2-b6e7-5f2007bba126">
</p>

- 하나의 클래스에 하나의 인스턴스 <br />
- 하나의 인스턴스를 다른 모듈들이 공유하며 사용하는 형태 <br />
- 보통 데이터베이스 연결 모듈이 많이 사용

##### 🟢 PROS

인스턴스 생성 비용 절감 <br />
실용적 <br />

##### 🔴 CONS

의존성이 높음 <br />
모듈 간의 결합을 강하게 함 → 의존성 주입으로 해결 가능 <br />
TDD의 걸림돌 <br />

###### TDD?

    Test Driven Development.
    주로 단위 테스트를 하는데 이때 테스트는 서로 독립적이어야 하며 테스트를 어떤 순서로든 실행 가능해야 함.

###### 의존성 주입?

**원칙** <br />
"상위 모듈은 하위 모듈에서 어떠한 것도 가져오지 않아야 한다. 또한 둘 다 추상화에 의존해야 하며, 이때 추상화는 세부 사항에 의존하지 말아야 한다."

<p align="center">
<img width="60%" src="https://github.com/inside-coding/cs-note/assets/134191817/1c12691c-1335-4565-bf4b-8930e1deb180" />
</p>

    DI, Dependency Injection.
    "의존성이 떨어진다" === "디커플링 된다"

###### 🟢 PROS

테스팅에 용이 <br />
수월한 마이그레이션 <br />
일관된 애플리케이션의 의존성 방향 <br />
애플리케이션의 쉬운 추론 <br />
모듈 간 관계들의 명확성 보장

###### 🔴 CONS

분리된 모듈들로 복잡성 증가 <br />
약간의 런타임 패널티

<br />

##### example

JS에서는 리터럴('{}') 또는 new Object로 객체 생성만으로도 싱글톤 패턴 구현이 가능 → 다른 어떤 객체와도 같지 않으므로

```javascript
const obj1 = { a: 27 };
const obj2 = { a: 27 };

console.log(obj1 === obj2); // false
```

실제 싱글톤은 아래와 같은 코드로 구성

```javascript
class Singleton {
  constructor() {
    if (!Singleton.instance) {
      Singleton.instance = this;
    }
    return Singleton.instance;
  }
  getInstance() {
    return this.instance;
  }
}

const a = new Singleton();
const b = new Singleton();
console.log(a === b); // true
```

<br />

### 팩토리 패턴

###### factory pattern

<p align="center">
<img width="70%"  src="https://github.com/inside-coding/cs-note/assets/134191817/6a32e896-3963-4548-ad9e-aaaea86eb7c9">
</p>

- 객체를 사용하는 코드에서 객체 생성 부분을 떼어내 추상화한 패턴
- 상속 관계에 있는 두 클래스에서 상위 클래스가 중요한 뼈대, 하위 클래스에서 구체적인 내용을 결정하는 패턴
- 클래스가 상위, 하위로 분리되므로 느슨한 결합으로 인해 유연성 ⬆️

##### 🟢 PROS

유지 보수성 용이 <br />

##### 🔴 CONS

<br />

###### example

```javascript
const num = new Object(123);
const str = new Object("abc");
num.constructor.name; // Number
str.constructor.name; // String
```

<br />

### 전략 패턴 (정책 패턴)

###### strategy pattern (policy pattern)

<p align="center">
<img width="70%" src="https://github.com/inside-coding/cs-note/assets/134191817/425e9a53-0226-420b-bae2-a568fc43f22b">
</p>

- 객체의 행위를 변경하고 싶은 경우 직접 수정 ❌
- 전략(캡슐화한 알고리즘)으로 컨텍스트 안에서 바꿔주며 상호 교체가 가능하도록 설계
- ex) 결제 시 네이버페이, 카카오페이 등 다양한 방법으로 결제하는 것

<br />

#### passport의 전략 패턴

전략 패턴을 활용한 라이브러리

<br />

### 옵저버 패턴

###### observer pattern

- 어떤 객체의 상태 변화를 관찰 → 변화 시 옵저버들에게 변화 알리기

<p align="center">
<img width="45%" src="https://github.com/inside-coding/cs-note/assets/134191817/d97af49f-3aaf-4a76-9a33-88c7da9bc322">
<img width="36%" src="https://github.com/inside-coding/cs-note/assets/134191817/a7a6bb87-19eb-4f03-b3ec-fe1925b63c25">
</p>

- 주체 : 객체의 상태 변화를 보고 있는 관찰자
- 옵저버 : 객체의 상태 변화에 따라 전달되는 것을 기반으로 **추가 변경 사항**이 생기는 객체들

- 주체와 객체를 따로 두지 않고 상태가 변경되는 객체를 기반으로 구축되기도 함
- ex) 트위터

<p align="center">
<img width="50%" src="https://github.com/inside-coding/cs-note/assets/134191817/baf358ab-fcbf-4785-8440-419a241236ae">
</p>

<br />

##### | MVC pattern

옵저버 패턴은 주로 이벤트 기반 시스템에 사용하며 MVC 패턴에도 사용됨

<p align="center">
<img width="70%" src="https://github.com/inside-coding/cs-note/assets/134191817/ec4633df-3ba1-4846-8f40-0b764a7fe393">
</p>

<br />

##### | Proxy

자바스크립트에서의 옵저버 패천은 프록시 객체를 통해 구현 가능

**| proxy 객체**란?

어떠한 대상의 기본적인 동작(속성 접근, 할당, 순회, 열거 함수 호출 등)의 작업을 가로챌 수 있는 객체로, 자바스크립트에서 프록시 객체는 두 개의 매개변수를 가진다.

1️⃣ target: 프록시할 대상 <br />
2️⃣ handler: target 동작을 가로채 어떤 동작을 할 것인지 설정돼 있는 함수

[함수]

- get( ) : 속성과 함수에 대한 접근을 가로챈다.
- has( ) : in 연산자의 사용을 가로챈다.
- set( ) : 속성에 대한 접근을 가로챈다.

```javascript
// 프록시 객체
const handler = {
  get: function(target, name){
    ...
  }
}
const intercept = new Proxy({}, handler)
```

<br />

### 프록시 패턴

###### proxy pattern

대상 객체에 접근 전 접근에 대한 흐름을 가로채 필터링하거나 수정하는 등의 역할을 하는 계층이 있는 디자인 패턴

<p align="center">
<img width="70%" src="https://github.com/inside-coding/cs-note/assets/134191817/6a4d55e2-f4ac-4615-995e-31d4dc3342cf">
</p>

객체의 속성, 변환 등을 보완 <br />
보안, 데이터 검증, 캐싱, 로깅에 사용 <br />
프록시 객체로도 프록시 서버로도 쓰임 <br />

##### 프록시 서버

서버와 클라이언트 사이에서 클라이언트가 자신을 통해 다른 네트워크 서비스에 간접적으로 접속할 수 있게 해주는 컴퓨터 시스템이나 응용 프로그램 <br />
CORS 에러 해결책 중 하나이며 다양한 API 서버와의 매끄러운 통신 가능

- nginx
- **CloudFlare**

  CDN(Content Delivery Network) 서비스 <br />
  DDOS 공격 방어 및 HTTPS 구축에 사용

<br />

### 이터레이터 패턴

###### iterator pattern

이터레이터를 사용해 컬렉션의 요소들에 접근하는 디자인 패턴 <br />

순회할 수 있는 여러 가지 자료형의 구조와는 상관 없이 이터레이터라는 하나의 인터페이스로 순회 가능

<p align="center">
<img width="60%" src="https://github.com/inside-coding/cs-note/assets/134191817/85a4c4ab-3f42-4111-9f38-a454918aaac1">
</p>

###### example

다른 자료구조인 set, map 임에도 **for ~ of ~** 로 순회 가능

```javascript
const mp = new Map();
mp.set("a", 1);
mp.set("b", 2);
mp.set("c", 3);

const st = new Set();
st.add(1);
st.add(2);
st.add(3);

for (let a of mp) console.log(a); // ['a', 1] ['b', 2] ['c', 3]
for (let a of st) console.log(a); // 1 2 3
```

<br />

### 노출모듈 패턴

###### revealing module pattern

즉시 실행 함수를 통해 접근 제어자를 만드는 패턴

자바스크립트는 접근 제어자가 존재하지 않고, 전역 범위에서 스크립트가 실행 <br />
따라서 노출모듈 패턴을 통해 접근 제어자를 구현하기도 한다. <br />
자바스크립트 모듈 방식 👉 [CJS(CommonJS)]

##### 접근 제어자

<table>
  <tr>
    <td rowspan="2">접근 제어자</td>
    <td rowspan="2">접근 가능 위치</td>
    <td colspan="2">접근 범위</td>
  </tr>
  <tr>
    <td>자식 클래스</td>
    <td>외부 클래스</td>
  </tr>
  <tr>
    <td>Public</td>
    <td rowspan="3">클래스에 정의된 함수에서 접근 가능</td>
    <td>O</td>
    <td>O</td>
  </tr>
  <tr>
    <td>Protected</td>
    <td>O</td>
    <td>X</td>  
  </tr>
  <tr>
    <td>Private</td>
    <td>X</td>
    <td>X</td>
  </tr>
</table>

<br />

### MVC 패턴

Model, View, Controller로 이뤄진 디자인 패턴

<p align="center">
<img width="70%" src="https://github.com/inside-coding/cs-note/assets/134191817/c83b41d7-70cb-4100-a102-fe4b6898aaf3">
</p>

애플리케이션의 구성 요소를 세 가지 역할로 구분해 개발 프로세스에서 각각의 구성 요소에만 집중해 개발 가능

##### 구성요소 설명

**| Model (모델)**

    View에서 데이터를 생성/수정하면 컨트롤러를 통해 모델을 생성/갱신

    애플리케이션의 데이터인 데이터베이스, 상수, 변수 등

**| View(뷰)**

    Model이 가지고 있는 정보를 따로 저장 X
    단순한 화면 표시 정보만 O
    변경이 일어나면 컨트롤러에 이를 전달

    모델을 기반으로 사용자가 볼 수 있는 화면으로 inputbox, checkbox, textarea 등 사용자 인터페이스 요소가 이에 해당

**| Controller(컨트롤러)** <br />

    하나 이상의 Model과 하나 이상의 View를 잇는 다리 역할
    이벤트 등 메인 로직을 담당
    Model과 View의 생명주기를 관리
    Model이나 View의 변경 통지 → 해석 → 각각의 구성 요소에 해당 내용 전달

<br />

##### 🟢 PROS

- 재사용성과 확장성이 용이

##### 🔴 CONS

- 애플리케이션이 복잡해질수록 Model과 View의 관계도 함께 복잡해짐

###### example

MVC 패턴을 이용한 대표적인 프레임워크는 자바 플랫폼을 위한 오픈 소스 애플리케이션 프레임워크인 **Spring(스프링)**

<br />

### MVP 패턴

MVC 패턴으로부터 파생된 패턴으로 Controller가 Presenter(프레젠터)로 교체된 패턴

<p align="center">
<img width="70%" src="https://github.com/inside-coding/cs-note/assets/134191817/093a0a0c-0059-4d09-81da-e8819a5f1f5b" />
</p>

View와 Presenter가 1:1 관계이므로 MVC 패턴보다 더 강한 결합을 지닌 패턴

<br />

### MVVM 패턴

MVC의 C에 해당하는 컨트롤러가 뷰모델(View Model)로 바뀐 패턴

<p align="center">
<img width="80%" src="https://github.com/inside-coding/cs-note/assets/134191817/840ba454-a9c7-4a4d-8eac-4716e1b9cd1f" />
</p>

뷰모델은 뷰를 더 추상화한 계층으로 MVC 패턴과는 다르게 커맨드와 데이터 바인딩을 가진다는 특징을 갖고 있다.

##### 🟢 PROS

- 뷰와 뷰 모델 사이의 양방향 데이터 바인딩을 지원
- UI를 별도의 코드 수정없이 재사용 가능
- 쉬운 단위 테스팅

###### example

MVVM 패턴을 가진 대표적인 프레임워크로 **Vue.js(뷰)**가 있다.

<br />

<br />
<hr />
<br />

## 02. 프로그래밍 패러다임

프로그래밍 패러다임은 프로그래머에게 프로그래밍의 관점을 갖게 해주는 역할을 하는 개발 방법론

<p align="center">
<img width="70%" src="https://github.com/inside-coding/cs-note/assets/134191817/792371f8-fb54-46c5-9a29-7e8a0b4ea669">
</p>

자바스크립트는 단순하고 유연한 언어이며 함수가 일급 객체이므로 객체지향 프로그래밍보다는 함수형 프로그래밍 방식이 선호됨

<br />

### 선언형과 함수형 프로그래밍

#### 선언형 (declarative)

'무엇을' 풀어내는가에 집중한 패러다임 <br />
"프로그램은 함수로 이뤄진 것이다." 라는 명제가 담긴 패러다임 <br />

#### 함수형 (functional)

선언형 패러다임의 일종 <br />
순수 함수들을 쌓아 로직을 구현 → '고차 함수'를 통해 재사용성을 높인 패러다임 <br />

##### 특징

- 커링(Currying)
- 불변성(Unmodifiable)
- ...

<br />

### 객체지향 프로그래밍 (OOP)

###### Object-Oriented Programming

객체들의 집합으로 프로그램이 상호 작용을 표현 <br />
데이터를 객체로 취급해 객체 내부에 선언된 메서드를 활용하는 방식 <br />

##### 특징

- 추상화 (abstraction)

  복잡한 시스템으로부터 핵심적인 개념 또는 기능을 간추린 것을 의미

- 캡슐화 (encapsulation)

  객체의 속성과 메서드를 하나로 묶고 일부를 은닉시키는 것을 의미

- 상속성 (inheritance)

  상위 클래스를 하위 클래스가 상속받아 재사용/추가/확장 하는 것 <br />
  코드의 재사용 측면, 계층적인 관계 생성, 유지보수측에서 중요

- 다형성 (polymorphism)

  하나의 메서드나 클래스가 다양한 방법으로 동작하는 것 <br />
  대표적으로 오버로딩과 오버라이딩

  오버로딩 (overloading) <br />
  같은 이름을 가진 메서드를 여러 개 두는 것 <br />
  타입, 매개변수 유형이나 개수 등으로 차이를 두지만 동일한 이름 <br />
  👉 '정적 다형성'

  오버라이딩(overriding) <br />
  주로 메서드 오버라이딩을 말하며
  상위 클래스로부터 상속받은 메서드를 하위 클래스가 재정의하는 것을 의미 <br />
  👉 '동적 다형성'

##### 🔴 CONS

- 설계에 많은 시간이 소요
- 처리 속도가 다른 프로그래밍 패러다임에 비해 상대적으로 느림

<br />

### SOLID

###### 설계 원칙(SOLID원칙)

객체지향 프로그래밍을 설계할 때 지켜야 하는 원칙 <br />

<p align="center">
<img width="70%" src="https://github.com/inside-coding/cs-note/assets/134191817/91354061-bb37-43d2-a2b4-bcb8c69e0bf4">
</p>

#### S

###### SRP(Single Responsibility Principle) : 단일 책임 원칙

모든 클래스는 하나의 책임만 가져야 한다.

#### O

###### OCP(Open Closed Principle) : 개방-폐쇄 원칙

기존 코드는 잘 변경하지 않으면서도 확장은 쉽게 할 수 있어야 한다.

#### L

###### LSP(Liskov Substitution Principle) : 리스코프 치환 원칙

프로그램의 객체는 프로그램의 정확성을 깨뜨리지 않으면서 하위 타입의 인스턴스로 바꿀 수 있어야 한다. <br />
상속 관계에서 부모와 자식의 위치를 바꾸어도 시스템이 문제없이 돌아가야 한다.

#### I

###### ISP(Interface Segregation Principle) : 인터페이스 분리 원칙

하나의 일반적인 인터페이스보다 구체적인 여러 개의 인터페이스를 만들어야 한다.

#### D

###### DIP(Dependency Inversion Principle) : 의존 역전 원칙

자신보다 변하기 쉬운 것에 의존하던 것을 추상화된 인터페이스나 상위 클래스를 두어 변하기 쉬운 것의 변화에 영향 받지 않게 하는 원칙. <br />
즉, 상위 계층은 하위 계층의 변화에 대한 구현으로부터 독립해야 한다.

<br />

### 절차형 프로그래밍

로직이 수행되어야 할 연속적인 계산 과정으로 이루어져 있다. <br />
계산이 많은 작업에 주로 사용됨. <br />
ex) 포트란(fortran)을 이용한 대기 과학 관련 연산 작업, 머신 러닝의 배치 작업 등

##### 🟢 PROS

코드를 구현하기만 하면 되서 코드의 가독성이 좋으며 실행 속도가 빠르다.

##### 🔴 CONS

모듈화하기가 어렵고 유지보수성이 떨어진다.

<br />

### 패러다임의 혼합

어떠한 패러다임이 가장 좋다는 정답은 ❌ <br />
비즈니스 로직이나 서비스의 특징을 고려해서 적재적소에 맞는 패러다임을 정하는 것이 좋다.

하나의 패러다임을 기반으로 통일하여 서비스를 구축하는 것도 좋은 생각이지만 여러 패러다임을 조합하여 상황과 맥락에 따라 패러다임 간의 장점만 취해 개발하는 것이 좋다.

<br />
