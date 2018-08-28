# python 기초

### 크롤링

> 크롤링은 코드를 통해 웹사이트의 정보를 수집하는 것을 뜻한다.



#### 필요한 라이브러리

1. `requests` : 요청을 python 코드를 통해 보내주는 것.
2. `bs4` : 요청받은 결과(html, xml, ..)를 쉽게 탐색할 수 있도록 도와주는 것 라이브러리.



#### 예제코드

```python
print("hello world")
import requests
from bs4 import BeautifulSoup

1. 요청을 보낼 주소를 가져온다.

url = 'https://finance.naver.com/sise/'

1. 그 주소로 요청을 보낸다.

res = requests.get(url)

#res.status_code => 200이면, 성공적으로 가져 온 것

1. 원하는 값을 찾는다.

print(res.content)

print(res.url)

result = BeautifulSoup(res.content, 'html.parser')
#KOSPI_now
kospi = result.select_one('#KOSPI_now')

b = result.select('#KOSPI_now')[0]

print(kospi.text)
print("지금 코스피 지수는 {}입니다.".format(kospi.text))

print(b.text)

print('요청받은이후')
print(type(res.content))
print('beautifulsoup 적용이후')
print(type(result))

```



#### 추가설명

```python
# 1. BeautifulSoup type으로 변형하여 찾기 편하게 활용
# 1) request 보낸 이후
type(res)
#=> <class byte>
# 2) BeautifulSoup으로 바꾼 이후
type(result)
#=> <bs4.BeautifulSoup>
# 3) 특정 tag을 select 한 이후
type(kospi)
#=> <class 'bs4.element.tag'>
```



#### Selector(셀렉터)

1. 요소 선택자 : HTML문서에서 tag를 선택하는 것.
   `<span>코스피지수</span>` => `span`
2. 클래스 선택자 : HTML문서에서 tag에 정의된 class를 통해 선택하는 것.
   `<span class="blue">코스피지수</span>` => `.blue`
3.  아이디 선택자 : HTML문서에서 tag에 정의된 id를 통해 선택하는 것.  **문서에서 단 한개**
   `<span id="KOSPI_now">2456,24</span>` => #KOSPI_now