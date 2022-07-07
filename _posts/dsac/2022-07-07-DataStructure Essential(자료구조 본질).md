---
title: 'DataStructure Essential(자료구조 본질)'
use_math: true
categories:
  - dsac
---


* 데이터 활용 입장 / 컴퓨터 내부 동작에 대한 생각해 보기
* Big O 및 복잡도 개념(알고리즘 효율성)
* 참조와 할당
* 성능
* Big O 표기법(시간복잡도, 공간복잡도)

> 책 추천: 코드 없는 알고리즘과 데이터구조

## 1. 자료구조의 배경

### 1) 자료구조의 시작
실생활에서 발생하는 대용량의 다양한 데이터를 효율적으로 처리(저장)하기 위해 자료구조라는 개념이 개발됨
* 효율적인 처리?
  * 자동화
  * 빠른 계산
  * 반복 내용 처리
  * 여러개의 값을 한 번에 처리
  * 값이 빠르게 변경되는 경우에 대한 처리
  * 특정 변수에 대한 처리
  * 특정 값을 다양한 형태로 보기 원할 경우
  * 조건에 따른 처리

```python
# 인트로 코딩
# 특정 두 수의 합과 같은 인덱스값을 찾자.
def twonumbersum(numbers, result):
  for i in range(len(numbers)):
    for j in range(i+1, len(numbers)):
      if numbers[i] + numbers[j] == result:
        return [i,j]

# 리스트값을 받기 위한 코드: 리스트 컴프리헨션 & 리스트 메소드(split) 활용
# input 예시: 10,5,7
numbers = [int(numbers) for numbers in input("리스트값을 입력하세요 : ").split(',')]
# input 예시: 17
result = int(input("두 수의 합을 입력하세요 : "))

print("인덱스값 : ", twonumbersum(numbers,result))
```
    > 리스트값을 입력하세요 : 10,5,7
    > 두 수의 합을 입력하세요 : 17
    > 인덱스값 :  [0, 2]

#### 1-1) 함수에 값만 전달하는 경우

```python
# 함수에 값만 전달하는 경우
def remainder(num, div):
    return num % div

print(remainder(20, 7))   # argument에 값 전달
```
    > 6

#### 1-2) 함수에 변수이름과 값을 함께 전달하는 경우
  
```python
# case 1 - 함수에 변수이름과 값을 함께 전달하는 경우
def remainder(num, div):
    return num % div

print(remainder(num = 20, div = 7))
```
    > 6
    * case 1처럼 코드를 작성하게 되면 대규모 프로젝트를 진행하는 경우에 처음 코드를 보는 사람도 함수에 전달되는 값이 무엇인지 알 수 있다.

#### 1-3) 함수에 디폴트값을 할당해주는 경우

```python
# case 2 - 함수에 디폴트값을 할당해주는 경우
def remainder(test, num = 5, div = 2):
    return num % div

print(remainder(test = 7))
```
    > 1
    * case 2처럼 파라미터를 디폴트값으로 하는 방법도 있는데, 이 방법은 함수에 전달되는 argument값이 고정값일 때 유연하게 쓰일 수 있다.

#### 1-4) 자료구조의 다양한 활용
* 자료구조를 체계적으로 정립하기 위해 프로그래밍 언어별로 다양한 자료형이 생겨났고, 파이썬에서는 **리스트**와 **튜플**을 통해서 자료구조의 기본인 배열을 구현할 수 있게됨
  * 배열이란
    * 컴퓨터과학에서 사용되는 기본용어
    * 배열의 기능은 각각의 변수를 하나의 변수에 여러개의 인덱스로 묶는 것.
    * 파이썬에서는 배열을 리스트와 튜플로 구현하고 활용함
* 파이썬은 리스트 자료형이 자료구조의 연결리스트로 기능을 지원함
* 리스트는 임의의 메모리(위치)에 자료를 동적으로 처리할 수 있음
* 파이썬의 리스트는 자료구조의 배열과 연결리스트의 특징을 모두 갖고 있음
  * 배열의 특징: 인덱스를 사용해 노드에 접근가능
  * 연결리스트의 특징: 인덱스 크기를 자유롭게 확장가능, 서로 다른 자료형을 노드로 가질 수 있다.
  * 파이썬 프로그래밍 언어는 기존 프로그래밍에서 발생한 부분을 개선시킴.

#### 1-5) 자료구조 개념이 있기 전

```python
# 자료구조라는 개념이 있기 전에는 필요할 때마다 변수를 만들어서 사용했다.

arr1 = 7
arr2 = 5
arr3 = 3
arr4 = 1
print(arr1)
print(arr2)
print(arr3)
print(arr4)
```
    > 7
    > 5
    > 3
    > 1
#### 1-6) 배열의 개념이 생긴 후 배열요소와 인덱스 활용해 배열을 구성

```python
# 배열의 개념이 생겼고 배열요소와 인덱스를 활용되어 배열이 구성된다.

arr = [7,5,3,1] # arr[0],arr[1],arr[2],arr[3]는 배열요소를 뜻하고, [0],[1],[2],[3]는 인덱스를 뜻한다.
print(arr[0])
print(arr[1])
print(arr[2])
print(arr[3])
```
    > 7
    > 5
    > 3
    > 1

#### 1-7) 배열의 구성(파이썬 리스트 활용)

```python
# 파이썬의 리스트를 활용하여 배열이 어떻게 구성되어있는지 알아보자.

arr = [1,2,3,4,5,6] # 리스트 이름선언 및 값 할당

for i in range(0,arr[5]):   # 반복문을 활용하여 코드 한 줄로 리스트전체를 출력한다.(반복과 자동화개념)
  print('배열요소 : ', arr[i], ', 배열인덱스 : ', [i])
```
    > 배열요소 :  1 , 배열인덱스 :  [0]
    > 배열요소 :  2 , 배열인덱스 :  [1]
    > 배열요소 :  3 , 배열인덱스 :  [2]
    > 배열요소 :  4 , 배열인덱스 :  [3]
    > 배열요소 :  5 , 배열인덱스 :  [4]
    > 배열요소 :  6 , 배열인덱스 :  [5]

```python
# len() 함수를 활용하여 배열의 원소길이 구하기
# 기존에 파이썬에서 배웠던 리스트 메소드이다.

x = [15,'x',20,13,['a','b'], 'cde','1']

# 리스트의 전체 길이 출력
print(len(x))
# 리스트의 특정 인덱스의 길이 출력
print(x[1],'의 length: ', len(x[1]))
print(x[4],'의 length: ',len(x[4]))
print(x[5],'의 length: ',len(x[5]))
print(x[6],'의 length: ',len(x[6]))
# print(x[6],'의 length: ',len(x[0]))  # 주석 풀어서 에러파악
```

    > 7
    > x 의 length:  1
    > ['a', 'b'] 의 length:  2
    > cde 의 length:  3
    > 1 의 length:  1

#### 1-8) 파이썬의 리스트
* 자료구조의 기본은 배열이라 할 수 있고, 파이썬에서는 리스트와 튜플로 구현할 수 있음
* 리스트나 튜플의 핵심은 인덱스를 사용하는 것임

```python
# 리스트 인덱싱/슬라이싱 예시

s = [11,22,33,44,55]

print('s[0:3] 결과:', s[0:3])
print('s[:3] 결과:', s[:3])
print('s[1:] 결과:', s[1:])
print('s[::2] 결과:', s[::2])
print('s[0:1:3] 결과:', s[0:1:3])
print('s[-3] 결과:', s[-3])
print('s[-3:-1] 결과:', s[-3:-1])
print('s[1:-1] 결과:', s[1:-1])
```
    > s[0:3] 결과: [11, 22, 33]
    > s[:3] 결과: [11, 22, 33]
    > s[1:] 결과: [22, 33, 44, 55]
    > s[::2] 결과: [11, 33, 55]
    > s[0:1:3] 결과: [11]
    > s[-3] 결과: 33
    > s[-3:-1] 결과: [33, 44]
    > s[1:-1] 결과: [22, 33, 44]

* 문자열 메소드, 반복문, 조건문 활용한 프로그래밍

```python
# 예시1 - 회문(팰린드롬)

def ispalindrome(s):
    return_numbers = []
    for char in s:
      if char.isalnum():
        return_numbers.append(char.lower())
      
    while len(return_numbers) > 1:
      if return_numbers.pop(0) != return_numbers.pop():
        return False

    return True

test_string = input()
print(ispalindrome(test_string))
```
    > 10
    > False

```python
# 예시2 - 문자열 뒤집기(반복문과 조건문, 대입개념 활용)

def reverse_string(strtest):
  left, right = 0, len(strtest) - 1
  while left < right:
    strtest[left], strtest[right] = strtest[right], strtest[left]
    left += 1
    right -= 1

  return strtest

strtest =['a','b','c','d']
print(reverse_string(strtest))
print(strtest) # 위의 print 결과와 비교해보자.
```
    > ['d', 'c', 'b', 'a']
    > ['d', 'c', 'b', 'a']

```python
# 예시3 - 문자열 뒤집기(리스트에서 제공하는 메소드 사용)
strtest2 =['a','b','c','d']
strtest2.reverse()

# 리스트 메소드를 사용하면 특정값을 반환하는 것이 아니라, 문자열을 뒤집어주는 기능만 한다.
# 그래서 기능을 print를 해보면 함수에 대한 print를 하기 때문에 None이 출력된다.
# print(strtest2.reverse())
print(strtest2) 
```
    > ['d', 'c', 'b', 'a']

```python
# 예시4 - 문자열 뒤집기(리스트에서 제공하는 메소드가 아닌, 파이썬의 내장함수 활용)
strtest3 =['a','b','c','d']
tuple_test =('a','b','c','d')

print(strtest3) 
print(list(reversed(strtest3)))
print(tuple(reversed(strtest3)))
print(strtest3)
```
    > ['a', 'b', 'c', 'd']
    > ['d', 'c', 'b', 'a']
    > ('d', 'c', 'b', 'a')
    > ['a', 'b', 'c', 'd']

 ## 2. 자료구조와 효율성
#### 3-1) 자료구조와 효율성
* 복잡성
* Big O 표기법
* 알고리즘의 성능 분류

#### 3-2) 알고리즘
* 컴퓨터에 지시하는 처리 절차
* 그 처리의 대상이 되는 것이 **데이터**다.
* 데이터의 처리를 실시하는 가장 기본적인 구조가 **변수**임
* 데이터가 **메모리**에 저장되어 사용됨
  * 데이터 입력/ 가공/ 출력
  * &rArr; 과정을 거치는 동안 데이터는 메모리라는 장치에 저장됨
  * 컴퓨터는 알고리즘에서의 처리 명령에 따라 메모리에서 데이터를 꺼내, 가공한 후 메모리에 저장하는 작업을 반복함.
* 변수에는 한계가 있다.(리스트, 튜플, 딕셔너리, 문자열이 없다고 가정했을 때)
  * 1개의 변수에는 데이터 각 1개씩만 넣을 수 있어짐.
  * 이때 변수의 한계를 넘어서기위해 만들어진게 **배열**임
* 배열의 구조

#### 3-3) Big O 표기법(notation)
* 빅오표기법을 확용해서 알고리즘 효율을 확인가능
  * 코드 결과를 출력하기 위해 연산 반복 횟수에 따라 효율성을 확인함
* 데이터 입력값 크기에 따라 알고리즘 실행 속도의 변화를 설명하는 방법임

* 입력값 증가에 중점을 두고 대비해서 실행시간이 얼마나 길어지는지 설명함.
  * 빅오표기법만으로 성능 예측은 할 수 없음
    * 실제 성능과 같을 수 없음.
* 알고리즘 계산 복잡도 종류
  * 시간복잡도/ 공간복잡도
* 복잡도
  * 시간복잡도 (주로 )
    * 얼마나 빠르게 실행되는지
  * 공간복잡도
    * 얼마나 많은 저장공간이 필요한지
  * 좋은알고리즘: 실행 시간이 짧고 저장공간도 적게쓰는 알고리즘
  * 둘다 만족 가능한가?
    * 통상 둘 다 만족시키기 어려움
    * 시간과 공간은 반비례적인 경향이 있음
    * 취사 선태
      * 보편적으로 시간복잡도 우선시해서 프로그램 작성
      * 컴퓨터 성능 발달 메모리의 여유 공간이 아주 충분해지면서 공간복잡도 중요성이 낮아짐
      * 알고리즘 시간복잡도 중심
 * 시간복잡도
   * 빠르고 느린지는 시간보다는 단계가 얼마나 있는지, 단계를 더 적게 만들어서 복잡도를 줄여 성능을 높이는 것을 목표로 함
   * 동일한 결과를 내는데 1개의 스텝이 필요한 코드 10개 스텝이 필요한 코드 중에 1개가 더 유리함
   * 데이터 양이 많을 경우 빠른 속도를 내는게 중요!
  
* Big O run times 비교
  * Constant_상수 O(1):
    * 입력값에 영향을 받지 않는 이상적인 방법
  * Logarithmic_로그 O(log n):
    * 입력값이 증가하면 실행시간은 약간 느려짐
  * Linear_입력값 O(n):
    * 입력값이 증가하면 동일한 속도로 실행시간 증가
  * Polynomial_다항식 O(n^c):
    * 입력값이 증가하면 더 빠른 속도로 실행시간 증가, 여기서부터 비효율적
  * Exponential_지수제곱 O(c^n):
    * 다항식보다 비효율적
  * Factorial O(n!):
    * 최대비효율. 비추천

```python
입력값(n)이 10인 경우

log(10) = 1           
10 = 10               
10log(10) = 10
10^2 = 100           
2^10 = 1024              
10! = 3628800  
```
* 파이썬 내장함수 시간복잡도
  * Index: n번째 요소에 접근
    * 코드 ex) list[i]
    * 복잡도: O(1)
  * Store: N번째 요소에 값 할당
    * ex) list[i] = 0
    * O(1)
  * Length: 리스트의 길이 반환
    * ex) len(list)
    * O(1)
  * Append: 리스트 마지막에 요소추가
    * ex) list.append(5) 
    * O(1)
  * Clear: 리스트값 초기화
    * ex) list.clear()
    * O(1)
    * L = [] 과 동일
  * Pop: 리스트 특정 요소 제거
    * ex) list.pop(Number)
    * O(N)
    * O(N-Number)
  * Slice: 리스트 요소의 일부분 활용
    * list[1:10]
    * O(10-1)
    * 복사되는 요소의 개수에 비례함
  * Sort: 리스트 정렬
    * list.sort()
    * O(NlogN)

* Contanst Time(상수시간) : O(1)

```python
def print_one_item(items):
    print(items[1])       # 상수시간(단순하게 하나의 출력)

print_one_item([0,1,2])
```
    > 1

* Linear Time(선형시간) : O(n)

```python
def print_every_item(items):
    for item in items:  # 하나의 반복문
        print(item)

print_every_item([0,1,2])
```
    > 0
    > 1
    > 2

* Quadratic Time(제곱시간) : O(n^2)

```python
def print_pairs(items):
    for item_one in items:      # 중첩반복문
        for item_two in items:
            print(item_one, item_two)

print_pairs([0,1,2])
```
    > 0 0
    > 0 1
    > 0 2
    > 1 0
    > 1 1
    > 1 2
    > 2 0
    > 2 1
    > 2 2

```python
def time_test(items):
    last_idx = len(items) - 1
    print(items[last_idx])      # 상수시간

    middle_idx = len(items) / 2
    idx = 0
    while idx < middle_idx:     # 반복문1
        print(items[idx])
        idx = idx + 1

    for num in range(2000):     # 반복문2
        print(num)

time_test([0,1,2])
```
    > 
    > 2
    > 0
    > 1
    > 0
    > 1
    > 2
    > 3
    > 4
    ...
    > 1998
    > 1999
&rArr; 선형 시간이 상수 시간보다 우선시 되므로 상수시간은 무시되고, 반복문이 독립적으로(중첩반복문이 아니다.) 수행되기 때문에 위 코드에 대한 런타임은 선형 시간(linear time) O (n)이 된다.

* Big O worst-case(최악의 경우)
  * 아래와 같은 경우는 두 가지로 나눠질 수 있다.
  * 처음에 있는 첫번째 아이템을 바로 찾는 경우는 O(1)로 끝난다.(반복없이 바로 결과반환)
  * 하지만 최악의 경우에는 마지막 아이템을 찾게 되므로, O(n)이 된다.(반복문을 통해 마지막 아이템을 찾을 때까지 검색하므로.)
  
```python
def search_thing(items, thing):
    for item in items:
        if item == thing:
            return True

    return False

search_thing([0,1,2],3)
```
    > False

```python
def test(n):
    i = 1
    while i < n:
        print(i)
        i *= 2

test(3)
```
    > 1
    > 2
* 위의 코드는 while의 반복수에 따라 달라지므로 O(1)이 될 수 없다.

* 출력값이 되는 i, 반복수행되는 횟수이자 입력값인 n이 동일한 횟수로 증가하지 않으므로 위의 시간은?
  * 위의 값에 대해서는 입력값과 출력값이 동일하지 않으므로 선형시간(O(n))이 될 수는 없다.
  * 입력값인 n에 따라 출력값인 i의 증가율이 동일하지 않기 때문에 로그 시간으로 측정된다. (O(logn))

```python
# 아래 코드에 대해 삽입정렬을 수행하는 경우 코드 실행시간은 어떻게 될까?

def example_sort(array_test):
  array_len = len(array_test)
  print('array_len:', array_len)

  array_test.append(5) # [3, 1, 7, 5]
  array_test.extend([2,9]) # [3, 1, 7, 5, 2, 9]
  array_test.pop() # [3, 1, 7, 5, 2]
  print('array_test:', array_test)
  print('array_len:', len(array_test))

  for i in range(1, array_len): # i: 1, 2, 3, 4
    # 한 번 수행되고 더 이상 반복되지 않는 반복문이다.
    for j in range(i, 0, -1):
      if array_test[j] < array_test[j-1]:
        print(i, j)
      else:
          break

test = [3,1,7]
example_sort(test)
```
    > array_len: 3
    > array_test: [3, 1, 7, 5, 2]
    > array_len: 5
    > 1 1
* 위의 코드에서 range는 필요한 정수들에 대해서만 반복자를 반환한다. j 때문에 반복문이 2개 있더라도 반환하는 경우가 1번이기 때문에 O(n) 시간이 소요된다.

* 정리

  * 시간복잡도를 확인할 때 우선적으로 고려할 것은 반복문으로서, 반복문이 한 번 수행되면 O(n)이 될 수 있고, 반복문이 중첩해서 2개가 수행되면 O(n^2)이 될 수 있다.
  * 단, 입력출력값 로직에 따라 달라질 수 있다.
