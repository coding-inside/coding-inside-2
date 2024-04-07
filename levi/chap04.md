## 📖 ERD란?

> **객체-관계 모델 (Entity-Relationship Modeling)**은 세상의 사물을 개체 (Entity)와 개체 간의 관계 (Relationship)로 표현하는 데이터 모델링 방식으로 개념적 데이터 모델링 단계에서 사용된다.

![](https://velog.velcdn.com/images/psik_2/post/8f44245b-f89c-43de-a013-1c9b805f2bc5/image.avif)

즉 ERD는 데이터베이스를 구축할 때 가장 기초적인 뼈대 역할을 하며, 릴레이션 간의 관계들을 정의한 것이다.

## 📖 Entity

> **Entity**는 관리하고자 하는 정보의 실체이며, 사물, 객체 혹은 개념이다.

Entity를 그대로 번역하면 실제, 독립체라는 뜻으로 데이터 모델링에 사용하는 객체를 의미한다. 즉 Entity는 업무에 필요하고 유요한 정보를 저장.관리하기 위한 **어떤 것(thing)**이라고 말할 수 있다.

**어떤 것**이라고 부르는 것처럼 엔터티는 추상적인 의미를 가지며 학교나 학생처럼 현실 세계에서 눈에 보이는 개념일 수도 있고 주문이나 결제처럼 눈에 보이지 않는 개념일 수도 있다.
![](https://velog.velcdn.com/images/psik_2/post/d4bcaa2c-73b5-4e07-bfe9-76d1fc8def32/image.png)
위 사진은 학생이라는 엔티티에 속성으로 구성된 인스턴스로 이루어져 있다.
이 때 **엔티티**는 **데이터베이스 테이블**, **인스턴스**는 **데이터베이스에 저장된 내용의 전체 집합**, **속성**은 **인스턴스의 구성 요소**이다.

_**그렇다면 어떤것을 엔티티로 도출해야 할까?**_

**업무에서 반드시 필요로 하는 정보여야 한다.**
![](https://velog.velcdn.com/images/psik_2/post/0dff550d-8a6e-4351-a363-28af9c447645/image.png)
위 사진에서 환자라는 엔티티는 병원에 있어서는 반드시 필요한 엔티티지만 일반 회사에서는 전혀 알 필요가 없는 엔티티이다.

**엔티티는 유일한 식별자가 있어야한다.**

![](https://velog.velcdn.com/images/psik_2/post/819cb8d8-b939-483e-82f5-ba1fce3505eb/image.png)

일반적으로 회사에서 직원을 구분할 수 있는 방법은 이름과 사원 번호가 있다. 이때 이름의 경우 동명이인이 있을시 정확히 식별하기 힘들다. 즉 사원번호는 고유하게 부여된 번호이므로 유일한 식별자가 될 수 있다.

**두 개 이상의 인스턴스 집합이어야 한다.**
![](https://velog.velcdn.com/images/psik_2/post/e896f199-0587-43ac-80ee-cd5e4f7756a8/image.png)

영속적으로 존재하는 인스턴스의 집합이 되어야 한다. 이때 집합은 한 개가 아닌 반드시 두 개 이상일 때 집합이라고 한다.

**업무 프로세스에 이용되어야 한다.**
![](https://velog.velcdn.com/images/psik_2/post/7f2ae68f-47c6-4515-a68b-3a6f494be5dd/image.png)

엔터티가 필요하다고 생각하여 만들었는데 업무 프로세스에 의해 전혀 사용되지 않는다면 어떻게 해야 할까? 이는 업무 분석, 업무 프로세스 도출이 적절하게 이루어지지 않았음을 의미한다

**반드시 속성을 포함해야 한다.**

![](https://velog.velcdn.com/images/psik_2/post/463bc514-d260-4067-b185-cd4ae9272500/image.png)

속성을 포함하지 않는 엔터티는 있어도 의미가 없다. 이런 엔티티는 관계가 생략되어 있거나 업무 분석이 미진하여 속성 정보가 누락되는 경우에 주로 발생한다.

**다른 엔티티와의 관계가 존재해야 한다.**
![](https://velog.velcdn.com/images/psik_2/post/0d7ac608-39c2-4e6a-8dd9-f576e1107bd5/image.png)

엔터티는 다른 엔터티와 최소 한 개 이상의 관계가 존재해야 한다.

_**그렇다면 엔티티는 어떻게 분류하는것이 좋을까?**_

엔터티는 존재하느냐 하지 않느냐와 같은 실체 유형에 따라 구분하거나 업무를 구성하는 모습에 따라 구분이 되는 발생 시점에 의해 분류할 수 있다.

물리적 형태가 존재하는지에 따라 유형, 개념, 사건 엔티티로 분류된다.

![](https://velog.velcdn.com/images/psik_2/post/a483a215-7a05-49d8-9986-9dc315f9f999/image.png)

또한 발생 시점에 따라 기본, 중심, 행위 엔티티로 분류된다.
![](https://velog.velcdn.com/images/psik_2/post/af016a47-4681-4cfd-839c-9e4233110d9c/image.png)

## 📖 ERD 엔티티 관계 표기법

각 엔티티 유형들을 만들었으면, 엔티티 끼리 관계가 있는 경우 선을 이어 관계를 맺어야 한다.

엔티티 끼리 관계 선을 그을때 실선으로 그을지 점선으로 그을지 나뉘는데, 두 엔티티 관계에서 부모의 키를 자식에서 PK로 사용하는지 일반 속성으로 사용하지에 따라서 표기가 다르게 된다.

![](https://velog.velcdn.com/images/psik_2/post/f7faf2ae-3991-4865-8800-2e809f66fd4e/image.png)

실선으로 그으면 강한 관계를 나타내는 것이며 **식별자 관계**라고 불리우며, 점선으로 그으면 약한 관계를 나타내는 것이며 **비식별자 관계**라고 불리우게 된다.

### ERD 카디널리티

관계가 존재하는 두 엔티티 사이에 한 엔티티에서 다른 엔티디 몇개의 개체와 대응되는지 제약조건을 표기하기위해 선을 그어 표현한다. 대표적으로 Mapping Cardinality의 종류는 다음과 같다.

**One-to-One Cardinality (1:1 관계)**
![](https://velog.velcdn.com/images/psik_2/post/6b00b814-f71a-4c9b-965c-3c69f510be30/image.png)

위 사진에서 학생과 신체 정보는 1대1로 매칭된다.

**One-to-Many Cardinality (1:N 관계)**

![](https://velog.velcdn.com/images/psik_2/post/01384341-4d3f-475f-976a-daef6b30b513/image.png)

한명의 학생은 여러개의 취미를 가질수도 있다.

**Many-to-Many Cardinality (M:N 관계)**
![](https://velog.velcdn.com/images/psik_2/post/aad74a88-3e37-4f64-a8c9-20bb9ea0f6ee/image.png)

제품 엔티티 입장에서, TV 제품은 대우 티비, 삼성 티비, 애플 티비 같은 여러 제조업체 제품이 있을 수 있다. 제조업체 엔티티 입장에서, 삼성 제조업체는 세탁기만 생산하는게 아닌 MP3도 같이 생산한다.

### ERD 관계의 참여도

![](https://velog.velcdn.com/images/psik_2/post/715b64be-154e-4ee7-9627-c84e46e18d3f/image.png)

관계선 각 측의 끝자락에 기호를 표시한다. **'|'** 표시가 있는 곳은 반드시 있어야 하는 필수적인 개체다. **'O'** 표시가 있다면 없어도 되는 선택적인 개체이다.

이때까지 정리한 것을 정리하여 정의하면 아래와 같이 ERD를 설계할 수 있는것을 알 수 있다.

![](https://velog.velcdn.com/images/psik_2/post/d6a7b209-713e-4db5-9b80-c90713c22020/image.png)
