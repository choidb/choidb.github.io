---
title: 'Data Structure(자료구조)의 활용'
use_math: true
categories:
  - dsac
---


* 검색, 재귀
* 트리

## 1. 검색과 재귀(Serching and Recursion)

```python
# 인트로 코딩
# 중첩반복문 복습

numbers = [1,2,3,4]
len_numbers = len(numbers)
for i in range(0, len_numbers):   # 반복인덱스 : 0,1,2,3
  for j in range(1, len_numbers): # 반복인덱스 : 1,2,3
    print("i:",i," j:",j)
  print()
```
        > i: 0  j: 1
        > i: 0  j: 2
        > i: 0  j: 3

        > i: 1  j: 1
        > i: 1  j: 2
        > i: 1  j: 3

        > i: 2  j: 1
        > i: 2  j: 2
        > i: 2  j: 3

        > i: 3  j: 1
        > i: 3  j: 2
        > i: 3  j: 3

```python
# 입력된 리스트에서 요소들의 합을 큰 순서대로 구해보자(조건 : 모든 요소들의 합이 아니다.)
# 리스트의 메소드와 반복문을 활용해야 한다.

def remain_sum(numbers):
  result = []
  init_value = 0

  # 왼쪽인덱스부터 합을 구한다.
  # 반복문 : 0부터 4까지 result 리스트에 값을 append 한다.(반복인덱스 : 0,1,2,3)
  for i in range(0, len(numbers)):
    result.append(init_value)
    print("left sum - result[",i,"]:",result[i])
    init_value = init_value + numbers[i]    # append되는 index와 value를 구분해야 된다.

  init_value = 0   # 값 초기화(왼쪽에 대한 합을 구했으니, 이제 오른쪽인덱스부터 합구하기)

  # 구해진 값을 활용하여 오른쪽인덱스부터 더하면서 최종 리스트값을 구한다.
  # 반복문 : 3부터 -1까지 -1줄어들면서 result 리스트에 값을 더한다.(반복인덱스 : 3,2,1,0)
  for i in range(len(numbers)-1, 0-1, -1):
    result[i] = result[i] + init_value
    print("final sum - result[",i,"]:",result[i])
    init_value = init_value + numbers[i]

  return result

numbers = [int(numbers) for numbers in input("리스트값을 입력하세요 : ").split(',')]
print("결과:",remain_sum(numbers))
```

### 1) 검색(Searching)
* 특정 노드를 추가하거나 삭제위해 검색이 우선되야함
* 다양한 알고리즘을 활용할 경우, 최적 알고리즘 경로를 측정하는데 쓰임
* 검색하는 컬렉션이 무작위이고 정렬되지 않는경우 선형검색이 기본적인 검색방법임

```python
# 선형 검색 알고리즘
# 하나의 반복문과 리스트의 인덱스, 조건문을 활용하여 특정값을 검색할 때까지 반복한다.

def linear_search(arr, target):

    # 입력 배열의 각 항목을 반복
    for idx in range(len(arr)):
        # 현재 인덱스의 항목이 비교 대상과 같은지 확인
        if arr[idx] == target:
            # 현재 인덱스를 일치 항목으로 반환
            return idx
            
    # 전체 배열을 반복할 수 있다면, 비교 대상은 존재하지 않는다.(의미없는 -1 값 반환)
    return -1

print(linear_search([0,1,2], 2)) # case 1 - true
print(linear_search([0,1,2], 3)) # case 2 - false
```
    > 2
    > -1


### 2) 재귀(Recursion)
* 재귀함수란
  * 함수가 자기자신을 다시 호출하는것, 종료조건이 정상작동한다.
    * 종료조건이 충족될 때까지 반복적으로 스스로 불러내면서 주어진 작업을 수행하는 것
  * 반복문과 스택 구조가 결합된 함수
  * 파이썬 함수 &rArr; 콜스택 형태
* 재귀적인 문제 해결
  * 한 단계 낮은 문제가 해결된다면, 그것을 바탕으로 답을 얻을 수 있다.
  * 재귀함수 작성시
    * 재귀호출할 때 인자를 반드시 규모가 줄어들도록 설정
    * 재귀호출없이 해결할 수 있는 최소문제(base case) 설정하기
      * 이때는 재귀호출하지 않고, 바로 답을 반환할 수 있도록 하기

* 재귀의 개념은 수학적 사고에 기반하고, 코드를 작성하기 전에 문제를 해결하는 재호출 로직을 발견해야함
* 재귀 호출은 스택의 개념이 적용, 함수의 내부는 스택처럼 관리됨 (LIFO, 후입선출)
  * 단점: 재귀를 사용하면 함수를 반복적으로 호출되는 상황이므로 메모리를 많이 사용
  * 수학적으로 개념이 복잡한 경우 시간과 공간 복잡도 측면에서 효율이 안 좋더라도 재귀를 사용해서 문제를 해결해야함
  * 하위 문제를 쉽게 해결할 때까지 문제를 더 작은 하위 문제로 나누는 것임
  * 재귀적으로 다양한 문제를 해결할 수 있는데, 대표적으로 분할 정복법을 사용함
    * 분할 정복법: 하나의 문제를 분할하면서 해결하고 해결 후 하나로 다시 합침
    * 재귀는 해결을 위한 특적 기능을 재호출한다는 측면이고, 분할 정복은 문제를 분할하고 해결하는 구체적인 방법론임
    * 분할정복법을 활용하기 위해서는 재귀개념(기능 재호출)이 필요
    * 재귀에서는 조건에 따른 반복 계산을 중점적으로 생각한다.

```python
my_list = [1,2,3,4,5]
def sum_list(items):
    sum = 0
    for i in items:
        sum = sum + i
    return sum

sum_list(my_list)
```
    > 15

```python
def sum_list(items):
    if len(items) == 1: # Base Case(항목이 1개인 경우가 기본 케이스)
        return items[0]
    elif len(items)>1:
        print("items:",items[0:])
        return items[0] + sum_list(items[1:]) # items[:]는 한 항목씩 감소한다.
        
print("sum_list:",sum_list([2,3,4,5]))
```
    > items: [2, 3, 4, 5]
    > items: [3, 4, 5]
    > items: [4, 5]
    > sum_list: 14

```python
def add_two(num): # 매개변수
  return num + 2  # 반환값

def add_four(num):  # 매개변수
  return add_two(add_two(num))  # 반환값으로 매개변수가 있는 함수를 넣는다.

print(add_two(2))
print(add_four(6))
```
    > 4
    > 10

위의 함수에 대한 수행과정

 1) add_two(num) 함수 선언
 2) add_four(num) 함수 선언
 3) print(add_two(2)) 코드 읽기
 4) 선언된 add_two 호출
 5) return 4 값반환
 6) print(add_four(6)) 코드 읽기
 7) 선언된 add_four 호출
 8) return add_two(add_two(6)) 반환
 9) 선언된 add_two(6) 함수 호출
 10) return 8 값반환
 11) 선언된 add_two(8) 함수 호출
 12) return 10 값반환

* 재귀 제한
  * 파이썬에서는 재귀 깊이의 제한을 1000으로 기본 설정하고 있다.

  * 재귀 함수의 호출이 1000에 도달했을 때 RecursionError가 발생한다.

```python
# 파이썬에서 최대 재귀 깊이 확인하기
import sys
print(sys.getrecursionlimit())
```
    > 1000
```python
def sum_number(n):
    if n <= 0:
        return 0
    else:
      return n + sum_number(n-1)

print(sum_number(3000))
# 파이썬이 정한 최대 재귀 깊이보다 재귀의 깊이가 더 깊어질 경우 에러 발생!
```
```python
import sys
sys.setrecursionlimit(3500) # 재귀 깊이 3500으로 변경 

def sum_number(n):
    if n <= 0:
        return 0
    else:
      return n + sum_number(n-1)

print(sum_number(3000))
```
    > 4501500

## 2. 트리(Tree)
* 루트(root): 가장 위쪽에 있는 노드, 트리별 하나만 존재
  * 루트와 부모는 다름. 부모노드는 자식노드가 1개 이상 있는 경우만 존재
* 서브트리: 자식노드이면서 부모노드역할을 하는 노드가 있는 트리
* 차수: 노드가 갖고 있는 최대 자식노드 수
* 리프(leaf): 레벨별로 가장 마지막에 있는 노드, 단말노드(terminal node), 외부노드(external node)라 함. 리프는 트리별로 여러개 존재할 수 있음
* 레벨: 루트노드에서 얼마나 멀리 떨어져 있는지 각각 나타냄. 루트노드의 레벨은 0이고 아래로 내려갈때마다 1씩 증가함
* 높이: 루트에서 가장 멀리 떨어진 리프노드까지거리, 리프 레벨의 최대값을 높이라함
* sibling(형제) 노드: 부모가 같은 두 개의 노드

### 1) 바이너리 트리(이진 트리)
* 최대 2개의 서브노드를 가질수 있음(left, right)
* 가장 기본, 활용이 많이 됨
* 2가지 조건
  * 루트노드를 중심으로 두 개의 서브트리로 나뉨
  * 나눠진 두 서브트리도 각각 두 개의 서브트리를 가짐
    * 서브트리의 노드가 반드시 값을 안 가져도됨

```python
# 기본코드

class BinaryTreeNode:
    def __init__(self, value):
        self.left = None  # 왼쪽서브노드
        self.value = value
        self.right = None # 오른쪽서브노드
```

#### 1-1) Full Binary Tree(포화이진트리)
* 노드가 0개 혹은 2개를 가질 때
#### 1-2) Complete Binary Tree(완전이진트리)
* 노드가 위에서 아래로 채워져있다.
* 노드가 왼쪽에서 오른쪽 **순서**대로 채워져있다.
#### 1-3) Binary Search Trees(BST, 이진검색트리)
* 이진탐색트리는 노드를 정확하게 정렬해야하는 특정 유형의 이진 트리다. 

* BST의 목적은 단순 이진트리보다 빠른 노드탐색이다. 때문에 insert node에서 중복을 처리해주는 것이 아닌, 아래 '값 크기 조건'에 맞도록 값을 넣어주는 경우가 이진탐색트리가 되는 것이다.

* 만약 아래 '값 크기 조건'을 지키지 않고 값을 삽입하는 경우 '이진탐색트리'의 로직이 아닌 '단순이진트리'의 로직으로 '탐색'이 진행되므로 더 느린 탐색이 진행된다.

  * 값 크기 조건 : 오른쪽 서브노드의 값(right child) > 루트(부모)노드의 값(root node) > 왼쪽 서브노드의 값(left child)

    * 중복값을 갖고 있는 노드가 없어야 한다.

    * 왼쪽 서브트리노드들의 값은 루트(부모)노드값보다 작아야 한다.

    * 오른쪽 서브트리노드들의 값은 루트(부모)노드값보다 커야 한다.

  * 위에 대한 규칙이 정해진 이유는 왼쪽부터 오른쪽으로 검색을 하는 구조이기 때문이다.

    * 왼쪽 -> 오른쪽 개념이 적용되는 이유 : 트리와 같은 자료구조는 기본이 되는 연결리스트를 참조해서 만들어진 개념이기 때문이다.
  * 특징

    * 구조가 단순함

    * base node/검색할 노드/자식노드존재여부에 따라 검색되는 노드의 순서가 달라진다.

    * 검색이 일반 이진트리보다 빠르기 때문에 노드를 삽입하기 쉽다.

```python
# 노드 클래스 생성(해당 클래스는 검색알고리즘에 필요한 기본클래스이다.)

class node:
  def __init__(self, value):
    self.value = value
    self.left = None
    self.right = None
```
```python
# 이진검색트리에 노드삽입 함수추가

class binary_search_tree:
  def __init__(self, head):
    self.head = head

  def insert_node(self, value):
    self.base_node = self.head
    while True:
      if value < self.base_node.value:
        if self.base_node.left != None:
          self.base_node = self.base_node.left
        else:
          self.base_node.left = node(value)
          break
      else:
        if self.base_node.right != None:
          self.base_node = self.base_node.right
        else:
          self.base_node.right = node(value)
          break
```
```python
# 이진검색트리를 위한 기본노드생성

head = node(1)  # 루트노드 지정
bt = binary_search_tree(head) # binary_search_tree(node(1))
```
```python
# 이진검색트리에 값 삽입

bt.insert_node(2)
```
```python
# 이진검색트리에 노드검색 함수추가

class binary_search_tree:
  def __init__(self, head):
    self.head = head

  # 노드삽입
  def insert_node(self, value):
      # self.base_node = node(6)
    self.base_node = self.head

    while True:
    # 1 / 6 
    # 신규값(value)이 베이스노드(self.base_node.value)보다 작으면        
      if value < self.base_node.value:
          # 트리 왼쪽이 빈값이 아니면
        if self.base_node.left != None:
            # 베이스노드를 베이스노드 왼쪽 값으로 갱신
            # self.base_node (비포) 6 (에프터) 2
          self.base_node = self.base_node.left
          # 트리 왼쪽이 빈값이면
        else:
            # 베이스노드 왼쪽에 신규값을 넣는다.
          self.base_node.left = node(value)
          break
    # 신규값(value)이 베이스노드(self.base_node.value)보다 크면
      else:
        if self.base_node.right != None:
          self.base_node = self.base_node.right
        else:
          self.base_node.right = node(value)
          break

  # 노드검색
  def search_node(self, value):
    self.base_node = self.head

    while self.base_node:
      if self.base_node.value == value:
        return True
      ###### 검색부분 미구현 ######
    return False
```
```python
# 노드삽입

head = node(10)  # 루트노드지정
bt = binary_search_tree(head)

bt.insert_node(2)
bt.insert_node(5)
bt.insert_node(0)
bt.insert_node(-1)

bt.head.value # 출력


```


#### 1-4) Perfect Binary Tree
* 2^n-1
  * n: 노드 개수
