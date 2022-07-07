---
title: '파이썬 with OOP(Object-Oriented Programming)'
use_math: true
categories:
  - pythonps
---

* OOP(객체 지향 프로그램) 기본개념
* 프로그래밍 패러다임의 특징
* 클래스 설계

### 클래스의 정의 (1) 파이썬의 자료형은 하나의 '**클래스**'입니다.
* 파이썬 자료형, 어떤특징?
  * 해당 자료형이 무엇인지에 따라 할 수 있는 것이 결정됨
  * 예를 들어 a.split()은 문자열 자료형에 쓸 수있음
### 클래스의 정의 (2) 구조, 용어 정리
* 상속
* __int__
* 포함
* 클래스
  * 반복되는 불필요한 소스코드를 최소화하면서 현실 세계의 사물을 컴퓨터 프로그래밍 상에서 쉽게 표현할 수 있도록 해주는 프로그래밍 기술
  * 이점??
    * 변수, 자료형, 제어문, 함수
    * 프로그램 개발, 유지보수 간편 >> 대규모 프로그램 개발
  * 상속 기능을 이용가능
    * 상속
      * 재산 물려받기
      * 앞에꺼 끌어다가 활용하기
      * 이전 내용 활용하기
        * 클래스들끼리 기능을 물려주는것
        * 부모클래스 --(기능)-->자식클래스
        * 상속을 받으면 부모의 기능을 자식 클래스에 코딩안해도됨
        * 기본 card 클래스 (카드의 주요기능)-->
          * 영화할인 카드 클래스
          * 마트할인 카드 클래스
* 객체
  * 객체는 속성(상태, 특징)과 행위(행동, 동작, 기능)로 구성된 대상을 의미
  * 객체는 자동차나 로봇같은 사물일 수도 있고 사람이나 동물일 수도 있으며 어떤 개념일 수도 있음
  * 프로그래밍 언어에서 객체를 만들 때는 주로 현실 세계를 반영해서 만듦
  * 객체의 특징인 속성은 변수로, 객체가 할 수 있는 일인 행동은 함수로 구현함
  * 객체는 변수와 함수의 묶음이다.
  * 객체가 사람이라면 이름, 키, 몸무게 같은 속성은 변수로 구현하고 걷거나 뛰거나 앉는 행동은 함수로 구현함. 객체가 자전거라면 바퀴의 크기, 색깔같은 속성은 변수로 구현하고 전진, 방향전환 같은 동작은 함수로 구현함니다.
  * 객체를 만들고 이용할 수 있는 기능을 제공하는 프로그래밍 언어를 객체지향프로그래밍 언어라함. 파이썬도 객체지향 언어임
  * 이러한 객체를 만들려면 먼저 클래스를 선언해야함
  * 클래스는 객체의 공통된 속성과 행위를 변수와 함수로 정의한 결과임. 다시말해 클래스는 객체를 만들기위한 기본틀이고 객체는 기본틀을 바탕으로 만들어진 결과임
  * 객체는 클래스에서 생성하므로 객체를 클래스의 인스턴스라함
* 객체지향
  * 어떤 프로그래밍 방식(방법론) > 재사용하려고(더 쉽게 더 잘하기위해) 
* 다변성
* 추상화
  
### 클래스 구조

```python
# 클래스 선언
class 클래스명():
    실행코드
    # self: 객체 생성한 후에 자신을 참조하는데 이용됨
    def 함수명(self):
        실행코드

# 객체 선언
객체명 = 클래스명()

# 객체의 메소드 호출
객체명, 메소드명()
```
* 객체 초기화

&rarr;
&rArr;


### 클래스의 정의 (3) 클래스에서 사용하는 변수
* 클래스에 사용하는 변수는 위치에 따라 2개로 나뉨
  * 클래스 변수
    * 클래스 내에 있지만 함수 밖에서 '변수명=데이터' 형식으로 정의한 변수로서 클래스에서 생성한 모든 객체가 공통으로 사용될 수 있다. 
  * 인스턴스 변수
    * 클래스 내의 함수 안에서 self.변수명=데이터 형식으로 정의한 변수로서 클래스 내의 모든 함수에서 self.변수명으로 접근할 수 있음.

```python
#클래스명 card를 통해 my_card_1, my_card_2, my_card_3을 만들고,
# 3개의 카드의 balance가 모두 10000으로 출력되게 만들어보시오.

# 클래스 선언
class Card():
    def __init__(self):
        self.balance = 10000

# 객체 3개 선언
my_card_1 = Card()
my_card_2 = Card()
my_card_3 = Card()

# 객체에 속성값을 가져와서 출력
print(my_card_1.balance)
print(my_card_2.balance)
print(my_card_3.balance)
```
```python
# 아래의 코드를 활용하여 총 발급된 카드 수가 3이 나오도록 코드를 수정해보시오!

# 클래스 선언
class Card():
    issued_card_count = 0
    def __init__(self):
        self.balance = 10000
        Card.issued_card_count += 1

# 선언된 클래스로부터 객체를 생성
my_card_1 = Card()
my_card_2 = Card()
my_card_3 = Card()


print('총 발급된 카드 수: ', Card.issued_card_count)
```


## 1. OOP(Object-Oriented Programming) 기본

* OOP의 기본 전제는 기능(함수, 변수) 재사용이 가능하도록 설계 및 프로그래밍하는 것이다.

```python
# 인트로 코딩

# 난수 다루기(1~100 사이 정수형 난수를 구하자.)
# 정수를 입력받고, 입력숫자가 출력될 때까지 입력숫자만큼 반복하여 난수를 출력하고 1개의 종료메시지를 띄우시오.

import random

input_num = int(input())

for i in range(input_num):
  ran_num = random.randint(1,100)
  print(ran_num, end = ' ')

  if ran_num == input_num:
    print("input random number print")
    continue

else:
  print('exit')
```
    > 5
    > 39 44 11 66 67 exit

* 기본개념: 설계(사람이 이해하는 방식)와 구현할 소스코드(컴퓨터가 이해하는 방식) 간의 상호이해가 중요하다.
  * HW&SW 성능증가(CPU성능 증가, 소프트웨어 다중실행) 덕분에 OOP의 모든 기능을 활용할 필요는 없다.

    * OOP의 개념을 무분별하게 활용하면 유지보수가 어려워질 수도 있기때문에 설계방향 및 서비스기능에 따라 사용해야 한다.
* OOP의 어려운 점 :

  * OOP는 하나의 패러다임일 뿐이기 때문에 기존의 프로그래밍 패러다임(Procedural Programming, Functional Programming, ...)들과 우열을 가릴 필요는 없다.

  * OOP는 주관성이 높으므로, 보편적으로 활용되는 개념에 대해 배운다.(주관성이 높다는 뜻은 소프트웨어 서비스 설계방향에 영향을 많이 받는다.)

  * OOP를 제대로 하는 법은 프로그래밍뿐만 아니라 다양한 도메인에서 재사용 가능한 클래스, 메소드(기능) 설계가 중요하다.
* OOP 나오기 이전의 방식
  * OOP 개념이 나오기 전에는, 배열과 함수, 변수를 많이 생성하고 활용하여 최대한 많은 기능을 적은 양의 소스코드파일에 담았다.

  * 속성과 기능이 증가할 때마다 배열과 함수를 계속 생성해야했기 때문에 소스코드를 관리하는데 있어서 비효율이 발견되었다.

  * 이에 따라 속성과 기능을 object라는 최소단위로 분리하는 OOP의 개념이 나오기 시작했다.

  * 프로그래밍에서 OOP의 개념을 항상 활용하지는 않는다. (데이터 분석을 진행하는 경우, 모듈과 라이브러리를 활용한 분석 인사이트가 중요하다.)

* OOP의 필요성
  * data-driven(데이터기반 의사결정), 컴퓨터하드웨어성능, 데이터양 증가에 따라 OOP활용도 증가하였다.

    * 프로그래밍 패러다임 : OOP와 Procedural Programming, functional Programming에 대해 알아본다.

    * 함수형은 함수의 사용을 극대화시켜서 코드의 가독성을 높여주는 형태이다. 프로그래밍 코드를 특정 상황에 특정 함수를 사용하기위해 고안된 방법이다.

    * 특정 컴퓨터환경과 특정 대용량 개발환경에서 많이 쓰이고 있지만 절대적으로 좋은 프로그래밍은 아니다.

* OOP와 일상생활

  * 일상 생활에서 볼 수 있는 것, 실제로 머릿속에서 떠올릴 수 있는 것을 프로그래밍하는 것이 OOP의 중요한 점이다.

  * 기능별로 개체가 효율적으로(재사용가능하도록) 분리되어야 한다. 그래서 설계가 중요하다.
  
  * 위의 두 개의 프로그래밍에 대한 내용을 파이썬 코드로 작성한다.

```python
# 절차 프로그래밍(Procedural Programming, 일명 PP)
# 조건 또는 기능이 증가할 때마다 함수와 변수 같은 요소가 계속 증가할 수 있으므로 비효율적이다.

# 케이스 1 : 함수활용
def carAttribute():
  speed = 50
  color = 'black'
  model = 'CarModel'
  return speed,color,model

# return값을 통해 함수 요소값을 확인할 수 있다.
print("Car Attribute: ", carAttribute())

# 케이스 2 : 변수활용
speed = 50
color = 'black'
model = 'CarModel'

# 해당 변수를 각각 명시해주어야 한다.
print("Car Attribute: ", speed,color,model)
```
    > Car Attribute:  (50, 'black', 'CarModel')
    > Car Attribute:  50 black CarModel
```python
# OOP / 기능에 따라 Car클래스 안에 있는 함수와 변수만 추가해주면 된다.
# 아래와 같이 클래스 선언 순서에 관계없이 실행된다.
# 절차 프로그래밍과 다르게 기능별로 수행되기 때문이다.
class Bus:
  def __init__(self, speed, color):
      self.speed = speed
      self.color = color
  
  def drive_bus(self):
    self.speed = 70

class Car:
  def __init__(self, speed, color, model):
    self.speed = speed
    self.color = color
    self.model = model
  
  def drive(self):
    self.speed = 50
  
myCar = Car(0, "green", "testCar")
print("--------Car Object Create Complete--------")
print("Car Speed: ", myCar.speed)
print("Car Color: ", myCar.color)
print("Car Model: ", myCar.model)
print("Bus color: ", myBus.color)

myBus = Bus(0, 'black')
print("--------Bus Object Create Complete--------")
print("Bus color: ", myBus.color)


# 운전 중이 아니므로 speed는 0을 출력한다.
print("--------Car/Bus Speed 1--------")
print("Car Speed by drive: ", myCar.speed)
print("Bus Speed by drive: ", myBus.speed)

# Car/Bus object method Call
myCar.drive()
myBus.drive_bus()

# 각각의 개체가 각자의 속도로 움직이고 있다.
print("--------Car/Bus Speed 2--------")
print("Car Speed by drive: ", myCar.speed)
print("Bus Speed by drive: ", myBus.speed)
```
    > --------Car Object Create Complete--------
    > Car Speed:  0
    > Car Color:  green
    > Car Model:  testCar
    > Traceback (most recent call last):
    >   File "c:\Users\choidb\Desktop\practice.py", line 26, in <module>
    >     print("Bus color: ", myBus.color)
    > NameError: name 'myBus' is not defined

## 2. OOP 구성
### 캡슐화
* 캡슐화 기본개념 : 내부 속성(변수)과 함수를 하나로 묶어서 클래스로 선언하는 일반적인 개념

  * 캡슐화형태로 코드를 작성하지 않으면 특정 기능(함수, 변수)에 직접 접근하게 되는 상황이 된다.

  * 기능이 많아질수록 재사용의 개념을 활용하기가 어려움

  * 해당 접근제어 관련해서는 아래 콘텐츠 파이썬 활용 및 OOP에서 추가적으로 다룹니다.

```python
# 캡슐화코드

class Encap:
  def __init__(self,value):
    self.value = value
    print('init :', self.value)

  def _set(self):
    print('set :', self.value)

  def printTest(self):
    print('printTest :', self.value)

  # def __printTest2(self):
  #   print('printTest :', self.value)

# object 생성
e = Encap(10)

# object 실행 
# 케이스1
e.__init__(20)
e._set()
e.printTest()
#e.__printTest2()


print('\n')

# 케이스2
e.__init__(30)
e._set()
e.printTest()
```
    > init : 10
    > init : 20
    > set : 20
    > printTest : 20


    > init : 30
    > set : 30
    > printTest : 30

### 상속과 포함(Inheritance & Composition)
* object의 종류는 현실 세계에 있는 대부분이기 때문에, 설계될 수 있는 다양한 object가 있다.
* 상속(Inheritance)
  * "개는 동물이다." 또는 "선생님은 직장인이다."라는 관계로서 설명된다.

  * 기본개념 : 상위 클래스의 모든 기능(함수, 변수)을 재사용할 수 있다.

* 포함(Composition)

  * "개는 몸을 갖고 있다." 라는 관계로서 설명된다.

  * 기본개념 : 다른 클래스의 일부 기능(함수)만을 재사용한다.

```python
# 상속코드

# 클래스 선언
class Person:
    def __init__(self, name):
        self.name = name
        
class Student(Person):      # Person 클래스 상속받음(name 변수를 파라미터로 재사용)
    def study(self):
        print (self.name + " studies hard")

class Employee(Person):     # Person 클래스 상속받음(name 변수를 파라미터로 재사용)
    def work(self):
        print (self.name + " works hard")

# object 생성
s = Student("Dave")
e = Employee("David")

# object 실행
s.study()
e.work()
```
    > Dave studies hard
    > David works hard

```python
# 포함코드

# 클래스 선언
class Person:
    def __init__(self, name, age):
        self.name = name
        self.age = age

    def printPerson(self):
        print('Person_printPerson')

class Student(Person):
    def __init__(self, name, age, id):
        Person.__init__(self, name, age)
        Person.printPerson(self)
        self.id = id

    def test(self, score):
        if score > 80:
            print (self.name + " studies hard")
        else:
            print (self.name + " needs supplementary lessons")


# object 생성
# 한 번 생성된 object는 파라미터가 변하지 않는 이상 출력값 또한 변하지 않는다.
s = Student("Dave", 20, 1)

# object 실행
print("s.age:", s.name)   # result : Dave
print("s.age:", s.age)   # result : 20
print("s.id:", s.id)   # result : 1
print('\n')

# 객체 하나 더 생성하기
s2 = Student("Jamie", 25, 2)
print("s2.age:", s2.name)   # result : Jamie
print("s2.age:", s2.age)   # result : 25
print("s2.id:", s2.id)   # result : 2
print('\n')

# 점수입력
print('-- test score result --')
s.test(52)
s2.test(88)
```
    > Person_printPerson
    > s.age: Dave
    > s.age: 20
    > s.id: 1


    > Person_printPerson
    > s2.age: Jamie
    > s2.age: 25
    > s2.id: 2


    > -- test score result --
    > Dave needs supplementary lessons
    > Jamie studies hard

```python
# 포함코드

# 클래스 선언
class Bill():
    def __init__(self, description):
        self.description = description


class Tail():
    def __init__(self, length):
        self.length = length


class Duck():
    def __init__(self, bill, tail):
        self.bill = bill
        self.tail = tail

    def about(self):
        print(
            f"This duck has a {self.bill.description} and a {self.tail.length}.")

# object 생성
duck = Duck(Bill('bill object'), Tail('tail object'))

# object 실행
duck.about()
```
    > This duck has a bill object and a tail object.

### 추상화
* 기본개념: 추상화(abstraction)는 복잡한 내용에서 핵심적인 개념 및 기능을 요약하는 것을 말한다.

  * object의 기능에 따라 추상클래스(상위클래스)를 상속받아 개별적으로 클래스(하위클래스)를 생성한다.

  * 기본적으로 추상메소드를 선언하며 실제 실행되는 기능은 보여지지 않는다.

  * 실제 실행되는 기능은 선언된 추상클래스를 상속받은 다른 클래스의 메소드에서 확인할 수 있다.

  * 추상클래스를 사용하는 이유

    * 클래스 또는 함수가 예상했던 것 이상으로 많이 생성되는 경우 추상클래스를 생성하여 핵심적인 기능만 생성해놓는다.
    * 실제로 동작기능은 추상클래스에서 상속받은 하위클래스의 메소드에서 진행된다.
    * 추상클래스의 추상메소드를 활용할 때 장점은 추상클래스를 중심으로 하위클래스의 메소드를 다양하게 생성할 수 있기 때문에, 유지보수를 진행하는 경우 추상클래스만 수정하면 되므로 복잡성을 낮출 수 있다.

```python
# 추상화 코드

from abc import ABCMeta, abstractmethod # abc : abstract base class

# 추상 클래스
class People(metaclass=ABCMeta):  

# 추상 메소드
    @abstractmethod # 추상 메소드에는 @abstractmethod를 선언해줘야 함
    def charecter(self): 
        pass        # 추상 메소드는 기능 내 실제 실행내용은 없다.

# 상속받는 클래스
class Student(People):
    def charecter(self, pow, think):
        self.pow = pow
        self.think = think

        print('체력: {0}'.format(self.pow))
        print('생각: {0}'.format(self.think))

# 상속받는 클래스
class Driver(People):
    def charecter(self, pow, think):
        self.pow = pow
        self.think = think

        print('체력: {0}'.format(self.pow))
        print('생각: {0}'.format(self.think))

# Student object 생성      
peo1 = Student()
print('Student : ')

# Student object 실행
peo1.charecter(30, 10)

print()

# Driver object 생성
peo2 = Driver()
print('Driver : ')

# Driver object 실행
peo2.charecter(10, 10)
```
    > Student : 
    > 체력: 30
    > 생각: 10

    > Driver :
    > 체력: 10
    > 생각: 10

### 다형성
* 다형성: 같은 종의 생물이지만, 모습이나 고유한 특징이 다양한 성질을 말한다.
* OOP에서 다형성은 계층 구조의 상속 관계에서 상속받은 기능 외, 다른 기능을 추가적으로 제공하고자 할 때 사용한다.
  * 장점
    * 프로그램 작성 코드량을 줄여준다.(다형성을 잘 쓰면 if/else 문을 많이 줄일 수 있음)
    * 코드의 가독성을 높혀줌

```python
class Slimes:
    def __init__(self):
        self.hp = 100
        self.attack_power = 50
    def get_damage(self):
        self.hp -= self.attack_power
        if self.hp <= 0:
            self.hp = 0
            print('Slime is dead!!!')

class Slime_Yellow(Slimes):
    pass

class Slime_Blue(Slimes):
    def __init__(self):
        super().__init__()
        self.attack_power = int(self.attack_power * 0.8)
    def get_damage(self):
        self.hp -= self.attack_power
        if self.hp <= 0:
            self.hp = 0
            print('Blue Slime is dead!!! You get 100 Gold')


class Slime_Purple(Slimes):
    def __init__(self):
        super().__init__()
        self.attack_power = int(self.attack_power * 0.5)
    def get_damage(self):
        self.hp -= self.attack_power
        if self.hp <= 0:
            self.hp = 0
            print('Purple Slime is dead!!!, You get 300 Gold')


Slime_1 = Slime_Yellow()
# 슬라임 제거하기: hp=0 만들기
print(Slime_1.hp)
Slime_1.get_damage()
print('Slime_1 hp:', Slime_1.hp)
Slime_1.get_damage()
print('Slime_1 hp:',Slime_1.hp)
```
    > 100
    > Slime_1 hp: 50
    > Slime is dead!!!
    > Slime_1 hp: 0
    > Slime_2 hp: 60
    > Slime_2 hp: 20
    > Blue Slime is dead!!! You get 100 Gold
    > Slime_2 hp: 0
    > Slime_3 hp: 75
    > Slime_3 hp: 50
    > Slime_3 hp: 25
    > Purple Slime is dead!!!, You get 300 Gold
    > Slime_3 hp: 0
    > Purple Slime is dead!!!, You get 300 Gold
    > Slime_4 hp: 0
    > Purple Slime is dead!!!, You get 300 Gold

```python
# 오해하지 않도록 코드를 작성하자.
# foo: 프로그래밍 상에서 임시로 변수이름을 지정해줘야 할 때 주로 쓰이는 변수 이름이다.
foo = ''

# 가독성 좋음
if foo is not None: # 한 번만 해석하면 된다. (A는 B가 아니다.)
  print('가독성 좋음')

# 가독성 좋지 않음
if not foo is None: # 두 번 해석해야된다. (A가 아닌 것은 None이다.)
  print('가독성 좋지 않음')
```
    > 가독성 좋음
    > 가독성 좋지 않음

## 3. 프로그래밍을 위한 설계
### 1) 클래스 설계(코드 재사용성)
* 코드 설계 전 그림과 글로 코드블록을 구성해 볼것.
* 1단계
  * 코드 설계 시 사용할 object부터 적기
    * Users
      * Customers
      * Vendors
      * Admin
    * Products
    * Purchases

* 2단계
  * 코드 작성 전, 각 object별로 요구되는 속성과 어떤 기능을 위해 생성되었는지 설계한다.
    * Users
      * Attributes(속성)
        * 이름
        * 사용자가 관리자인지?
      * Customers
        * Attributes
          * 이름
          * 구매목록
      * Vendors
        * Attributes
          * 이름
          * 상품목록
      * Admin
        * 이름
        * 사용자가 관리자임을 나타내는 구분값
    * Products
      * Attributes
        * 이름
        * 가격
        * 공급업체
    * Purchases
      * Attributes
        * 제품
        * 고객
        * 가격
        * 구매완료기간
* object간 관계에 대해 생각해본다.
  * 판매자는 1개 이상의 제품을 갖고 있다.
  * 고객은 1개 이상의 구매를 한다.
  * 구매는 1개 이상의 제품을 구매하는 것이다.

```python
# 기본이 될 수 있는 User 클래스 생성

class User:
    def __init__(self, name, is_admin=False):
        self.name = name
        self.is_admin = is_admin
```
```python
# User로부터 상속받는 3개의 클래스를 정의
"""
부모 클래스에서 정의한 함수와 변수는 자식 클래스에서 정의한 것처럼 사용할 수 있습니다.

부모 클래스에서 정의한 함수와 자식 클래스에서 정의한 함수 이름이 같은 경우,
부모 클래스의 함수를 호출하려면 두 가지 방법 중 하나를 사용해야 합니다.
1) 부모클래스명.함수명()
2) super().함수명()

즉, super()는 자식클래스에서 부모클래스에 있는 함수를 사용하고 싶고,
플러스 해당 함수명이 자식클래스에 중복되어 있을 때 사용할 수 있는 코드입니다.
"""

class User:
    def __init__(self, name, is_admin=False):
        self.name = name
        self.is_admin = is_admin

class Admin(User):
    def __init__(self, name):
        super().__init__(name, is_admin=True)

# 부모 클래스(User)로부터 상속을 받으려면 클래스를 선언할 때,
# 클래스 이름 다음에 있는 소괄호 안에 부모 클래스의 이름을 넣어주면 됩니다.
class Customer(User):
    def __init__(self, name):
        super().__init__(name)
        self.purchases = []

class Vendor(User):
    def __init__(self, name):
        super().__init__(name)
        self.products = []
```
```python
# 위의 코드에서 제품(Product)과 구매(Purchase) 클래스 생성 코드 추가

from datetime import datetime

class User:
    def __init__(self, name, is_admin=False):
        self.name = name
        self.is_admin = is_admin

class Admin(User):
    def __init__(self, name):
        super().__init__(name, is_admin=True)

class Customer(User):
    def __init__(self, name):
        super().__init__(name)
        self.purchases = []

class Vendor(User):
    def __init__(self, name):
        super().__init__(name)
        self.products = []

class Product:
    def __init__(self, name, price, vendor):
        self.name = name
        self.price = price
        self.vendor = vendor

class Purchase:
    def __init__(self, product, customer):
        self.product = product
        self.customer = customer
        self.purchase_price = product.price
        self.purchase_data = datetime.now()
```
```python
"""
현재 생성된 클래스: User(Admin, Customer, Vendor), Product, Purchase

1) 고객(Customer): 제품(Product)을 구매(Purchase)하는 행동
   => Customer 클래스에 purchase_product 메소드 추가

2) 공급업체(Vendor): 제품(Product)을 생산(Product)하는 행동
   => Vendor 클래스에 create_product 메소드 추가
"""

from datetime import datetime

class User:
    def __init__(self, name, is_admin=False):
        self.name = name
        self.is_admin = is_admin

class Admin(User):
    def __init__(self, name):
        super().__init__(name, is_admin=True)

class Customer(User):
    def __init__(self, name):
        super().__init__(name)
        self.purchases = []
    # 함수 추가
    def purchase_product(self, product):
        purchase = Purchase(product, self)
        self.purchases.append(purchase)

class Vendor(User):
    def __init__(self, name):
        super().__init__(name)
        self.products = []
    # 함수 추가
    def create_product(self, product_name, product_price):
        product = Product(product_name, product_price, self)
        self.products.append(product)

# 모델링을 위한 추가 소스코드
class Product:
    def __init__(self, name, price, vendor):
        self.name = name
        self.price = price
        self.vendor = vendor

class Purchase:
    def __init__(self, product, customer):
        self.product = product
        self.customer = customer
        self.purchase_price = product.price
        self.purchase_data = datetime.now()
```
### 2) 모듈
* 모듈: 파이썬에서 코드가 저장된 파일
  * 유지보수가 쉬운 프로그램 작성 가능
  * 파이썬 파일을 다른 코드 파일에서도 해당 파일의 변수, 함수, 클래스를 불러와 사용가능
* 모듈 불러오기 방법 Preview
  * import 모듈명
  * from 모듈명 import 변수/함수/클래스명
  * from 모듈명 import *

```python
# test 폴더에 my_function.py 으로 저장
def my_divide():
    try:
        x = input('분자의 숫자를 입력하세요 ~ ')
        y = input('분모의 숫자를 입력하세요 ~ ')
        return int(x)/int(y)
    except:
        return '나누기를 할 수 없습니다'

writer = 'Lion'
```
```python
# test 폴더에 test_function.py 로 저장 후에 해당 코드를 실행해보시오.
import my_function

print(my_function.my_divide())
```
* import 모듈명 을 사용할 때에는 모듈 내에 사용할 내용들을 모듈명.변수, 모듈명.함수(), 모듈명.클래스() 형태로 불러와서 사용한다.
* 아래와 같이 모듈명은 별명을 사용할 수 있다.
```python
# test/test_function.py 로 저장 후에 해당 코드를 실행해보시오.
import my_function as mf

print(mf.my_divide())
```
* 위 코드는 from 모듈명 import 함수명 형태로 사용할 수있다.
```python
# test/test_function.py 로 저장 후에 해당 코드를 실행해보시오.
from my_function import my_divide

print(my_divide())
```
* 위 형태로 변수, 함수, 클래스 를 불러오면 모듈명. 없이 바로 변수/함수/클래스를 사용할 수 있다.
* 또한 불러온 변수/함수/클래스 명도 별명을 붙여서 사용할 수 있다.

```python
# test/test_function.py 로 저장 후에 해당 코드를 실행해보시오.
from my_function import my_divide as md

print(md())
```
* 모듈 내의 모든 변수, 함수, 클래스를 사용하고자 할 때는 아래 코드와 같이 from 모듈명 import * 를 사용한다.

```python
# test/test_function.py 로 저장 후에 해당 코드를 실행해보시오.
from my_function import *

print(my_divide())
print('writer:', writer)
```
### 3) 클래스의 인스턴스화
* 클래스를 생성했으면, 그것을 활용하기 위한 인스턴스화가 필요하다.

    * object가 생성된 이후, object가 소프트웨어의 메모리할당이 되면 인스턴스가 되는 것이다.
      * object는 인스턴스를 포함할 수 있으며, 포괄적 의미를 갖는다.
      * object는 프로그래밍 전체에서 쓰이는 포괄적인 의미를 갖으므로 인스턴스와 비교하면서 학습하는 대상은 아니다.

```python
# 가장 기본적인 클래스를 생성해보고 값을 확인해본다.

class MyFirstClass:
    pass

a = MyFirstClass()  # 인스턴스화(메모리할당됨)

print(a)    # 주소값은 일반적인 정수값과 다르게 나온다.
```

## 4. 파이썬 활용 및 OOP
### 1) 데이터 캡슐화와 접근제어
* 캡슐화 : object 및 소스코드 구현에 대한 상세정보를 분리하는 과정
* 캡슐화하는 이유
  * 모듈화가 가능해진다.(함수, 메소드, 클래스 등을 활용한 기능 분리.)
  * 기능이 분리되어있으니 디버깅을 하는 경우 편리하다.
  * 프로그램이 기능별로 분리되어있으니 소스코드의 목적을 알기쉽다.
  * 파이썬은 object 접근제어를 위한 접근제어자를 제공하지 않기때문에 변수, 메소드, 함수에 직접 접근할 수 있다.
    * 파이썬에서는 상단 표와 같이 직접 접근을 허용하지 않는 규칙을 만들었다.
    * Notation : 접근 정도를 나타내는 명칭이며 Private -> Protected -> Public 순서로 코드접근이 어렵다.
  * 파이썬의 변수나 함수를 감춰주는 기능으로서, 외부에서 무분별한 접근을 막기위해 위와 같은 개념이 생겨났다.
    * 외부 object가 속성이나 메소드에 대한 접근을 막기 위해 이중 밑줄 __을 접두사로 추가할 수 있다.
    * '_클래스이름__메소드이름' 형태로 이름을 변환시켜, 부모클래스와 서브클래스의 변수나 메소드이름을 구분짓는다.

```python
class Point:
   def __init__(self, x, y):
       self.x = x
       self.y = y
       self.__private_name = "private 접근"

class Point_sub(Point):
  def __init__(self,x, y):
    Point.__init__(self,x,y)
    self.x = x
    self.y = y
    
  def __sub(self):
    self.__x = 10
    self.__y = 20

  def sub(self):
    self.__sub()
    print(self.__x)
    print(self.__y)
 
my_point = Point(1, 2)
my_point_sub = Point_sub(10,20)


# case 1 - error case: private 으로 해당코드로 접근할 수 없다
# print(my_point.__private_name)

# case 2
# 클래스 생성자에 있는 private변수에 접근하기위해 '_클래스이름__private변수' 를 활용한다.
print(my_point._Point__private_name)

# case 3
print('case3 ------------')
my_point_sub.sub()    # 변환된 이름에 대해 값 출력
```
    > private 접근
    > case3 ------------
    > 10
    > 20
* 아래와 같이 클래스이름과 속성에 대해 알고 있으면, 변형된 이름을 사용해 접근가능
* 따라서, 코드상에서 접근을 강제로 막을 방법은 없다.

```python
class A(object):
  def __init__(self):
    self.__X = 3        # self._A__X 로 변환

  def __test(self):     # _A__test() 로 변환
    print('self.__X' ,self.__X)

  def bast(self):
    self.__test()

class B(A):
  def __init__(self):
    A.__init__(self)
    self.__X = 20       # self._B__X 로 변환

  def __test(self):     # _B__test() 로 변환
    print(self.__X)

  def bast(self):
    self.__test()

# 객체 생성
a = A()

# 오류 발생 코드
# a.__test()

# private 메소드 접근방법
# 1) 변형된 이름을 통해 접근가능: '_클래스이름__private메소드'
print('a ----------------------')
a._A__test()

# 2) 우회경로로 접근가능
a.bast()

# 객체 생성
b = B()

# private 메소드 접근
print('b ----------------------')
b._B__test()
b.bast()

# 오류 발생 코드
# print(a.__X)

# __X 변수 접근
print('X ----------------------')
print(a._A__X)
print(b._A__X)
print('\n')

# 상속을 받았기 때문에 B클래스의 인스턴스에서 A클래스의 함수와 변수도 확인가능하다.
# dir(객체): 파이썬 내장메소드로 해당 객체가 어떤 변수와 메소드를 가지고 있는지 나열
print('[부모클래스 A를 사용해 생성한 객체 a의 변수와 메소드]')
print(dir(a))

print('[부모클래스 B를 사용해 생성한 객체 b의 변수와 메소드]')
print(dir(b))       
```
    > a ----------------------
    > self.__X 3
    > self.__X 3
    > b ----------------------
    > 20
    > 20
    > X ----------------------
    > 3
    > 3


    > [부모클래스 A를 사용해 생성한 객체 a의 변수와 메소드]
    > ['_A__X', '_A__test', '__class__', '__delattr__', '__dict__', '__dir__', '__doc__', '__eq__', '__format__', '__ge__', '__getattribute__', '__gt__', '__hash__', '__init__', '__init_subclass__', '__le__', '__lt__', '__module__', '__ne__', '__new__', '__reduce__', '__reduce_ex__', '__repr__', '__setattr__', '__sizeof__', '__str__', '__subclasshook__', '__weakref__', 'bast']
    > [부모클래스 B를 사용해 생성한 객체 b의 변수와 메소드]
    > ['_A__X', '_A__test', '_B__X', '_B__test', '__class__', '__delattr__', '__dict__', '__dir__', '__doc__', '__eq__', '__format__', '__ge__', '__getattribute__', '__gt__', '__hash__', '__init__', '__init_subclass__', '__le__', '__lt__', '__module__', '__ne__', '__new__', '__reduce__', '__reduce_ex__', '__repr__', '__setattr__', '__sizeof__', '__str__', '__subclasshook__', '__weakref__', 'bast']

* _와 __의 활용
* 프로그램이 길어지고 다양한 변수를 선언하는 경우 클래스의 속성이 충돌(변수의 중복)할 수 있다.

```python
# 속성충돌

class parent_class:
  def __init__(self):
    self.value = 30
    self._value = 40
    self.__value = 50

  def get(self):
    return self.value

class sub_class(parent_class):
  def __init__(self):
    super().__init__()
    self.__value = 20    # 위의 parent_class의 _value와 충돌(값의 중복)발생

s = sub_class()
print(s.value) # public
print(s._value)# protected

print('어떤 클래스에서 값을 받아오냐에 따라 값의 정보가 바뀜--')
print(s._parent_class__value)
print(s._sub_class__value)
print('parent_class value:',s.get(),' sub_class value:', s.value)
```
    > 30
    > 40
    > 어떤 클래스에서 값을 받아오냐에 따라 값의 정보가 바뀜--
    > 50
    > 20
    > parent_class value: 30  sub_class value: 30

* 위처럼 속성의 충돌(같은 값)이 발생하는 이유는 대체로 프로그램에서 중복되는 속성(attribute)을 활용하는 경우이다.

* 속성명을 다르게 해줘도 되지만 파이썬에서 활용할 수 있는 '비공개 속성' 을 활용할 수 있다.

* 비공개 속성은 위에서 설명한 '__'를 활용한다.

```python
# 속성충돌방지(언더바와 접근제어의 개념을 활용하여 같은 변수이름끼리 헷갈리지 않도록 한다.)

class parent_class:
  def __init__(self):
    self.__value = 10   # parent_class는 '__'

  def get(self):
    return self.__value # parent_class는 '__'

class sub_class(parent_class):
  def __init__(self):
    super().__init__()  # parent_class 호출을 위해 super() 사용
    self._value = 20    # sub_class는 '_'


s = sub_class()
print('parent_class value:',s.get(),' sub_class value:', s._value)
```
    > parent_class value: 10  sub_class value: 20

### 2) 메소드 오버라이딩(method overriding)

* 오버라이딩은 우선시하다라는 의미로, 상속처럼 부모클래스의 메소드를 재호출하는 것이 아니라 같은 이름의 메소드를 신규 생성하는 것이다.

* 새로운 이름의 메소드를 기능별로 만들면 되는데 부모클래스의 메소드이름을 그대로 사용하는 이유는 무엇일까?

  * 중복되는 기능(메소드)은 기존 부모클래스의 메소드(기능)로 재사용하고, 다르게 사용하려면 재정의하는 개념으로 활용할 수 있다.

    * 프로그래밍의 핵심이 되는 재사용을 위함이다.

    * 메소드 오버라이딩도 다형성 개념의 한 종류이다.

```python
class Bicycle():
     def exclaim(self):
       print("부모클래스 자전거")

class Specialized(Bicycle):            # 부모클래스를 상속받음
    def exclaim(self, specialized):    # 메소드 오버라이딩(specialized 파라미터 추가, return 추가)
         print("자식클래스 재정의:",specialized)
         return 'return 자식클래스 재정의: '+specialized


a_bike = Bicycle()
a_specialized = Specialized()

# 출력1 - 부모클래스 메소드
print('출력1:')
a_bike.exclaim()

# 출력2 - 오버라이딩된 자식클래스 메소드(파라미터 추가, return 추가)
print('출력2:')
a_specialized.exclaim('specialized test')
```
    > 출력1:
    > 부모클래스 자전거
    > 출력2:
    > 자식클래스 재정의: specialized test

```python
class Bicycle():
    def exclaim(self):  
        print("부모클래스 자전거")

class Specialized(Bicycle): # 부모클래스를 상속받음
    def exclaim(self):    # 메소드 오버라이딩
        super().exclaim() # super는 위의 부모클래스 메소드를 그대로 활용한다.
        print('super를 활용한 부모클래스의 메소드입니다.')
         


a_bike = Bicycle()
a_specialized = Specialized()

# 출력1 - 부모클래스 메소드
print('출력1:')
a_bike.exclaim()

# 출력2 - super : 부모클래스 메소드 그대로 활용
print('출력2:')
a_specialized.exclaim()
```
    > 출력1:
    > 부모클래스 자전거
    > 출력2:
    > 부모클래스 자전거
    > super를 활용한 부모클래스의 메소드입니다.

### 3) super 사용
* 아래 예시에서 Graduate(자식클래스)는 Student(부모클래스)가 가지고 있는 모든 매개변수(파라미터, arguments)를 사용한다.
  * 상속을 통한 재사용을 하는 경우, 아래와 같이 다른 매개변수(graduation_date)도 신규 생성할 수 있다.

```python
class Student:    # 부모클래스
     def __init__(self, name):
         self.name = name
         print(self.name)

class Graduate(Student):    # 부모클래스 상속받음
     def __init__(self, name, graduation_date): 
         super().__init__(name)   # super를 활용하여 부모 메소드를 호출하여 name 매개변수 재사용(super를 사용하면 부모클래스의 상속받는다는 것을 의미함)
         self.graduation_date = graduation_date

print('출력1: ', end='')
a_student = Student('stu_class')
print('출력2: ', end='')
a_graduate = Graduate('gradu_class',11)

print('출력3: ', end='')
a_student.__init__('stu')
print('출력4: ', end='')
a_graduate.__init__('gradu',11)

# graduate 인스턴스 생성
print('출력5: ', end='')
print(a_graduate.name)

print('출력6: ', end='')
print(a_graduate.graduation_date)
```
    > 출력1: stu_class
    > 출력2: gradu_class
    > 출력3: stu
    > 출력4: gradu
    > 출력5: gradu
    > 출력6: 11

```python
# range보다는 enumerate를 사용한다.
# range 내장 함수는 정수집합을 반복하는 상황에서 유용하다.

# 하지만 리스트에 대해서 특정 인덱스에 따라 반복을 하는 경우, list의 길이를 알아야하고(len함수 써야함), 
# 인덱스를 사용해 배열원소에 접근해야 한다.(index함수 써야함)

# case 1 - range를 통한 반복
fla_list = ['A','B','C','D']

len_list = len(fla_list)            # len을 통해 리스트 길이 확인
index_list = fla_list.index('B')    # index를 통해 배열원소 접근

for i in range(0, len_list):
  print('range with len method : ',i)

print('index method : ',index_list)
```
    > range with len method :  0
    > range with len method :  1
    > range with len method :  2
    > range with len method :  3
    > index method :  1

```python
# 리스트 반복의 경우 enumerate 내장함수를 사용해보는게 좋다.

# case 2 - enumerate 활용
fla_list = ['A','B','C','D']
enu_list = enumerate(fla_list)
# print(enu_list)
# print(next(enu_list))
# print(next(enu_list))

# enumerate는 인덱스와 값을 함께 출력해주기 때문에 상황에 따라 다양하게 활용해볼 수 있다.

for i,enu_list in enumerate(fla_list):
  print(f'{i+1}: {enu_list}')
  ```
    > 1: A
    > 2: B
    > 3: C
    > 4: D
```python
# 위의 방법을 range로 해보고 비교해보자.

for i in range(0,len(fla_list)):
  fla = fla_list[i]
  print(f'{i+1}: {fla}')
```
    > 1: A
    > 2: B
    > 3: C
    > 4: D
