## 📖 Overview

우리가 흔히 프로그래밍할 때 사용하는 **React.js, Vue.js, Spring** 등 라이브러리나 프레임워크의 기본이 되는 디자인 패턴에 대해 알아보자

## 📖 디자인 패턴이란?

예로부터 건물을 지을 때는 사전 설계가 중요했습니다. 건물을 설계하는 과정에서 문제가 발생하거나 수정 사항이 발생했을 때, 처음부터 하나씩 다시 짓기에는 수많은 시간과 비용이 들어가죠.

이처럼 사람들은 같은 실수를 반복하지 않기 위해 자신의 시행착오를 바탕으로 특정 상황에서 발생하는 문제 패턴을 발견하고 해결방안을 기록으로 남겼습니다. 그리고 우리는 이것을 **디자인 패턴**이라 부릅니다.

![](https://velog.velcdn.com/images/psik_2/post/da15cc33-6bf2-4c58-95bd-60eb356c3192/image.jpg)

즉 디자인 패턴을 통해 우리는 **어떠한 문제 상황에서는 "OOO 패턴이 좋다"**라는 사실을 알 수 있습니다. 이는 수많은 전문가들의 경험을 통해 얻게된 산물이라는 거죠😁

### 그렇다면 소프트웨어에서 디자인 패턴은 무엇을 의미할까❓

> **디자인 패턴(Design Pattern)**은 프로그램을 설계할 때 발생했던 문제점을 객체 간의 상호 관계 등을 이용하여 해결할 수 있도록 하나의 **규약** 형태로 만들어 놓은것을 의미합니다.

다시말해 디자인 패턴은 소프트웨어 디자인 과정에서 자주 발생하는 문제들에 대한 **해결 방법**이라고 생각하면 됩니다.

### 그래서 디자인 패턴은 왜 써야 하는건데❓

디자인 패턴을 사용하면 코드의 **재사용성**을 향상시키고 코드를 쉽게 모듈화하여 변경이 필요하면 해당 모듈만 수정하여 **유지보수**가 쉬워집니다.

또한 패턴을 사용하여 소통하면 일상어로 소통할 때보다 효율적으로 **의사소통**을
할 수 있습니다.

> _**"오리들의 다양한 행동을 전략패턴으로 구현하고 있습니다💬"**_

우리가 디자인 패턴을 잘 알고 있다면 **오리들의 행동이 쉽게 확장하거나 변경할 수 있는 클래스들의 집합으로 캡슐화되어 있다** 라는 것을 알 수 있습니다.

## 📖 다양한 디자인 패턴

### [1] 싱글톤 패턴

> **싱글톤 패턴(singleton pattern)**은 하나에 클래스에 오직 하나의 인스턴스만 가지는 패턴입니다.

아래 코드는 싱글톤 패턴을 구현한 간단한 예제입니다.

```javascript
class Singleton {
  constructor() {
    if (!Singleton.instance) {
      Singleton.instance = this;
    }
    return Singleton.instance;
  }

  getInstance() {
    return this;
  }
}

const a = new Singleton();
const b = new Singleton();
console.log(a === b); // true
```

코드의 출력 결과를 보면 **true**가 나오는 것을 알 수 있습니다.
즉 Singleton 클래스는 Singleton.instance 라는 하나의 인스턴스를 가진 싱글톤 패턴인 것을 알 수 있습니다. 이를 통해 a와 b는 하나의 인스턴스를 가집니다.

이렇게 하나의 인스턴스를 만들어 놓고 해당 인스턴스를 다른 모듈들이 공유하여 사용하면 인스턴스를 생성할 때 드는 비용이 줄어드는 장점이 있습니다.

하지만 이렇게 코드를 작성하게 되면 **의존성**이 높아진다는 단점이 있습니다.
~~이 문제는 의존성 주입에서 알아보도록 하자~~

### [2] 팩토리 패턴

> **팩토리 패턴(factory pattern)**은 객체를 사용하는 코드에서 객체 생성 부분을 떼어내어 추상화한 패턴이자 상속 관계에 있는 두 클래스에서 상위 클래스가 중요한 뼈대를 결정하고, 하위 클래스에서 객체 생성에 관한 구체적인 내용을 결정하는 패턴입니다.

다음 그림은 팩토리 패턴을 바리스타 공장에 비유한 그림입니다.
![](https://velog.velcdn.com/images/psik_2/post/d144299e-5292-41ff-929a-6534dbdce913/image.png)

라떼 레시피와 아메리카노 레시피, 그리고 우유 레시피를 하위 클래스로 정의하고 바리스타 공장을 상위 클래스로 정의해보자.
위 사진을 보면 상위 클래스인 바리스타 공장에서는 레시피(하위 클래스)들을 통해 우유를 생산하고 있다.

즉 팩토리 패턴은 상위 클래스인 바리스타 공장에서 중요한 뼈대를 결정하고, 하위 클래스인 레시피에서 제품 생성에 관한 내용을 결정하는 패턴인 것을 알 수 있다.

아래 코드는 커피 생산 공정을 팩토리 패턴으로 구현한 코드입니다.

```javascript
class CoffeeFactory {
  static createCoffee(type) {
    const factory = factoryList[type];
    return factory.createCoffee();
  }
}

class Latte {
  constructor() {
    this.name = "latte";
  }
}
class Espresso {
  constructor() {
    this.name = "Espresso";
  }
}

class LatteFactory extends CoffeeFactory {
  static createCoffee() {
    return new Latte();
  }
}
class EspressoFactory extends CoffeeFactory {
  static createCoffee() {
    return new Espresso();
  }
}
const factoryList = { LatteFactory, EspressoFactory };

const main = () => {
  // 라떼 커피를 주문한다.
  const coffee = CoffeeFactory.createCoffee("LatteFactory");
  // 커피 이름을 부른다.
  console.log(coffee.name); // latte
};
main();
```

CoffeeFactory 라는 상위 클래스가 커피 공정에 있어 중요한 뼈대를 결정하고 하위 클래스인 LatteFactory, EspressoFactory가 구체적인 내용을 결정하고 있습니다.

즉 상위 클래스와 하위 클래스가 분리되기 때문에 느슨한 결합을 가지며 상위 클래스에서는 인스턴스 생성 방식에 대해 전혀 알 필요가 없기 때문에 더 많은 유연성을 갖게 되는 장점이 있습니다.

또한 객체 생성 로직이 분리되어 있어 코드를 리팩터링 하더라도 한 곳만 고칠 수 있으니 유지 보수성이 증가합니다.

### [3] 전략 패턴

> **전략 패턴(strategy pattern)**은 객체의 행위를 바꾸고 싶은 경우 '직접' 수정하지 않고 전략이라고 부르는 '캡슐화한 알고리즘'을 컨텍스트 안에서 바꿔주면서 상호 교체가 가능하게 만드는 패턴입니다.

간단하게 말해 전략 패턴은 런타임중에 알고리즘 전략을 선택하여 객체의 동작을 실시간으로 바뀌게 할 수 있는 디자인 패턴입니다.

다음 코드는 전략 패턴을 이용하여 작성한 코드입니다.

```java script
// 전략 인터페이스
class Strategy {
  execute() {}
}

// 각 전략 클래스
class ConcreteStrategy1 extends Strategy {
  execute() {
    return "Executing strategy 1";
  }
}

class ConcreteStrategy2 extends Strategy {
  execute() {
    return "Executing strategy 2";
  }
}

// Context 클래스
class Context {
  constructor(strategy) {
    this.strategy = strategy;
  }

  setStrategy(strategy) {
    this.strategy = strategy;
  }

  executeStrategy() {
    return this.strategy.execute();
  }
}

const context = new Context(new ConcreteStrategy1());
console.log(context.executeStrategy()); // Executing strategy 1

context.setStrategy(new ConcreteStrategy2());
console.log(context.executeStrategy()); // Executing strategy 2

```

### [4] 옵저버 패턴

> **옵저버 패턴(observer pattern)**은 주체가 어떤 객체(subject)의 상태 변화를 관찰하다가 상태 변화가 있을 때마다 메서드 등을 통해 옵저버 목록에 있는 옵저버들에게 변화를 알려주는 디자인 패턴입니다.

여기서 **주체란 객체의 상태 변화를 보고 있는 관찰자**이며, **옵저버란 이 객체의 상태 변화에 따라 전달되는 메서드 등을 기반으로 변화가 생기는 객체**들을 의미합니다.

우리 주변에 옵저버 패턴을 활용한 대표적인 서비스로는 트위터가 있습니다.

![](https://velog.velcdn.com/images/psik_2/post/b6c6befc-edd5-4725-80a8-81cc09f479f6/image.jpg)

트위터를 사용하는 사람들이 특정 연예인(주체)을 팔로우했다면 해당 연예인(주체)가 포스팅을 올리게 되면 알람이 팔로워(옵저버)에게 전달됩니다.
유튜브도 마찬가지로 우리가 유튜버를 구독했을때 해당 유튜버가 동영상을 업로드 하면 구독자들에게 알람이 전달됩니다.

옵저버 패턴은 주로 이벤트 기반 시스템에 사용하며 MVC(Model-View-Controller) 패턴에도 사용됩니다.

### [5] 프록시 패턴

> **프록시 패턴(proxy pattern)**은 대상 객체(subject)에 접근하기 전 그 접근에 대한 흐름을 가로채 해당 접근을 필터링하거나 수정하는 등의 역할을 하는 계층이 있는 디자인 패턴입니다.

프록시 패턴의 구조는 아래와 같다.

Subject는 Proxy와 RealSubject를 하나로 묶는 인터페이스를 의미, RealSubject와 Proxy와 는 각각 원본 대상 객체와 대상 객체(RealSubject)를 중계할 대리자이다.

![](https://velog.velcdn.com/images/psik_2/post/c0c8e0d9-d986-4a3c-9860-98b1dc54362a/image.png)

프록시(Proxy)의 사전적인 의미는 '대리인'이다. 즉 프록시 패턴은 대상 객체를 대리하여 처리하게 함으로써 로직의 흐름을 제어하는 디자인 패턴이다.

_**그렇다면 왜 대리자를 이용해서 객체를 처리하는걸까?
**_

만약 대상 클래스가 민감한 정보를 가지고 있거나 인스턴스화 하기에 무거운 경우 혹은 기능을 추가하고 싶은데, **원본 객체를 수정할 수 없는 상황일 때**를 극복하기 위해 사용된다.

대체적으로 프록시 패턴은 객체의 속성, 변환 등을 보완하며 **보안, 데이터 검증, 캐싱, 로깅**에 사용된다.

다음은 기본적인 프록시 패턴을 구현한 코드이다.

```javascript
// 실제 대상 객체
class RealSubject {
  fetchData() {
    console.log("데이터를 가져옵니다.");
  }
}

// 프록시 객체
class ProxySubject {
  constructor(realService) {
    this.realService = realService;
  }

  fetchData() {
    console.log("접근을 확인합니다.");
    this.realService.fetchData();
  }
}

const realService = new RealSubject();
const proxyService = new ProxySubject(realService);

proxyService.fetchData();
/*
  접근을 확인합니다.
  데이터를 가져옵니다.
*/
```

### [6] 이터레이터 패턴

> **이터레이터 패턴(iterator pattern)**은 이터레이터(iterator)을 사용하여 컬렉션(collection)의 요소들에 접근하는 디자인 패턴입니다.

아래 코드는 이터레이터 패턴을 구현한 코드이다.

```javascript
const map = new Map();
map.set("a", 1);
map.set("b", 2);
map.set("c", 3);
const set = new Set();
set.add(1);
set.add(2);
set.add(3);

for (let result of map) console.log(result);
/*
  [ 'a', 1 ]
  [ 'b', 2 ]
  [ 'c', 3 ]
*/
for (let result of set) console.log(result);
/* 
  1
  2
  3
*/
```

map과 set은 서로 다른 자료 구조이지만 for ... of 라는 동일한 이터레이터 프로토콜을 통해 순회하는 것을 알 수 있습니다.

### [7] 노출모듈 패턴

> **노출모듈 패턴(revealing module pattern)**은 즉시 실행 함수를 통해 private, public 같은 접근 제어자를 만드는 패턴을 말합니다.

아래 코드는 즉시 실행 함수를 사용하여 구현한 노출모듈 패턴입니다.

```javascript
const revealingModule = (() => {
  const a = 1;
  const b = () => 2;
  const public = {
    c: 2,
    d: () => 3,
  };
  return public;
})();

console.log(revealingModule); // { c: 2, d: [Function: d] }
console.log(revealingModule.a); // undefined
```

a와 b는 다른 모듈에서 사용할 수 없는 변수나 함수이며 private한 범위를 가지게 됩니다. 하지만 c와 d는 다른 모듈에서 사용할 수 있는 변수 및 함수이며 public한 범위를 가집니다.

자바스크립트는 private, public와 같은 접근 제어자가 존재하지 않고 전역 범위에서 스크립트가 실행됩니다. 따라서 위와 같이 노출모듈 패턴을 통해 private 및 public 접근 제어자를 구현하기도 합니다.

### [8] MVC 패턴

> **MVC 패턴**은 모델(Model), 뷰(View), 컨트롤러(Controller)로 이루어진 디자인 패턴입니다.

MVC 패턴과 같이 애플리케이션의 구성 요소를 세 가지 역할로 구분하여 개발 프로세스에서 각각의 구성 요소에만 집중하여 개발할 수 있습니다.

_**그렇다면 모델(Model), 뷰(View), 컨트롤러(Controller)는 무엇일까?
**_

> **모델**
> 모델(model)은 애플리케이션의 데이터인 데이터베이스, 상수, 변수 등을 뜻합니다.

예를 들어 사각형 모양의 박스 안에 글자가 들어 있다면 그 사각형 모양의 박스 위치 정보, 글자 내용, 글자 위치, 글자 포맷(utf-8 등)에 관한 모든 정보를 가지고 있어야 합니다.
뷰에서 데이터를 생성하거나 수정하면 컨트롤러를 통해 모델을 생성하거나 갱신합니다.

> **뷰**
> 뷰(view)는 inputbox, checkbox, textarea 등 사용자 인터페이스 요소를 나타냅니다.

즉 모델을 기반으로 사용자가 볼 수 있는 화면을 뜻합니다. 모델이 가지고 있는 정보를 따로 저장하지 않아야 하며 단순히 사각형 모양 등 화면에 표시하는 정보만 가지고 있어야 합니다.
또한 변경이 일어나면 컨트롤러에 이를 전달해야 합니다.

> **컨트롤러**
> 컨트롤러(controller)는 하나 이상의 모델과 하나 이상의 뷰를 잇는 다리 역할을 하며 이벤트 등 메인 로직을 담당합니다.

또한, 모델과 뷰의 생명주기를 관리하며, 모델이나 뷰의 변경 통지를 받으면 이를 해석하여 각각의 구성 요소에 해당 내용에 대해 알려줍니다.

_**그렇다면 웹에서 MVC 패턴은 어떤 방식으로 동작할까?**_

![](https://velog.velcdn.com/images/psik_2/post/b5a47a8a-43bc-4517-add7-bc6b7a79a953/image.png)

**사용자가 웹사이트에 접속해서 검색하는 상황을 가정해보자❗**

> ***컨트롤러(Controller)***는 검색 결과에 대한 데이터를 받기 위해 ***모델(Model)***을 호출한다.
>
> **_모델(Model)_**은 데이터베이스 파일과 같은 데이터 소스를 제어한 후 결과를 리턴한다.
>
> ***컨트롤러(Controller)***는 ***모델(Model)***이 리턴한 결과를 ***뷰(View)***에 반영한다.
>
> 데이터가 반영된 ***뷰(View)***는 사용자에게 보여진다.

MVC 패턴은 가장 **보편적으로 사용되는 디자인 패턴**이지만 모델(Model)과 뷰(View) 사이에 의존성이 높아 **애플리케이션이 커질수록 유지보수가 어려워진다는 단점**이 있습니다.

### [9] MVP 패턴

> **MVP 패턴**은 MVC 패턴으로부터 파생되었으며 MVC에서 C에 해당하는 컨트롤러가 프레젠터(presenter)로 교체된 패턴입니다.

_**MVP 패턴**_ 의 핵심 설계는 MVC와 다르게 뷰(View)와 모델(Model) 로직을 분리하고 서로 간에 상호작용을 _**프레젠터(Presenter)**_ 에 줌으로써, 서로의 영향 즉 _**의존성**_ 을 최소화 하는 것에 있습니다.

_**MVP 패턴**_ 에서 모델(Model)과 뷰(View)는 MVC 패턴과 동일한 역할을 한다.

그렇다면 _**프레젠터(Presenter)**_ 는 무엇일까?

> **프레젠터**
> 프레젠터(Presenter)는 모델(Model)과 뷰(View) 사이의 매개체로 컨트롤러(Controller)와 유사하지만, 뷰(View)에 직접 연결되는 대신 인터페이스를 통해 상호작용 하는 차이가 있습니다.

_**그렇다면 MVP 패턴은 어떤 방법으로 동작할까?**_

![](https://velog.velcdn.com/images/psik_2/post/93d94a83-cfa1-48af-b71c-e9d61c5b9f3f/image.png)

> 사용자의 액션(Action)은 ***뷰(View)***를 통해 들어오게 된다.
>
> ***뷰(View)***는 데이터를 _**프레젠터(Presenter)에**_ 요청한다.
>
> **프레젠터(Presenter)**는 데이터를 ***모델(Model)***에 요청한다.
>
> ***모델(Model)***은 ***프레젠터(Presenter)***에게 요청받은 데이터를 응답한다.
>
> ***프레젠터(Presenter)***은 데이터를 가공하고 다시 ***뷰(View)***에 응답한다.
>
> ***뷰(View)***는 ***프레젠터(Presenter)***로부터 응답받은 데이터를 이용해 UI를 갱신한다.

MVP 패턴은 **인터페이스를 통해 통신하기 때문에 모델(Model)과 뷰(View)의 의존성이 낮지만** 반대로 **애플리케이션이 복잡해질수록 뷰(View)와 프레젠터(Presenter) 사이의 의존성이 강해지는 문제**가 있습니다.

### [10] MVVM 패턴

> **MVVM 패턴**은 MVC의 C에 해당하는 컨트롤러가 뷰모델(view model)로 바뀐 패턴입니다.

여기서 뷰모델(View Model)은 뷰를 더 추상화한 계층이다.

> **뷰모델**
> 뷰모델(View Model)은 View 상태를 유지 및 변화시키고, 뷰(View)에 대한 작업의 결과로 모델(Model)을 조작하고, 뷰(View)에서 발생되는 이벤트를 트리거하는데 도움이 되는 메서드, 명령, 혹은 다른 속성을 노출하는 역할을 합니다. 즉 뷰(View)를 표현하기 위해 만들어진 뷰(View)를 위한 모델(Model) 입니다.

_**그렇다면 MVVM모델은 어떤 방식으로 동작할까?**_

![](https://velog.velcdn.com/images/psik_2/post/23d0391c-e40f-4cdb-9269-ab637a754d55/image.png)

> 사용자의 액션(Action)은 ***뷰(View)***를 통해 들어오게 된다.
>
> ***뷰(View)***는 액션을 _**뷰모델(View Model)에**_ 요청한다.
>
> **뷰모델(View Model)**은 데이터를 ***모델(Model)***에 요청한다.
>
> ***모델(Model)***은 ***뷰모델(View Model)***에게 요청받은 데이터를 응답한다.
>
> ***뷰모델(View Model)***은 데이터를 가공하고 저장한다.
>
> ***뷰(View)***는 _**뷰모델(View Model)**_ 과의 **데이터 바인딩**으로 인해 자동으로 갱신된다.
>
> _\* 데이터 바인딩(Data Binding)
> 데이터 바인딩의 개념은 쉽게 말해 Model과 UI 요소 간의 싱크를 맞춰주는 것이라 할 수 있습니다.
> 이 패턴을 통해 View와 로직이 분리되어 있어도 한 쪽이 바뀌면 다른 쪽도 업데이트가 이루어져 데이터의 일관성을 유지할 수 있습니다._

MVVM 패턴은 MVP 패턴과 유사한 점이 많이 있습니다. 하지만 MVP 패턴은 뷰(View)와 프레젠터(Presenter)의 의존 관계가 1:1로 형성되어 있고, **MVVM 패턴은 뷰(View)와 뷰모델(View Model)의 관계가 N:1** 입니다. 또한 **데이터 바인딩으로 인해 코드의 양이 줄어들고 뷰(View)와 뷰모델(View Model) 사이의 의존성을 없앨 수 있습니다**.

하지만 **간단한 UI에서 뷰모델(View Model)을 설계하는데 어려움**이 있을 수 있고, **애플리케이션이 복잡해지면 MVC 패턴의 컨트롤러(Controller)처럼 뷰모델(View Model)이 비대**해질수 있습니다.
