> CHAPTER 1 디자인 패턴과 프로그래밍 패러다임
>

>SECTION 1

###### 라이브러리와 프레임워크는 공통으로 사용될 수 있는 특정한 기능들을 모듈화한 것이다

###### 라이브러리(폴더명, 파일명 규칙X, 내가 직접 컨트롤) vs 프레임워크(폴더명, 파일명 규칙O, 엄격, 나는 도구로써 사용함)

  
# 1.1 디자인 패턴
> 디자인 패턴이란 프로그램을 설계할 때 발생했던 문제점들을 객체 간의 상호 관계 등을 이용해 해결할 수 있도록 하나의 '규약' 형태로 만들어 놓은 것


## 1.1.1 싱글톤 패턴
> 하나의 클래스에 오직 하나의 인스턴스만!


![image](https://github.com/inside-coding/cs-note/assets/134191815/21032b38-0df1-45dd-8c2c-58238c7064f0)


### 자바스크립트의 싱글톤 패턴

자바스크립트에서 리터럴{} 또는 new Object로 객체를 생성하면 다른 어떤 객체와도 같지 않기 때문에

이 자체만으로도 싱글톤 패턴을 구현할 수 있다

```jsx
const obj = {
  a: 27
}


const obj2 = {
  a: 27
}

console.log(obj === obj2)
//false
```


보통의 싱글톤 패턴 구성 예시

```jsx
class Singleton {
  constructor() {
    if (!Singleton.instance) {
      Singleton.instance = this
    }
    return Singleton.instance
  }
  getInstance() {
    return this
  }
}


const a = new Singleton()
const b = new Singleton()
console.log(a === b) //true
```

Singleton.instance라는 하나의 인스턴스를 가지는 Singleton 클래스를 구현한 모습

a와 b는 하나의 인스턴스를 가진다.


#### 싱글톤 패턴은 '데이터베이스 연결 모듈'에 많이 쓰인다

```jsx
const URL = 'mongodb://localhost:27017/kundolapp';
const createConnection = url => ({"url": url});

class DB {
  constructor(url) {
    if (!DB.instance) {
      DB.instance = createConnection(url);
    }
    return DB.instance;
  }
  connect() {
    return this.instance
  }
}

const a = new DB(URL);
const b = new DB(URL);
console.log(a === b);
// true
```

이를 통해 데이터베이스 연결에 관한 인스턴스 생성 비용 아낄 수 있다.


### 싱글톤 패턴의 단점

싱글톤 패턴은 TDD(Tesst Driven Development)를 할 때 걸림돌이 된다 </br>
TDD를 할 때 단위 테스트를 주로 하는데, 단위 테스트는 서로 독립적이어야 하며 어떤 순서로든 실행이 가능해야한다.

하지만 싱글톤 패턴은 미리 생성된 하나의 인스턴스를 기방느로 구현하는 패턴이므로, </br>
각 테스트마다 '독립적인' 인스턴스를 만들기가 어렵다.


##### 싱글톤 패턴은 모듈간의 결합을 강하게 만들 수 있다는 단점이 있다
##### 의존성 주입(DI, Dependency Injection)을 통해 모듈 간 결합 더 느슨하게 만들어 해결!


### 의존성 주입

의존성이란 종속성이라고도 하며 A가 B 에 의존성이 있다. === B의 변경사항에 대해 A또한 변해야 된다는 것을 의미

![image](https://github.com/inside-coding/cs-note/assets/134191815/55b730c7-86b1-4c57-a162-db84b35472d0)


직접 다른 하위 모듈에 의존성을 주기보다 중간에 의존성 주입자가 이 부분을 가로채 메인 모듈이 '간접'적으로  의존성을 주입하는 방식

#### 이를 통해 메인 은 하위 모듈에 대한 의존성이 떨어지게 됨 === '디커플링'


### 의존성 주입의 장점

- 모듈을 쉽게 교체할 수 있는 구조가 되어 테스팅에 용이
- 마이그레이션 하기 수월
- 추상화 레이어를 넣고 이를 기반으로 구현체를 넣어주게 되어 의존성 방향 일관
- 애플리케이션 쉽게 추론
- 모듈 간 관계들 조금 더 명확해짐



### 의존성 주입의 단점

- 모듈이 더욱 더 분리되어 클래스 수가 늘어나 복잡성 증대
- 약간의 런타임 패널티 가능성

### 의존성 주입 원칙

- 상위 모듈은 하위 모듈에서 어떠한 것도 가져오지 않아야한다!
- 둘다 추상화에 의존해야하며, 추상화는 세부 사항에 의존하지 말아야 한다!


## 1.1.2 팩토리 패턴
> 객체를 사용하는 코드에서 객체 생성 부분을 떼어내 추상화</br>
>상위 클래스가 중요한 뼈대 결정, 하위 클래스에서 개개체 생성에 관한 구체적인 내용 결정


상위 클래스와 하위 클래스가 분리 되기 때문에 '느슨한 결합'을 가짐
>상위클래스: 인스턴스 생성방식 몰라도됨 -> 유연성 증가 </br>
>객체 생성 로직 따로 떼어져 있어 코드 리팩터링 시 유지보수성 증가


### 자바스크립트의 팩토리 패턴

```jsx
const num = new Object(42)
const str = new Object('abc')

num.constructor.name; //Number
str.consstructor.name; //String
```

어떤 것을 전달하냐에 따라 다른 타입의 객체 생성

![image](https://github.com/inside-coding/cs-note/assets/134191815/23a0fef1-3049-4b2e-acd1-e764a2cf3f32)


```jsx
class Latte{
	constructor(){
		this.name = "latte"
	}
}

class Espresso{
	constructor(){
		this.name = "Espresso"
	}
}

class LatteFactory{
	static createCoffee(){
		return new Latte()
	}
}

class EspressoFactory{
	static createCoffee(){
		return new Espresso()
	}
}

const factoryList = {LatteFactory,EspressoFactory}

class CoffeeFactory{
	static createCoffee(type){
		const factory = factoryList[type]
		return factory.createCoffee()
	}
}

const main = () => {
	// 라떼 커피를 주문함
	const coffee = CoffeeFactory.createCoffee("LatteFactory")
	// 커피 이름을 부름
	console.log(coffee.name) // latte
}
```

- CoffeeFactory : 중요한 뼈대 결정
- LatteFactory  : 구체적인 내용 결정



###### Enum: 상수의 집합을 정의할 때 사용되는 타입(ex. 월, 일, 색상 등)


## 1.1.3 전략 패턴
> 정책 패턴이라고도 하며, 객체의 행위를 바꾸고 싶은 경우 '직접' 수정하지 않고 전략이라고 부르는 </br>
> '캡슐화한 알고리즘'을 컨텍스트 안에서 바꿔주며 상호 교체가 가능하게 만드는 패턴


![image](https://github.com/inside-coding/cs-note/assets/134191815/36201294-6df3-455b-9b3d-e60fd55665b9)


###### 컨텍스트: 상황, 맥락, 문맥을 의미. 개발자가 어떤 작업을 완료하는 데 필요한 모든 관련 정보

매서드에 '전략'을 매개변수로 넣어서 로직 수행




## 1.1.4 옵저버 패턴
> 주체가 어떤 객체의 상태 변화를 관찰하다가 상태 변화가 있을 때마다 메서드 등을 통해 옵저버들에게 변화 알려주는 패턴
>

![image](https://github.com/inside-coding/cs-note/assets/134191815/eb8fdcd1-75da-4a06-9ffc-7399b5474bd5)



- 주체: 객체의 상태 변화를 보고 있는 관찰자
- 옵저버들: 객체의 상태 변화에 따라 전달되는 메서드 등을 기반으로 '추가 변화 사항'이 생기는 객체들을 의미



트위터의 옵저버 패턴

![image](https://github.com/inside-coding/cs-note/assets/134191815/fce83152-199b-4761-8089-f6d2c1f7e5f3)


어떤 사람의 주체를 '팔로우' 시 주체가 포스팅 올리면 알림 '팔로워'에게!


옵저버 패턴은 주로 이벤트 기반 시스템에 사용하며 **MVC(Model-View-Controller)패턴**에도 사용됨</br>
주체인 모델에서 변경사항 생겨  update() 메서드로 옵저버인 뷰에 알려주고 이를 기반으로 컨트롤러 작동




### 자바: 상속과 구현


##### 자바

상속은 자식 클래스가 부모 클래스의 메서드 등을 상속받아 사용하며 자식 클래스에서 추가 및 확장을 할 수 있는 것을 말함

이로 인해 재사용성, 중복성의 최소화가 이뤄짐

##### 구현

구현은 부모 인터페이스를 자식 클래스에서 재정의하여 구현하는 것을 말하며,

상속과는 달리 반드시 부모 클래스의 메서드를 재정의하여 구현해야 함


##### 상속과 구현의 차이

상속은 일반 클래스, abstract 클래스를 기반으로 구현, 구현은 인터페이스를 기반으로 구현



### 자바스크립트에서의 옵저버 패턴

##### 프록시 객체

프록시 객체는 어떠한 대상의 기본적인 동작(속성 접근, 할당, 순회, 열거, 함수 호출 등)의 작업을 가로챌 수 있는 객체

매개변수
- target: 프록시할 대상
- handler: target 동작을 가로채고 어떠한 동작을 할 것인지가 설정되어 있는 함수



```jsx
const handler = {
  get: function(target, name) {
    return name === 'name' ? `${target.a} ${targget.b}` : target[name]
  }
}

// handler: target동작 가로채고 어떤 동작할거지
const p = new Proxy({a: 'Kimi', b: 'is best'}, handler)
console.log(p.name) //Kimi is best
```

특정 속성 접근 시 그 부분을 가로채서 어떠한 로직을 강제할 수 있는 것

- get(): 속성과 함수에 대한 접근을 가로챔
- has(): in 연산자의 사용을 가로챔
- set(): 속성에 대한 접근을 가로챔


###### DOM(Document Object Model): 문서 객체 모델을 말하며, 웹 브라우저상의 화면을 이루고 있는 요소 지칭




### 프록시 패턴

대상 객체에 접근하기 전 그 접근에 대한 흐름을 가로채 해당 접근을 필터링하거나 수정하는 등 역할


객체의 속성, 변환등을 보완하며 보안, 데이터 검증, 캐싱, 로깅에 사용 </br>
이는 프록시 서버로도 활용

```
- 프록시 서버에서의 캐싱 -

캐시안에 정보를 담아두고, 캐시 안에 있는 정보를 요구하는 요청에 대해
다시 저 멀리있는 원격 서버에 요청하지 않고 캐시 안의 데이터 활용하는 것을 말함.

이를 통해 불필요하게 외부와 연결하지 않기에 트래픽을 줄일 수 있다는 장점이 있음
```


### 프록시 서버

서버와 클라이언트 사이에서 클라이언트가 자신을 통해 다른 네트워크 서비스에 간접적으로 접근할 수 있게 해주는 컴퓨터 시스템이나 응용프로그램



###### 버퍼: 데이터가 저장되는 메모리 공간
###### 버퍼 오버플로우: 메모리 공간을 벗어나는 경우. 사용되지 않아야 할 영역에 데이터가 덮어씌워져 주소, 값을 바꾸는 공격이 발생함

###### CDN(Content Delivery Network): 인터넷에 접속하는 곳과 가까운 곳에서 콘텐츠를 캐싱 또는 배포하는 서버네트워크. 이를 통해 웹 서버로부터 다운로드 하는 시간 줄임



### CORS와 프론트엔드의 프록시 서버

**CORS(Cross-Origin Resource Sharing)** 는 서버가 웹 브라우저에서 리소스를 로드 시 다른 오리진을 통해 로드하지 못하게 하는 HTTP 헤더 기반 메커니즘

해결: 프록시 서버를 만들기


###### 오리진: 프로토콜과 호스트이름, 포트의 조합 (ex. https://kimi.com:12101/test에서 오리진은 https://kimi.com:12101이다.)


## 1.1.6 이터레이터 패턴

> 이터레이터를 사용하여 컬렉션의 요소들에 접근하는 패턴</br>
> 순회할 수 있는 여러가지 자료형의 구조와 상관없이 이터레이터 한나의 인터페이스로 순회가 가능
>


```jsx
const mp = new Map()
mp.set('a', 1)
mp.set('b', 2)
mp.set('c', 3)
const st = new Set()
st.add(1)
st.add(2)
st.add(3)
for (let a of mp) console.log(a)
for (let a of st) console.log(a)
/**
 * ['a', 1]
 * ['b', 2]
 * ['c', 3]
 * 1
 * 2
 * 3
 */
```

다른 자료구조인 set과 map임에도 불구하고, 똑같은 for a of b 라는 이터레이터 프로토콜을 통해 순회

###### 이터레이터 프로토콜: 이터러블한 객체들을 순회할 때 쓰이는 규칙

###### 이터러블한 객체: 반복 가능한 객체로 배열을 일반화


## 1.1.7 노출 모듈 패턴

- public: 클래스에 정의된 함수에서 접근 가능하며, 자식 클랫와 외부 클래스에서 접근 가능한 범위
- protected: 클래스에 정의된 함수에서 접근 가능, 자식 클래스에서 접근 가능하지만 외부클래스에서 접근 불가능한 범위
- private: 클래스에 정의된 함수에서 접근 가능하지만, 자식과 외부 클래스에서 접근 불가능
- 즉시 실행 함수: 함수 정의시 바로 호출, 초기화 코드, 라이브러리 내 전역 변수의 충돌 방지 등에 사용


## 1.1.8 MVC 패턴

> 모델, 뷰, 컨트롤러 로 이루어짐

애플리케이션의 구성요소를 세 가지 역할로 구분하여 집중 개발

재사용성과 확장성이 용이, 애플리케이션이 복잡해질수록 모델과 뷰의 관계가 복잡해진다는 단점


### 모델

애플리케이션의 데이터인 데이터베이스, 상수, 변수


### 뷰

inputbox, checkbox, textarea 등 사용자 인텉페이스 요소를 나타냄

즉, 모델을 기반으로 사용자가 볼 수 있는 화면을 뜻함

변경이 일어나면 컨트롤러에 이를 전달

### 컨트롤러

하나 이상의 모델과 하나 이상의 뷰를 잇는 다리 역할, 이벤트 등 메인 로직 담당

모델과 뷰의 생명주기도 관리, 변경 통지 받을 시 해석하여 각각 구성 요소에 해당 내용에 대해 알림


###### 커맨드: 여러가지 요소에 대해 하나의 액션으로 처리할 수 있게 하는 기법
###### 데이터 바인딩: 화면에 보이는 데이터와 웹 브라우저의 메모리 데이터를 일치시키는 기법, 뷰모델 변경시 뷰가 변경됨








