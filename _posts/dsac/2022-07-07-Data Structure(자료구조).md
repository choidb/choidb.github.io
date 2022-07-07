---
title: 'Data Structure(자료구조)'
use_math: true
categories:
  - dsac
---


* 자료구조의 가장 기본적인 의미
  * 자료를 쉽게 관리하기 위해 다양한 구조로 묶는 것
  * 자료구조: 자료를 저장하는 방법
    * data structure &rArr; 자료구조, 자료 &rArr; 데이터
  * 다양한 자료구조 &rArr; 각각의 자료구조마다 장단점 존재
* 자료구조 장점
  * 같은 알고리즘도 어떤 데이터 구조를 사용하는지에 따라 효율성이 달라짐
    * 모든 자료구조가 같은 효율성을 지니고 있지 않다.
    * 배열은 배열 안에 있는 자료를 불러오는 것이 빠르다.
    * 연결리스트
      * 연결리스트 같은 경우 n번째 자료에 접근하기 위해서 1번부터 모든 데이터를 거쳐서 가야되기 때문에 Read 연산이 느림.(연결리스트 단점)
      * 데이터를 삭제, 새로운 데이터를 추가하는 연산이 빠르다. 반면에 배열은 경우에 따라 느림.(연결리스트 장점)
        * 확장/축소(크기)
  * 데이터를 관리하는데 도움이됨
    * 선착순 &rArr; 수강신청, 타겟팅
    * 배열, 큐 자료구조
* 배열
  * 기본적인 자료구조 배열
  * 선형자료구조
    * 배열
      * 정해진 크기의 같은 타입의 데이터를 저장하는 구조
    * 동적배열
      * 크기가 정해지지 않은 데이터를 저장하기 위해 고안됨
    * 연결리스트
      * 각각의 데이터가 다음 데이터를 가리키도록해서 중간에 추가나 제거가 쉽게 되도록 고안됨
  * 비선형 자료구조 &rArr; 하나의 자료 뒤에 다수의 자료가 올 수 있는 형태

* 추상자료형(ADT)
* 연결리스트, 큐, 스택의 설계
* 연결리스트, 자료구조의 시간복잡도
  * 자료구조의 시간복잡도
    * 데이터 연산 4개: Read, Serach, Add, Delete
  * 연결리스트
    * 종류
      * 노드당 다음 노드를 알려주는 링크가 하나밖에 없다면 싱글의 **링크드 리스트(linked list)**
        * 한방향으로 이동함
      * 노드당 링크가 2개, 이전 노드를 갈 수 있는 링크가 추가하게 된다면 **더블리 링크드 리스트**
        * 양방향 움직임
      * **환형 링크드 리스트(Circular)**
        * 더블일 수도 있고, 싱글일 수도 있는데, 계속 앞으로 가서 맨 마지막 노드에 도착했을 때 다음이 어딘지 처음으로 알려주는 순환이되는 형태를 환형 링크드 리스트라함
        * 마지막 노드가 첫번째 노드를 가리켜서 계속 회전할 수 있게 만든 연결리스트



## 1. ADT(추상자료형)의 구체적 시작
### 1) ADT(Abstract Data Type)
* 프로그래밍하면서 데이터 처리를 위한 자료형이 존재함
* ADT는 추상적으로 필요한 기능을 나열한 일종의 명세서(로직)이다.
  * ADT는 기본자료형(리스트, 숫자, 문자열)을 활용해서 사용자에 의해 구현됨
* abstract는 소프트웨어가 발전하면서 프로그램의 크기나 복잡도가 같이 증가하였고 프로그램의 핵심부분을 간단하게 설명하기 위해 생겨났다.

### 2) linked-list(연결리스트)
* 리스트들을 연결해줌
  * 연결은 참조의 기능으로 구현됨
  * 연결리스트는 리스트의 길이를 별도로 지정해줄 필요가 없음
  * 배열은 요소를 직접 접근해 저장하고 인덱스를 활용함
  * 연결리스트와 각 요소는 참조하는 노드에 저장됨
    * 각 노드는 연결리스트의 다음 노드에 대해 참조(포인터)를 함
      * 참조기호: . 로 지칭
      * 삽입, 할당기호: = 로 표현

```python
# 연결리스트의 노드를 저장하는 첫 단계

class Node:
  def __init__(self,value,next=None):
    self.value = value  # 노드의 값을 나타내는 value
    self.next = next  # 노드의 다음위치를 가리키는 next의 초기값은 None

class linked_list:
  def __init__(self,value):
    self.head = Node(value) # 초기 클래스에 head노드선언

  def add_node(value):
    print('head.value:', head.value)
    print('head.next:', head.next)
    node = head           # 첫번째 위치에 해당하는 head를 생성하고, node 변수에 저장해둔다.
    while node.next:      # head노드의 다음위치에 노드가 생성될 때까지 반복문 진행한다.
      node = node.next    # head노드의 다음위치에 노드가 있는 경우(두번째 노드라고 가정),
      print('print in while:', node.next)
                          # 두번째 노드부터 node변수에 저장
    node.next = Node(value) # 데이터를 노드 다음위치에 저장
```
```python
# 연결리스트의 노드값들에 대해서 봐보자.

head = Node(5)    # head노드에 값5를 저장
linked_list.add_node(11) # 값11을 추가

print(head.value) # head노드의 값은 5
print(head.next.value) # head노드의 다음위치노드의 값은 11
```
    > head.value: 5
    > head.next: None
    > 5
    > 11

* 연결리스트의 핵심개념은 연결이고, 이것은 참조되는 노드의 '위치바꾸기'라고 할 수 있다.

```python
# 리스트를 연결해보자.

node1 = Node(3)
node2 = Node(4)

node3 = Node(5)
node4 = Node(6)

node1.next = node2
node2.next = node3
node3.next = node4

node = node1        # 첫번째노드부터 시작한다.
while node:         # 노드별로 반복문을 수행
  print(node.value) 
  node = node.next  # 다음노드를 현재노드에 저장하면서 위치를 바꾼다.
```
    > 3
    > 4
    > 5
    > 6

* 연결리스트도 리스트의 메소드와 같은 기능들을 구현할 수 있다.
  * 삽입 / 삭제 / 검색

```python
# 클래스에 연결리스트 구현
class Node:
  def __init__(self, value):
    self.value = value
    self.next = None

class linked_list:
  def __init__(self, value):
    self.head = Node(value)

  def add_node(self, value):
    if self.head == None:
      self.head = Node(value)
    else:
      node = self.head
      while node.next:
        node = node.next
      node.next = Node(value) # init함수의 value

  # 연결리스트의 삭제구현
  def del_node(self,value):
    if self.head == None:
      # 해당 값에 대한 노드는 없다.
      # 의미없는 조건에서 함수는 아무것도 반환하지 않는다. 
    elif self.head.value == value:
      # 노드의 위치를 변경시킨다.
      # 변경된 노드에 대해서 삭제를 진행한다.
    else:
      node = self.head
      while node.next:
        if node.next.value == value:
         # 노드의 위치를 변경시킨다.
         # 변경된 노드에 대해서 삭제를 진행한다.
        else : 
         # 다음 노드의 위치를 현재 노드에 넣어준다.

  # 연결리스트의 노드출력을 위한 기능
  def ord_desc(self):
    node = self.head
    while node:
      print(node.value)
      node = node.next 
  ```
  ```python
  # 노드출력 테스트
linkedlist = linked_list(0)
linkedlist.ord_desc()
```
```python
# 노드 삽입 테스트
for value in range(1,10):
  linkedlist.add_node(value)
linkedlist.ord_desc()
```
```python
# 연결리스트의 head의 주소를 확인함으로써 메모리상에 연결리스트가 존재함을 확인
linkedlist.head
```
```python
# 노드삭제 테스트 1
print('test1 ---------')
linkedlist = linked_list(0) # 노드 초기값 설정
linkedlist.del_node(0)  # 노드삭제
linkedlist.del_node(0)  # 노드삭제
linkedlist.ord_desc()

# 노드삭제 테스트 2
print('test2 ---------')
linkedlist = linked_list(0) # 노드 초기값 설정
linkedlist.add_node(1)
linkedlist.del_node(0)  # 노드삭제
linkedlist.ord_desc()

# 노드삭제 테스트 3
print('test3 ---------')
linkedlist = linked_list(0) # 노드 초기값 설정
for value in range(1,5):
  linkedlist.add_node(value)
linkedlist.del_node(3)  # 노드삭제
linkedlist.ord_desc()
```
* 노드간의 '동적'이라는 개념을 컴퓨터 프로그래밍에서는 '연결'이라는 개념으로 접목시켰다.

  * 연결하면서 값의 위치가 바뀌고 위치가 바뀌면 값도 바뀌는 것이다.

  * 위의 소스코드와 같은 경우는 주소의 위치를 바꿔주면서 '교체'를 해준다.

```python
# 연결리스트에서 검색구현
class Node:
  def __init__(self, value):
    self.value = value
    self.next = None

class linked_list:
  def __init__(self, value):
    self.head = Node(value)

  def add_node(self, value):
    if self.head == None:
      self.head = Node(value)
    else:
      node = self.head
      while node.next:
        node = node.next
      node.next = Node(value) # init함수의 value

  # 연결리스트의 삭제구현
  def del_node(self,value):
    # head의 참조값이 없는 경우
      # 해당 값에 대한 노드는 없다.
      # 의미없는 조건에서 함수는 아무것도 반환하지 않는다. 
    # head의 값이 현재 값과 같은 경우
      # 노드의 위치를 변경시킨다.
      # 변경된 노드에 대해서 삭제를 진행한다.
    # 나머지 경우
      node = self.head
      while node.next:
        if node.next.value == value:
         # 노드의 위치를 변경시킨다.
         # 변경된 노드에 대해서 삭제를 진행한다.
        else : 
         # 다음 노드의 위치를 현재 노드에 넣어준다.

  # 연결리스트의 노드출력을 위한 기능
  def ord_desc(self):
    node = self.head
    while node:
      print(node.value)
      node = node.next 
          
  # 연결리스트 검색함수
  def search_node(self,value):
    node = self.head
    # 노드가 있는 경우 아래 작업을 반복한다.
      # 노드의 값이 현재 값과 같은 경우
        #노드를 반환한다.
      # 노드의 값이 다른 경우
        # 다른 노드의 위치를 현재 노드에 넣어준다.
```
```python
linkedlist = linked_list(0) # 연결리스트 초기화

# 연결리스트에 노드 다시 추가
for value in range(1,11):
  linkedlist.add_node(value)
linkedlist.ord_desc()
```
```python
# 4라는 값을 갖고 있는 노드를 연결리스트에서 검색해보자.

node = linkedlist.search_node(4)
print(node.value)
print(node.next.value)      # 4 다음 값 검색
```
* 위의 head 노드를 삭제하는 것도 head 자체를 바로 삭제하는 것이 아니라, head의 위치를 바꿔주는 것이다.
* 기존방식이었던 인덱스를 통해 함수로 삽입/삭제/검색이 가능했었지만, 연결리스트는 인덱스의 기능을 할 수 있도록 노드별로 위치를 변경해줘야하는 다른 점이 있다.

### 스택 , 큐
* 스택
  * 팬케이크
  * 리포(Last in First Out)
  * 자료의 입출력이 한 방향에서만 이루어지는 자료구조
  * 스택의 주요기능
    * push: 스택에 데이터를 
    * pop:
* 큐
  * 파이포(First in First Out)
  * 줄서기
  * 한쪽 끝에서 데이터(자료)의 삽입 연산만 가능하고, 반대쪽 끝에서는 삭제 연산만 가능한 자료구조
  * 데이터를 꺼내는 쪽을 Front(맨 앞의 원소), 데이터 넣는쪽을 Rear(맨 끝의 원소)라고 함
    * enqueue: 큐에 값을 집어넣는 함수(스택의 역할)
    * dequeue: 큐에 값을 빼내는 함수

## 2. Queue(큐)

* 큐는 항목을 FIFO(first in, first out)[선입선출] 순서로 저장하는 자료구조이다.
* deque : double-ended queue
  * 큐에서 양방향으로 데이터를 처리함
  * double은 자료구조에서 양방향을 의미
  
```python
# 리스트 메소드를 사용해서 큐를 만들어보기

from collections import deque
queue = deque(["Eric", "John", "Michael"])
queue.append("Terry")           
queue.append("Graham")

print('queue:', queue)
print('queue.popleft():',queue.popleft())
print('queue.popleft():',queue.popleft())
print('queue:', queue) 
```
    > queue: deque(['Eric', 'John', 'Michael', 'Terry', 'Graham'])
    > queue.popleft(): Eric
    > queue.popleft(): John
    > queue: deque(['Michael', 'Terry', 'Graham'])

* Queue 클래스의 경우, 먼저 init 메서드를 정의해야한다.

  * 이 메서드에서 front(앞)와 rear(뒤) 인스턴스변수를 초기화 해야한다.

```python
class Queue:
    def __init__(self):
        self.front = None
        self.rear = None
```

* 큐의 Time and Space Complexity(시간, 공간 복잡도)

  * Enqueue(대기열에 넣기)

  * 데이터를 큐에 추가하면 (데이터를 큐 rear에 추가) O(1) 시간이 걸린다.

  * Dequeue(대기열에서 빼기)

  * 데이터를 큐에서 빼면 (데이터를 큐 front에서 제거) O(1) 시간이 걸린다.

*  연결리스트를 이용하여 큐와 스택을 구현하는 이유

  * 연결리스트는 파이썬에 없는 자료구조로, 사용하려면 직접 클래스로 구현하여 사용하여야 한다. 연결리스트를 구현하고 이해하기 위해서는 해당 자료구조를 많이 사용해 보아야 한다. 그렇기 때문에 연결리스트를 기반으로 큐와 스택 자료구조를 구현하는 연습을 해봄으로써 연결리스트를 좀 더 잘 이해하는 것을 목표로 한다.

```python
# 연결리스트를 이용한 큐 구현
class LinkedListNode:
    def __init__(self, data):
        self.data = data
        self.next = None

class Queue:
    def __init__(self):
        self.front = None
        self.rear = None

    # 대기열에서 넣기(큐에 값을 집어넣는 함수)
    def enqueue(self, item):
        new_node = LinkedListNode(item)
        # 큐가 비어있는지 체크
        if self.rear is None:
            self.front = new_node
            self.rear = new_node
        else:
            # 새로운 노드를 rear 다음에 삽입
            self.rear.next = new_node
            # 새로운 노드를 rear 재할당
            self.rear = new_node
        return new_node.data

    # 대기열에서 빼기(큐에서 값을 빼내는 함수)
    def dequeue(self):
        # 큐가 비어있는지 체크
        if self.front is not None:
            # front값을 old front에 삽입
            old_front = self.front
            # old front 다음 값을 front값에 삽입
            self.front = old_front.next

        # 큐가 비어있는지 체크
        if self.front is None:
            # rear를 None으로 지정한다.
            self.rear = None

        return old_front.data
    
    # 연결리스트의 노드출력을 위한 기능
    def ord_desc(self):
        node = self.front
        while node:
            print(node.data)
            node = node.next
```
```python
print('1,2,3 차례대로 추가하기:')
q = Queue()
q.enqueue(1)
q.enqueue(2)
q.enqueue(3)
q.ord_desc()

print('대기열에서 빼기:')
q.dequeue()
q.ord_desc()
```
    > 1,2,3 차례대로 추가하기:
    > 1
    > 2
    > 3
    > 대기열에서 빼기:
    > 2
    > 3
* enqueue에서는 새로운 노드의 저장공간(변수)를 만들어주고, 그 저장공간에 노드를 넣어주는 개념이다.

* dequeue는 삭제할 노드를 위해 저장공간(변수)를 만들어주고, 그 저장공간에 삭제노드를 넣어주는 개념이다.

## 3. Stack(스택)
* 파이썬의 리스트는 동적으로 처리
* 스택이 컴퓨터 프로그램 활용 예시) 윈도우 프로그램(컴퓨터 종료시, 가장 먼저 운영체제가 구동되고 가장 마지막으로 종료됨)

```python
# 리스트 메소드를 사용해서 스택만들어보기

stack = [3, 4, 5]
stack.append(6)
stack.append(7)
print(stack)

stack.pop()
print(stack)

stack.pop()
print(stack)

stack.pop()
print(stack)

# 위의 코드처럼 push와 pop을 활용해서 공간에 값이 유동적으로 변한다.(동적처리)
```
    > [3, 4, 5, 6, 7]
    > [3, 4, 5, 6]
    > [3, 4, 5]
    > [3, 4]
* 리스트를 사용하여 스택을 구현하는 방법

```python
class Stack:
    def __init__(self):
        self.data = []    # 동적처리(리스트값이 정해져있지 않음, 대괄호만 선언 및 저장)
```
* push 함수는 파이썬의 리스트개념과 리스트메소드(append, pop)를 사용하여 인덱스를 추가한다.

* pop 함수는 인덱스의 마지막 노드를 추출한다.

```python
class Stack:
    def __init__(self):
        self.data = []

    def push(self, item):
        self.data.append(item)

    def pop(self):
        if len(self.data) > 0:
            return self.data.pop()
        return "The stack is empty"
```
* 내장함수가 아닌 연결리스트 개념과 단순 변수를 사용하여 스택을 구현 방법

```python
class LinkedListNode:
    def __init__(self, data):
        self.data = data
        self.next = None

class Stack:
    def __init__(self):
        self.top = None
```
* 아래 push 함수는 연결리스트의 헤드에 새 노드를 삽입한다.

* pop 함수는 연결리스트의 헤드(최상단)에 있는 노드를 추출한다.

* 스택의 소스코드도 큐와 동작은 유사하지만, 입출력의 순서는 반대이다.

```python
# [연결리스트를 이용한 스택 구현]
# 아래의 코드는 스택이 내부적으로 어떻게 작동되는지 확인하기 위해 작성되었다.
# 파이썬에서 자체적으로 제공하는 리스트의 append, pop 메소드를 활용하면 쉽게 구현될 수 있지만,
# 아래처럼 다른 방법으로도 구현하는 코드를 보면서 스택에 대한 이해도를 높일 수 있다.

class LinkedListNode:
    def __init__(self, data):
        self.data = data
        self.next = None

class Stack:
    def __init__(self):
        self.top = None

    def push(self, data):
        # 신규 노드 생성
        new_node = LinkedListNode(data)
        # 최상단의 노드를 신규 노드 다음 노드로 삽입
        new_node.next = self.top
        # 신규 노드를 최상단에 삽입
        self.top = new_node
        return new_node.data

    def pop(self):
        # 스택이 비어있는지 확인
        if self.top is not None:
            # 최상단의 노드를 삭제할 노드로 삽입
            popped_node = self.top
            # 삭제할 노드 다음 노드를 최상단의 노드로 삽입
            self.top = popped_node.next
            # 삭제할 노드로부터 값 리턴
            return popped_node.data

    # 연결리스트의 노드출력을 위한 기능
    def ord_desc(self):
        node = self.top
        while node:
            print(node.data)
            node = node.next
```
```python
# 스택에 내부적으로 값을 쌓고 pop하는 과정을 살펴본다.
s = Stack()

print('1,2,3 차례대로 추가하기:')
s = Stack()
s.push(1)
s.push(2)
s.push(3)
s.ord_desc()

print('대기열에서 빼기:')
s.pop()
s.ord_desc()
```
    > 1,2,3 차례대로 추가하기:
    > 3
    > 2
    > 1
    > 대기열에서 빼기:
    > 2
    > 1

