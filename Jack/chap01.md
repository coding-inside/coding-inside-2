# 디자인 패턴과 프로그래밍 패러다임

## 1.1 디자인 패턴

- 디자인 패턴 : 프로그램을 설계할 때 발생했던 문제점들을 객체 간의 상호 관계 등을 이용하여 해결할 수 있도록 하나의 '규약' 형태로 만들어 놓은 것

### 1.1.1 싱글톤 패턴

- 싱글톤 패턴 : 하나의 클래스에 오직 하나의 인스턴스만 가지는 패턴. 하나의 클래스를 기반으로 단 하나의 인스턴스를 만들어 이를 기반으로 로직을 만드는데 사용되며, 보통 데이터베이스 연결 모듈에 많이 사용된다.

- 장점 : 인스턴스를 생성 비용이 줄어든다.
- 단점 : 의존성이 높아진다.

#### 자바스크립트의 싱글톤 패턴 - 리터럴 {} 또는 new Object로 객체를 생성하게 되면 다른 어떤 객체와도 같지 않기 때문에 이 자체만으로도 싱글톤 패턴을 구현할 수 있다.

```
const obj = {
    a : 27
}
const obj2 = {
    a : 27
}
console.log(obj === obj2)
// false
```

이것도 어느정도 싱글톤 패턴이라고 할 수 있지만 실제 싱글톤 패턴은 다음과 같이 구성된다.

```
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
console.log(a === b) // true
```

Singleton.instance라는 하나의 인스턴스를 가지는 Singleton 클래스를 구현한 모습이다. 이를 통해 a와 b는 하나의 인스턴스를 가진다.

#### 데이터베이스 연결 모듈

```
const URL = 'mongodb://localhost:27017/kundolapp'
const createConnection = url => ({"url" : url})
class DB {
    constructor(url) {
        if (!DB.instance) {
            DB.instance = createConnection(url)
        }
        return DB.instance
    }
    connect() {
        return this.instance
    }
}
const a = new DB(URL)
const b = new DB(URL)
console.log(a === b) // true
```

DB.instance라는 하나의 인스턴스를 기반으로 a,b를 생성하는 것을 볼 수 있다. 이를 통해 데이터베이스 연결에 관한 인스턴스 생성 비용을 아낄 수 있다.

#### 자바에서의 싱글톤 패턴

자바는 중첩 클래스를 이용해서 만드는 방법이 가장 대중적이다.

```
class Singleton {
    private static class singleInstanceHolder {
        private static final Singleton INSTANCE = new Singleton();
    }
    public static Singleton getInstance() {
        return singleInstanceHolder.INSTANCE;
    }
}

public class HelloWorld{
     public static void main(String []args){
        Singleton a = Singleton.getInstance();
        Singleton b = Singleton.getInstance();
        System.out.println(a.hashCode());
        System.out.println(b.hashCode());
        if (a == b){
         System.out.println(true);
        }
     }
}
/*
705927765
705927765
true

1. 클래스안에 클래스(Holder), static이며 중첩된 클래스인 singleInstanceHolder를
기반으로 객체를 선언했기 때문에 한 번만 로드되므로 싱글톤 클래스의 인스턴스는 애플리케이션 당 하나만 존재하며
클래스가 두 번 로드되지 않기 때문에 두 스레드가 동일한 JVM에서 2개의 인스턴스를 생성할 수 없습니다.
그렇기 때문에 동기화, 즉 synchronized를 신경쓰지 않아도 됩니다.
2. final 키워드를 통해서 read only 즉, 다시 값이 할당되지 않도록 했습니다.
3. 중첩클래스 Holder로 만들었기 때문에 싱글톤 클래스가 로드될 때 클래스가 메모리에 로드되지 않고
어떠한 모듈에서 getInstance()메서드가 호출할 때 싱글톤 객체를 최초로 생성 및 리턴하게 됩니다.
*/
```

#### mongoose의 싱글톤 패턴

실제로 싱글톤 패턴은 Node.js에서 MongoDB 데이터베이스를 연결할 때 쓰는 mongoose 모듈에서 볼 수 있다.

```
Mongoose.prototype.connect = function(uri, options, callback) {
    const _mongoose = this instanceof Mongoose ? this : mongoose;
    const conn = _mongoose.connection;

    return _mongoose._promiseOrCallback(callback, cb => {
        conn.openUri(uri, options, err => {
            if (err != null) {
                return cb(err);
            }
            return cb(null, _mongoose);
        })
    })
}
```

#### MySQL의 싱글톤 패턴

Node.js에서 MySQL 데이터를 연결할 때 사용한다.

```
// 메인 모듈
const mysql = require('mysql');
const pool = mysql.createPool({
    connectionLimit: 10,
    host: 'example.org',
    user: 'kundol',
    password: 'secret',
    database: '승철이디비',
});
pool.connect();

// 모듈 A
pool.query(query, function (error, results, fields) {
    if(error) throw error;
    console.log('The solution is: ', results[0].solution);
});

// 모듈 B
pool.query(query, function (error, results, fields) {
    if(error) throw error;
    console.log('The solution is: ', results[0].solution);
});
```

#### 싱글톤 패턴의 단점

- DDT(Test Driven Development)를 할때 걸림돌이 된다.
- 모듈간의 결합을 강하게 만들수 있기 때문에 의존성 주입을 통해 모듈간의 결합을 조금 더 느슨하게 만들어 해결할 수 있다.

### 팩토리 패턴

- 객체를 사용하는 코드에서 객체 생성 부분을 떼어내 추상화한 패턴이자 상속 관계에 있는 두 클래스에서 상위 클래스가 중요한 뼈대를 결정하고, 하위 클래스에서 객체 생성에 관한 국체적인 내용을 결정하는 패턴

#### 자바스크립트의 팩토리 패턴

커피 팩토리 기반 커피 생성 코드를 구축

```
class CoffeeFactory {
    static createCoffee(type) {
        const factory = factoryList[type]
        return factory.createCoffee()
    }
}
class Latte {
    constructor() {
        this.name = "latte"
    }
}
class Espresso {
    constructor() {
        this.name = "Espresso"
    }
}

class LatteFactory extends CoffeeFactory{
    static createCoffee() {
        return new Latte()
    }
}
class EspressoFactory extends CoffeeFactory{
    static createCoffee() {
        return new Espresso()
    }
}
const factoryList = { LatteFactory, EspressoFactory }


const main = () => {
    // 라떼 커피를 주문한다.
    const coffee = CoffeeFactory.createCoffee("LatteFactory")
    // 커피 이름을 부른다.
    console.log(coffee.name) // latte
}
main()
```

#### 자바의 팩토리 패턴

위의 코드를 자바로 구현

```
enum CoffeeType {
    LATTE,
    ESPRESSO
}

abstract class Coffee {
    protected String name;

    public String getName() {
        return name;
    }
}

class Latte extends Coffee {
    public Latte() {
        name = "latte";
    }
}

class Espresso extends Coffee {
    public Espresso() {
        name = "Espresso";
    }
}

class CoffeeFactory {
    public static Coffee createCoffee(CoffeeType type) {
        switch (type) {
            case LATTE:
                return new Latte();
            case ESPRESSO:
                return new Espresso();
            default:
                throw new IllegalArgumentException("Invalid coffee type: " + type);
        }
    }
}

public class Main {
    public static void main(String[] args) {
        Coffee coffee = CoffeeFactory.createCoffee(CoffeeType.LATTE);
        System.out.println(coffee.getName()); // latte
    }
}
```

### 전략 패턴

- 전략 패턴 = 정책 패턴 : 객체의 행위를 바꾸고 싶은 경우 '직접' 수정하지 않고 전략이라고 부르는 '캡슐화한 알고리즘'을 컨텍스트 안에서 바꿔주면서 상호 교체가 가능하게 만드는 패턴

#### 자바의 전략 패턴

```
import java.text.DecimalFormat;
import java.util.ArrayList;
import java.util.List;
interface PaymentStrategy {
    public void pay(int amount);
}

class KAKAOCardStrategy implements PaymentStrategy {
    private String name;
    private String cardNumber;
    private String cvv;
    private String dateOfExpiry;

    public KAKAOCardStrategy(String nm, String ccNum, String cvv, String expiryDate){
        this.name=nm;
        this.cardNumber=ccNum;
        this.cvv=cvv;
        this.dateOfExpiry=expiryDate;
    }

    @Override
    public void pay(int amount) {
        System.out.println(amount +" paid using KAKAOCard.");
    }
}

class LUNACardStrategy implements PaymentStrategy {
    private String emailId;
    private String password;

    public LUNACardStrategy(String email, String pwd){
        this.emailId=email;
        this.password=pwd;
    }

    @Override
    public void pay(int amount) {
        System.out.println(amount + " paid using LUNACard.");
    }
}

class Item {
    private String name;
    private int price;
    public Item(String name, int cost){
        this.name=name;
        this.price=cost;
    }

    public String getName() {
        return name;
    }

    public int getPrice() {
        return price;
    }
}

class ShoppingCart {
    List<Item> items;

    public ShoppingCart(){
        this.items=new ArrayList<Item>();
    }

    public void addItem(Item item){
        this.items.add(item);
    }

    public void removeItem(Item item){
        this.items.remove(item);
    }

    public int calculateTotal(){
        int sum = 0;
        for(Item item : items){
            sum += item.getPrice();
        }
        return sum;
    }

    public void pay(PaymentStrategy paymentMethod){
        int amount = calculateTotal();
        paymentMethod.pay(amount);
    }
}

public class HelloWorld{
    public static void main(String []args){
        ShoppingCart cart = new ShoppingCart();

        Item A = new Item("kundolA",100);
        Item B = new Item("kundolB",300);

        cart.addItem(A);
        cart.addItem(B);

        // pay by LUNACard
        cart.pay(new LUNACardStrategy("kundol@example.com", "pukubababo"));
        // pay by KAKAOBank
        cart.pay(new KAKAOCardStrategy("Ju hongchul", "123456789", "123", "12/01"));
    }
}
/*
400 paid using LUNACard.
400 paid using KAKAOCard.
*/
```

#### passport의 전략 패턴

- 전략 패턴을 활용한 라이브러리로는 passport로 Node.js에서 인증 모듈을 구현할 때 쓰는 미들웨어 라이브러리로, 여러가지 '전략'을 기반으로 인증할 수 있게 한다.

```
var passport = require('passport')
    , LocalStrategy = require('passport-local').Strategy;

passport.use(new LocalStrategy(
    function(username, password, done) {
        User.findOne({ username: username }, function (err, user) {
          if (err) { return done(err); }
            if (!user) {
                return done(null, false, { message: 'Incorrect username.' });
            }
            if (!user.validPassword(password)) {
                return done(null, false, { message: 'Incorrect password.' });
            }
            return done(null, user);
        });
    }
));
```

### 옵저버 패턴

- 주체가 어떤 객체의 상태 변화를 관찰하다가 상태 변화가 있을 때마다 메서드 등을 통해 옵저버 목록에 있는 옵저버들에게 변화를 알려주는 디자인 패턴

#### 자바에서의 옵저버 패턴

```
import java.util.ArrayList;
import java.util.List;

interface Subject {
    public void register(Observer obj);
    public void unregister(Observer obj);
    public void notifyObservers();
    public Object getUpdate(Observer obj);
}

interface Observer {
    public void update();
}

class Topic implements Subject {
    private List<Observer> observers;
    private String message;

    public Topic() {
        this.observers = new ArrayList<>();
        this.message = "";
    }

    @Override
    public void register(Observer obj) {
        if (!observers.contains(obj)) observers.add(obj);
    }

    @Override
    public void unregister(Observer obj) {
        observers.remove(obj);
    }

    @Override
    public void notifyObservers() {
        this.observers.forEach(Observer::update);
    }

    @Override
    public Object getUpdate(Observer obj) {
        return this.message;
    }

    public void postMessage(String msg) {
        System.out.println("Message sended to Topic: " + msg);
        this.message = msg;
        notifyObservers();
    }
}

class TopicSubscriber implements Observer {
    private String name;
    private Subject topic;

    public TopicSubscriber(String name, Subject topic) {
        this.name = name;
        this.topic = topic;
    }

    @Override
    public void update() {
        String msg = (String) topic.getUpdate(this);
        System.out.println(name + ":: got message >> " + msg);
    }
}

public class HelloWorld {
    public static void main(String[] args) {
        Topic topic = new Topic();
        Observer a = new TopicSubscriber("a", topic);
        Observer b = new TopicSubscriber("b", topic);
        Observer c = new TopicSubscriber("c", topic);
        topic.register(a);
        topic.register(b);
        topic.register(c);

        topic.postMessage("amumu is op champion!!");
    }
}
/*
Message sended to Topic: amumu is op champion!!
a:: got message >> amumu is op champion!!
b:: got message >> amumu is op champion!!
c:: got message >> amumu is op champion!!
*/
```

#### 자바스크립트에서의 옵저버 패턴

- 프록시 객체를 이용한 옵저버 패턴

```
function createReactiveObject(target, callback) {
    const proxy = new Proxy(target, {
        set(obj, prop, value){
            if(value !== obj[prop]){
                const prev = obj[prop]
                obj[prop] = value
                callback(`${prop}가 [${prev}] >> [${value}] 로 변경되었습니다`)
            }
            return true
        }
    })
    return proxy
}
const a = {
    "형규" : "솔로"
}
const b = createReactiveObject(a, console.log)
b.형규 = "솔로"
b.형규 = "커플"
// 형규가 [솔로] >> [커플] 로 변경되었습니다
```

#### Vue.js 3.0의 옵저버 패턴

```
function createReactiveObject(
    target: Target,
    isReadonly: boolean,
    baseHandlers: ProxyHandler < any > ,
    collectionHandlers: ProxyHandler < any > ,
    proxyMap: WeakMap < Target, any >
) {
    if (!isObject(target)) {
        if (__DEV__) {
            console.warn(`value cannot be made reactive: ${String(target)}`)
        }
        return target
    }
    // target is already a Proxy, return it.
    // exception: calling readonly() on a reactive object
    if (
        target[ReactiveFlags.RAW] &&
        !(isReadonly && target[ReactiveFlags.IS_REACTIVE])
    ) {
        return target
    }
    // target already has corresponding Proxy
    const existingProxy = proxyMap.get(target)
    if (existingProxy) {
        return existingProxy
    }
    // only a whitelist of value types can be observed.
    const targetType = getTargetType(target)
    if (targetType === TargetType.INVALID) {
        return target
    }
    const proxy = new Proxy(
        target,
        targetType === TargetType.COLLECTION ? collectionHandlers :
        baseHandlers
    )
    proxyMap.set(target, proxy)
    return proxy
}
```

### 프록시 패턴과 프록시 서버

#### 프록시 패턴

- 대상 객체에 접근하기 전 그 접근에 대한 흐름을 가로채 해당 접근을 필터링하거나 수정하는 등의 역할을 하는 계층이 있는 디자인 패턴

#### 프록시 서버

- 서버와 클라이언트 사이에서 클라이언트가 자신을 통해 다른 네트워크 서비스에 간접적으로 접속할 수 있게 해주는 컴퓨터 시스템이나 응용프로그램을 말한다.

- 프록시 서버로 쓰는 nginx - 비동기 이벤트 기반의 구조와 다수의 연결을 효과적으로 처리 가능한 웹서버이며, 주로 Node.js 서버 앞단의 프록시 서버로 활용된다.
- 프록시 서버로 쓰는 CloudFlare - 전 세계적으로 분산된 서버가 있고 이를 통해 어떠한 시스템의 콘텐츠 전달을 빠르게 할 수 있는 CDN 서비스다.

### 이터레이터 패턴

- 이터레이터를 사용하여 컬렉션의 요소들에 접근하는 디자인 패턴

### 노출모듈 패턴

- 즉시 실행 함수를 통해 private, public 같은 접근 제어자를 만드는 패턴

### MVC 패턴

- 모델(Modal), 뷰(View), 컨트롤러(Controller)로 이루어진 디자인 패턴

### MVP 패턴

- MVC 패턴으로부터 파생되었으며 C의 컨트롤러가 프레젠터(presenter)로 교체된 패턴

### MVVM 패턴

- MVC 패턴으로부터 파생되었으며 C의 컨트롤러가 뷰모델(view modal)로 바뀐 패턴

---

# 프로그래밍 패러다임

- 프로그래머에게 프로그래밍의 관점을 갖게 해주는 역할을 하는 개발 방법론

## 선언형과 함수형 프로그래밍

- 선언형 프로그래밍 = '무엇을' 풀어내는가에 집중하는 패러다임이며, "프로그램은 함수로 이루어진 것이다."라는 명제가 담겨 있는 패러다임이기도 합니다.
- 함수형 프로그래밍은 선언형 패러다임의 일종이다.

## 객체지향 프로그래밍

- 객체들의 집합으로 프로그램의 상호 작용을 표현하며 데이터를 객체로 취급하여 객체 내부에 선언된 메서드를 활용하는 방식

```
const ret = [1, 2, 3, 4, 5, 11, 12]
class List {
    constructor(list) {
        this.list = list
        this.mx = list.reduce((max, num) => num > max ? num : max, 0)
    }
    getMax() {
        return this.mx
    }
}
const a = new List(ret)
console.log(a.getMax()) // 12
```

### 객체지향 프로그래밍의 특징

- 추상화 - 복잡한 시스템으로부터 핵심적인 개념 또는 기능을 간추려내는 것
- 캡슐화
- 상속성
- 다형성
- 오버로딩
- 오버라이딩

### 설계 원칙

- 단일 책임 원칙
- 개방-폐쇄 원칙
- 리스코프 치환원칙
- 인터페이스 분리 원칙
- 의존 역전 원칙

## 절차형 프로그래밍

## 패러다임의 혼합
