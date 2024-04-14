###### date | 2024.04.00 ~ 2024.04.14

###### week | 6th week

# 자료 구조
###### data structure

- 자료 구조는 효율적으로 데이터를 관리, 수정, 삭제, 탐색, 저장할 수 있는 데이터 집합 
- C++은 STL을 기반으로 전반적인 자료 구조를 가장 잘 설명할 수 있는 언어

<details>
  <summary>STL</summary>
  <p>C++의 표준 템플릿 라이브러리이자 스택, 배열 등 데이터 구조의 함수 등을 제공하는 라이브러리의 묶음</p>
</details>

<br />
<br />

## 복잡도

### 시간 복잡도

<p align="center">
  <img width="40%" src="https://github.com/inside-coding/cs-note/assets/134191817/a4071084-80f7-4d40-9052-883d5d252b0c" />
</p>


- 입력 크기에 대해 어떠한 알고리즘이 실행되는 데 걸리는 시간
- 주요 로직의 반복 횟수를 중점으로 측정
- 일반적으로 **빅오 표기법**으로 나타냄
- **효율적인 코드로 개선하는데 쓰이는 척도**

##### 빅오 표기법

- 입력 범위 n을 기준으로 로직이 몇 번 반복되는지 나타내는 표기법
- 가장 영향을 많이 끼치는 항의 상수 인자를 빼고 나머지 항을 제외
- 입력 크기가 커질수록 연산량이 가장 많이 커지는 항만 신경 쓰면 된다는 이론

<br />

#### 자료 구조에서의 시간 복잡도 

아래는 자주 쓰이는 자료 구조의 시간 복잡도를 나타낸 표입니다.
보통 시간 복잡도를 생각할 때 평균과 최악을 고려하며 사용합니다.

<p align="center">
  <img width="70%" src="https://github.com/inside-coding/cs-note/assets/134191817/c1db6ef0-dae4-4bfe-ab5d-af628595cef2" />
  <img width="70%" src="https://github.com/inside-coding/cs-note/assets/134191817/f9a6bf13-8bc2-4db5-a69c-42f4af996299" />
</p>

<br />

### 공간 복잡도

- 프로그램을 실행시켰을 때 필요로 하는 자원 공간의 양
- 공간을 계속해서 필요로 하는 경우도 포함

<br />
<hr />

## 선형 자료 구조

요소가 일렬로 나열돼 있는 자료 구조

### 연결 리스트

<p align="center">
  <img width="50%" src="https://github.com/inside-coding/cs-note/assets/134191817/b51a4d6e-c01d-42aa-ab5a-bc0d7226d94c" />
</p>

- 데이터를 감싼 노드를 포인터로 연결해 공간적인 효율성을 극대화시킨 자료 구조
- 삽입과 삭제 → O(1)
- 탐색 → O(n)
- next와 prev 포인터로 앞/뒤의 노드를 연결시킨 것
- 맨 앞에 있는 node는 head node라고 함
- **데이터 추가와 삭제**에 용이

<br />

#### 연결 리스트 종류

<p align="center">
  <img width="50%" src="https://github.com/inside-coding/cs-note/assets/134191817/73394dfd-92b7-46a1-9fa1-d123f58e4c3f" />
</p>

- **싱글 연결 리스트** : next 포인터만
- **이중 연결 리스트** : next 포인터 + prev 포인터 둘 다
- **원형 이중 연결 리스트** : 마지막 노드의 next 포인터가 head node를 가리킴 (나머지는 이중 연결 리스트와 동일)


<br />

### 배열 (Array)

- 같은 타입의 변수들로 이뤄짐
- 크기가 정해져 있음
- 인접한 메모리 위치에 있는 데이터를 모아놓은 집합
- 중복을 허용
- 순서가 존재
- 접근/참조 → O(1)
- 삽입과 삭제 → O(n)
- 랜덤 접근 가능
- **접근/참조**에 용이

<br />

#### 랜덤 접근과 순차적 접근

<p align="center">
  <img width="40%" src="https://github.com/inside-coding/cs-note/assets/134191817/c9d9577f-878d-4ec3-a1b1-2e7109ef85b6" />
</p>

- **랜덤 접근** : 동일한 시간에 배열과 같은 순차적인 데이터가 있을 때 임의의 인덱스에 해당하는 데이터에 접근할 수 있는 기능
- **순차 접근** : 데이터를 저장된 순서대로 검색

#### 배열과 연결 리스트의 차이

- 배열 : 상자를 순서대로 나열한 데이터 구조 → 몇 번째 상자인지 알면 해당 상자의 요소를 끄집어낼 수 있음
- 리스트 : 상자를 선으로 연결한 데이터 구조 → 상자 안 요소를 알기 위해선 상자 내부를 확인해야 함

<p align="center">
  <img width="50%" src="https://github.com/inside-coding/cs-note/assets/134191817/6ea3b337-5e49-47c2-aefd-2df801eb8522" />
</p>

접근/참조는 배열이 용이하고 추가와 삭제는 리스트가 용이합니다.

<br />

### 벡터 (Vector)

- 동적으로 요소를 할당할 수 있는 동적 배열
- 컴파일 시점에 개수를 모를 경우 사용
- 중복을 허용
- 순서 존재
- 랜덤 접근 가능
- 탐색과 맨 뒤 요소 삭제와 삽입 → O(1)
- 맨 뒤가 아닌 요소 삭제와 삽입 → O(n)

<br />

### 스택 (Stack)

<p align="center">
  <img width="50%" src="https://github.com/inside-coding/cs-note/assets/134191817/df1fb95a-9303-4c04-b01e-5a28c06c6b89" />
</p>

- 선입선출 (LIFO)
- 삽입과 삭제 → O(1)
- 탐색 → O(n)
- 사용 : 재귀적인 함수, **알고리즘**, **웹 브라우저 방문 기록** 등

<br />

### 큐 (Queue)

<p align="center">
  <img width="50%" src="https://github.com/inside-coding/cs-note/assets/134191817/35addbf5-482a-4089-9543-c00626f950e8" />
</p>

- 후입선출 (FIFO)
- 삽입과 삭제 → O(1)
- 탐색 → O(n)
- 사용 : CPU 작업을 기다리는 프로세스, **스레드 행렬**, **네트워크 접속을 기다리는 행렬**, 너비 우선 탐색, **캐시** 등

<br />
<hr />

## 비선형 자료 구조

일렬로 나열하지 않고 자료 순서나 관계가 복잡한 구조


<br />

### 그래프 (Graph)

<p align="center">
  <img width="40%" src="https://github.com/inside-coding/cs-note/assets/134191817/5279f9cf-5119-41ef-982a-d9f08664d680" />
</p>

- 정점과 간선으로 이뤄진 자료 구조
- "어떠한 곳에서 무언가를 통해 간다." 에서 어떠한 곳은 정점(vertex), 무언가는 간선(edge)
- 단방향 간선과 양방향 간선

<p align="center">
  <img width="40%" src="https://github.com/inside-coding/cs-note/assets/134191817/8a2cb855-fdf7-4fb8-a21b-885309b13c0d" />
</p>

- 정점으로 나가는 간선을 해당 정점의 outerdegree, 들어오는 간선을 해당 정점은 indegress라고 함
- 보통 어떤 정점으로붜 시작해 어떤 정점까지 간다 === "U에서부터 V까지 간다."
- **가중치** : 간선과 정점 사이에 드는 비용


<br />

### 트리 

<p align="center">
  <img width="50%" src="https://github.com/inside-coding/cs-note/assets/134191817/3a44acab-f73f-4b60-bba8-5eac151a023b" />
</p>

- 그래프 중 하나로 그래프의 특징처럼 정점과 간선으로 이뤄짐
- 트리 구조로 배열된 일종의 계층적 데이터의 집합
- 구성요소 : 루트 노드, 내부 노드, 리프 노드
- 숲 : 트리로 이뤄진 집합

#### 트리의 종류

##### 이진 트리
자식의 노드 수가 두 개 이하인 트리


<p align="center">
  <img width="50%" src="https://github.com/inside-coding/cs-note/assets/134191817/bdbd35e1-e178-4f5b-8b2d-c16041eb2b44" />
</p>

- **정이진 트리** : 자식 노드가 0 또는 두 개인 이진 트리
- **완전 이진 트리** : 왼쪽에서부터 채워져있는 이진 트리
- **변질 이진 트리** : 자식 노드가 하나 밖에 없는 이진 트리
- **포화 이진 트리** : 모든 노드가 꽉 차 있는 이진 트리
- **균형 이진 트리** : 왼쪽과 오른쪽 노드의 높이 차이가 1 이하인 이진 트리

<br />

#### 이진 탐색 트리 (BST)

노드의 오른쪽 하위 트리에는 '노드 값보다 큰 값'이 있는 노드만 포함되고 왼쪽 하위 트리에는 '노드 값보다 작은 값'이 들어 있는 트리

<p align="center">
  <img width="50%" src="https://github.com/inside-coding/cs-note/assets/134191817/948969eb-c910-4b50-847f-f1d031b727e4" />
</p>

<br />

#### AVL 트리
###### Adelson-Velsky and Landis tree

<p align="center">
  <img width="50%" src="https://github.com/inside-coding/cs-note/assets/134191817/9c6cb769-87e6-48f9-8590-0c0dcab2b18d" />
</p>


- 위에 있는 최악의 경우 선형적인 트리가 되는 것을 방지하고 스스로 균형을 잡는 이진 탐색 트리
- 두 자식 서브 트리의 높이는 항상 최대 1만큼 차이가 난다는 특징 존재

<br />

#### 레드 블랙 트리

<p align="center">
  <img width="50%" src="https://github.com/inside-coding/cs-note/assets/134191817/4b26b87f-1a0c-4338-b1ee-f035588f845f" />
  <img width="50%" src="https://github.com/inside-coding/cs-note/assets/134191817/4fd677a1-b144-454b-b208-6239d0cbfb3e" />
</p>

- 균형 이진 탐색 트리
- 탐색, 삽입, 삭제 모두 시간 복잡도가 O(logn)
- 각 노드는 빨간색/검은색의 색상을 나타내는 추가 비트를 저장
- 삽입과 삭제 시 트리가 균형을 유지하도록 하는 데 사용
- 규칙 : "모든 리프 노드와 루트 노드는 블랙이고 어떤 노드가 레드이면 그 노드의 자식은 반드시 블랙이다."

<br />

### 힙 (heap)

- 완전 이진 트리 기반의 자료 구조

<p align="center">
  <img width="50%" src="" />
</p>

- 최소힙과 최대힙
- 해당 힙에 따라 특정한 특징을 지킨 트리
- 어떤 값이 들어와도 특정 힙의 규칙을 지키도록 만들어짐

<br />

### 우선순위 큐 (Priority Queue)

<p align="center">
  <img width="50%" src="https://github.com/inside-coding/cs-note/assets/134191817/84dfcb04-394b-43c1-8dc5-7331ac820282" />
</p>

- **대기열**이라고도 함
- 우선순위가 높은 요소가 우선순위가 낮은 요소보다 먼저 제공되는 자료 구조
- 힙을 기반으로 구현


<br />

### 맵 (Map)

- 특정 순서에 따라 키와 매핑된 값의 조합으로 형성된 자료 구조
- 레드 블랙 트리 자료 구조를 기반으로 형성
- 삽입 시 자동으로 정렬
- map은 해시 테이블을 구현할 때 사용
- 정렬 보장이 되지 않는 unordered_map과 정렬을 보장하는 map으로 나뉨

<br />

### 셋 (Set)

- 특정 순서에 따라 고유한 요소를 저장하는 컨테이너
- 중복되는 요소는 없고 오로지 희소한 unique 값만 저장하는 자료 구조


<br />

### 해시 테이블 (hash table)

- 무한에 가까운 데이터들을 유한한 개수의 해시 값으로 매핑한 테이블
- 삽입,삭제, 탐색 시 평균적으로 O(1) 시간 복잡도를 가짐
- unordered_map으로 구현

<br />
<hr />
