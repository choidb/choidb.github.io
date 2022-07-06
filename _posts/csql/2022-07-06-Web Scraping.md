---
title: 'Web Scraping'
use_math: true
categories:
  - csql
---

**목차**  
[1. HTML & CSS](#1-html--css)  
[2. DOM](#2-domdocument-object-model)  
[3. Web Scraping](#3-web-scraping)  
[4. Beautifulsoup](#4-beautifulsoup-라이브러리)  

---
* Contents
  1. 크롤링
  2. HTML / CSS 읽기
  3. DOM
  4. requests
  5. beautifulsoup

>
* Keywards
  * 크롤링
  * 웹 스크레이핑
  * HTML, CSS
  * DOM
  * beautifulsoup 라이브러리
  * parser
  * requests 라이브러리
  
[HTML 시작하기](https://developer.mozilla.org/ko/docs/Learn/HTML/Introduction_to_HTML/Getting_started)  
[DOM 소개](https://developer.mozilla.org/ko/docs/Web/API/Document_Object_Model/Introduction)  
[Beautiful Soup Documentation](https://www.crummy.com/software/BeautifulSoup/bs4/doc/)  
[Requests: HTTP for humans](https://docs.python-requests.org/en/master/)  
[Python’s Requests Library (Guide)](https://realpython.com/python-requests/)  
[CSS: Cascading Style Sheets](https://developer.mozilla.org/ko/docs/Web/CSS)  
[클래스 선택자](https://developer.mozilla.org/ko/docs/Web/CSS/Class_selectors)  
[ID 선택자](https://developer.mozilla.org/ko/docs/Web/CSS/ID_selectors)  


---

## 1. HTML & CSS
* HyperText Markup Language 의 약자로 웹에서 페이지를 표시할 때 사용
* 웹 페이지에서 보여지는 것들이 어떻게 어떤 방식으로 보여져야 하는지 알려주는 마크업 언어

1_1. HTML
1_1_1. HTML Element
* head, body, div, li 등등 
* HTML 에서는 각 엘레멘트들은 태그를 통해 표현
  * head 는 <head></head> 처럼 표현
  * 열어주는 태그 (opening tag), 닫아주는 태그 (closing tag)로 구성
    * closing tag만 '/' 사용

1_1_2. HTML Children
* HTMl 요소 안에 다른 요소를 추가 가능

```html
<ul>
    <li>Hello</li>
    <li>World</li>
    <li>!</li>
</ul>
```
1_2. CSS
* CSS 는 웹 페이지 문서가 어떻게 표현되는지 알려주는 스타일시트 언어
* Cascading Style Sheets 의 약자. HTML이 표현한 문서가 어떻게 표현이 되는지 알려줌.

1_2_1. CSS Selector
* 여러 가지 셀렉터들이 존재
* Selector는 특정 요소를 선택할 수 있는 방법
  * Type selector: CSS 타입에 따라서 선택할 수 있습니다 (예를 들어 'p', 'div' 등)
  * Class selector: 클래스에 따라 선택할 수 있습니다.
  * Id selector: id 에 따라 선택할 수 있습니다.

1_2_2. CSS 상속
* CSS 는 요소의 위치에 따라 상위 요소의 스타일을 상속받도록 되어 있다.

```html
<div style="color:red">
    <p>I have no style</p>
</div>
```
* p 태그는 아무런 스타일이 적용이 되어 있지 않지만 상위 요소인 div 의 영향을 받게됨

1_2_3. CSS 클래스
* 클래스는 어떤 특정 요소들의 스타일을 정하고 싶을 때에 사용
* 동시에 여러 개의 요소들에 대한 스타일을 정할 때에는 보통 클래스를 지정해서 상속을 받도록 정함

1_2_4. CSS ID
* ID: 클래스와 비슷하게 사용가능
* '#' 기호로 지정가능

```javascript
#pink {
    color:"pink";
}
```
# 2. DOM(Document Object Model)

2_1. DOM 소개
* Document Object Model 이라는 약자
* 웹 페이지에서 매우 중요한 역할을 하고 문서 객체 모델이라 부름
* HTML, XML 등 문서의 프로그래밍 인터페이스
* 프로그래밍 언어를 통해서 HTML 문서 등에 접근하게 함
  * 프로그래밍 언어에서도 웹 페이지의 요소나 스타일 등을 추가하거나 수정하는 등 다양한 작업을 진행 가능하게 함.
* 문서를 하나의 구조화된 형식으로 표현
  * 구조를 통해서 원하는 동작을 할 수가 있음
* DOM 은 객체 (object) 로 표현을 하는데 이 때 object 란 자바스크립트에서 사용되는 데이터 구조 중 하나
* 파이썬에서는 자바스크립트의 object 와 비슷한 dictionary 가 존재

2_2. DOM 메소드
* 웹 브라우저에서 개발자 도구를 열어 콘솔 창으로 들어가 **자바스크립트**를 통해 사용할 수 있음.

```javascript
document.querySelectorAll('p')
```
* DOM 기능
  * getElementsbyTagName: 태그 이름으로 문서의 요소 리턴
  * getElementById: 'id' 가 일치하는 요소 리턴
  * getElementsByClassName: '클래스' 가 일치하는 요소 리턴
  * querySelector: 셀렉터(들)과 일치하는 요소를 리턴
  * querySelectorAll: 셀렉터(들)과 일치하는 모든 요소 리턴
    * querySelector 나 querySelectorAll 같은 경우에는 셀렉터 (selector) 를 활용

2_3. DOM 과 크롤링
* 보통은 웹페이지를 텍스트 형식으로 사용하는 것이 아닌 DOM 을 활용

2_4. DOM 예시

```html
<!DOCTYPE html>
<html>
    <head>
    </head>
    <body>
        <h1>h1 태그입니다.</h1>
        <p>p 태그입니다.</p>
    </body>
</html>
```

## 3. Web Scraping
* 웹 크롤링: 웹을 돌아다니면서 정보를 수집하는 행위
  * 크롤링은 주로 인터넷에 있는 사이트들을 인덱싱하는 목적
* 웹 스크레이핑: 자동화에 초점이 맞춰져 있고 알아서 돌아간다.
  * 스크레이핑은 특정 정보를 가져오는 것이 목적
  * 동적 스크레이핑: 동적인 데이터를 수집하는 방법
    * 동적인 데이터: 입력, 클릭, 로그인 등과 같이 페이지 이동이 있어야 보이는 데이터
  * 정적 스크레이핑: 정적인 데이터를 수집
    * 정적 데이터: 변하지 않는 데이터
      * 한 페이지 안에서 원하는 정보가 모두 드러날때 정적 데이터라 함
  

||정적 크롤링|동적 크롤링|
|-|-|-|
|연속성|주소를 통해 단발적으로 접근|브라우저를 사용해 연속적으로 접근|
|수집 능력|수집 데이터의 한계가 존재|수집 데이터의 한계가 없음|
|속도|빠름|느림|
|라이브러리|requests, BeautifulSoup|selenium, chromedriver|

3_1. requests 라이브러리  
* 웹 스크레이핑의 가장 기초는 웹과 소통을 편하게 해줌.
* 파이썬에서 HTTP 요청을 보낼 때 거의 표준으로 사용되는 정도로 많이 사용
* HTTP 요청을 간단한 메소드를 통해 실행할 수 있도록 짜여있음.

```
pip install requests
```
3_2. 요청 보내기
```python
import requests
requests.get('https://google.com')
# 구글에 'get' 메소드로 HTTP 요청하게 됨. 
```
3_3. 응답 받기
```python
import requests

url = 'https://google.com'

resp = requests.get(url)
```
* 응답 성공 여부
  * 보낸 요청이 제대로 갔는지 확인
  * HTTP 에서는 응답에 따라 상태 메세지와 번호를 부여한다.
    * [HTTP 상태 코드](https://developer.mozilla.org/ko/docs/Web/HTTP/Status)

```python
resp.status_code
```
```python
# if 구문으로 응답 확인
import requests
from requests.exceptions import HTTPError

url = 'https://google.com'

try:
    resp = requests.get(url)

    resp.raise_for_status()
except HTTPError as Err:
    print('HTTP 에러가 발생했습니다.')
except Exception as Err:
    print('다른 에러가 발생했습니다.')
else:
    print('성공')
```

* 응답 내용
  * Response 객체에는 'text' 라는 속성이 존재
    * text 속성이 서버에서 받은 응답을 텍스트 형식으로 보여줌
  * 응답의 데이터는 사실 바이트 (bytes) 로 받음.
    * 해당 데이터를 텍스트로 인지하기 위해서는 알맞게 디코딩 작업 필요
      * 디코딩 작업은 보통 'text' 속성이 알아서 해줌.

## 4. BeautifulSoup 라이브러리
* 받아온 HTML 파일을 파싱해서 원하는 정보를 손쉽게 찾을 수 있도록 해줌
* 설치
```
pip install beautifulsoup4
```
4_1. 기본 파싱
* 파싱할 문자열과 어떻게 파싱할 것인지를 정함
* 'html.parser' : 기본적으로 사용되는 파서
  * 파싱 (parsing): 문자열로 구성된 특정 문서들 (HTML, XML) 등을 파이썬에서도 쉽게 사용할 수 있도록 변환해주는 작업

```python
import requests
from bs4 import BeautifulSoup

url = 'https://google.com'
page = requests.get(url)

soup = BeautifulSoup(page.content, 'html.parser')
```
4_2. 요소 찾기

*  find 및 find_all 메소드
   * find: bs4 에서 한 개의 요소를 찾을 때 사용
     * 조건에 일치하는 첫번째 결과를 리턴
   * find_all: 여러 개의 요소들을 찾을 때 사용
     * 조건에 일치하는 모든 결과를 리스트에 담아 리턴

>
*  id, class, tag 등의 특징

```python
# id 는 주로 한번만 사용이 되기 때문에 find 를 사용
dog_element = soup.find(id='dog')

# class 를 이용해 찾을 때에는 class 가 아닌 뒤에 밑줄 '_' 을 추가. 추가하지 않으면 파이썬의 class 로 인식함.
cat_elements = soup.find_all(class_='cat')
```
* 태그 활용
  * 상세하게 찾고 싶을 때에는 태그와 함께 조합해서 사용

```python
# 예시
# 'cat' 이라는 클래스가 'div' 태그에도 있고 'p' 태그에도 존재하며
# 'div' 태그를 사용하는 요소를 가지고 올 때

cat_div_elements = soup.find_all('div', class_='cat')
```
* string 활용

```python
# raining 문자열이 포함되어 있는 요소 찾을 때
soup.find_all(string='raining')

# 대소문자 구분없이 문자 찾을 때 사용
soup.find_all(string=lambda text: 'raining' in text.lower())

# 문자열이 아닌 하나의 요소로 받기 위해서는 태그('h3')도 같이 추가해야함.
soup.find_all('h3', string='raining')
```

