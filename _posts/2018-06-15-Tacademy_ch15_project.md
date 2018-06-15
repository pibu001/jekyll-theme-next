---
title: Python - T아카데미 정리 & 주가 parsing 프로젝트  
description:  
categories: 
 - tutorial  
tags:  
---

## 정적메서드, 클래스 메서드

> 정적(스태틱) 메서드

스태틱 메서드는 클래스 내부에 정의된 일반 함수이며, 단지 클래스나 인스턴스를 통해서 접근할 수 있을 뿐 
해당 클래스나 인스턴스에 영향을 주는 것은 불가능하다.

스태틱메서드는 `@staticmethod`데코레이터를 붙여 선언한다.

스태틱메서드는 다양한 방식으로 인스턴스를 생성하는 클래스를 작성할 때 자주 사용된다. `__init__()`초기화 함수는 
하나만 존재할 수 있기 때문에, 다른 생성함수를 정적 메서드로 만들어 사용할 수 있다.

```python
import random

class Animal:
    def __init__(self, name, type):
        self.name = name
        self.type = type

    @staticmethod
    def ground():
        animals = ('lion', 'tiger', 'cat')
        selected_animals = random.choice(animals)
        return Animal(selected_animals, '땅')

    @staticmethod
    def sea():
        animals = ('꼬부기', '아쿠스타', '라프라스')
        selected_animals = random.choice(animals)
        return Animal(selected_animals, '바다')
```

> 클래스 메서드

클래스 메서드는 클래스 속성에 대해 동작하는 메서드이다. 위의 인스턴스 메서드와 달리 호출 주체가 클래스이며, 첫 번째 인자도 클래스이다.
만약 인스턴스가 첫 번째 인자로 주어지더라도 해당 인자의 클래스로 자동으로 바뀌어 전달된다.

클래스메서드는 `@classmethod`데코레이터를 붙여 선언하며, 첫 번째 인자의 이름은 관용적으로 `cls`를 사용한다.

클래스 메서드를 사용하면 부모 클래스를 상속받은 자식클래스에서 해당 부모클래스의 클래스 메서드를 사용할 경우, 
자기 자신(자식)의 클래스를 사용할 수 있다.


## 다형성 동적 바인딩

다형성은 관용적으로는 일반적으로 하나의 코드가 여러 역할을 한다는 의미이다. 예를 들어, str()이라는 내장 함수는 인수로 전달되는 객체의 타입에 관계 없이 해당 객체를 문자열 형으로 형변환 시켜준다. 이는 str()함수가 다형성을 띄고 있다는 말이며, 하나의 함수가 여러 타입의 객체를 처리할 수 있도록 설계되어 있음을 나타낸다.

동적 바인딩은 타입을 신경 쓰지 않고 인스턴스를 사용할 수 있게 해주는 방식이다. 위의 다형성과 맞물려 다형성을 띄는 함수에 타입에 관계없이 다양한 객체들을 인수로 전달할 수 있다.

동적 바인딩은 속성 검색과정을 통해서 이루어진다. obj.attr을 통해 속성에 접근하면, 인스턴스에서 attr을, 다음엔 클래스에서, 그 다음에는 상속받은 클래스에서 해당 속성을 검색하며 가장 먼저 검색한 속성을 반환한다.

동적으로 속성을 바인딩하는 과정은 obj객체의 타입에 영향받지 않으며, 오로지 해당 객체가 attr에 해당하는 속성을 가졌는지만 검사한다. 위의 str()함수를 예로 들면, str()함수는 전달된 인수의 __str__()속성을 리턴한다.

이러한 작동방식은 '오리처럼 울고걸으면 그것은 오리이다'라는 말에서 유래한 덕 타이핑(duck typing)이라고 한다. 덕 타이핑은 동적 타이핑의 한 종류이며, 객체가 가진 변수와 메서드가 해당 객체의 타입을 결정함을 말한다.


## 정규표현식(Regular Expressions)

특정한 패턴에 일치하는 복잡한 문자열을 처리할 때 사용하는 기법. 

파이썬에서는 표준 모듈 `re`를 사용해서 정규표현식을 사용할 수 있다.

```python
import re
result = re.match('Lux', 'Lux, the Lady of Luminosity')
```

위에서 `match`의 첫 번째 인자에는 패턴이 들어가며, 두 번째 인자에는 문자열 소스가 들어간다. `match()`는 소스와 패턴의 일치 여부를 확인하고, 일치할 경우 `Match object`를 반환한다.

조금 복잡하거나 자주 사용되는 패턴은 미리 **컴파일**하여 속도를 향상시킬 수 있다.

```python
pattern1 = re.compile('Lux')
```

컴파일된 패턴객체를 문자열 대신 첫 번째 인자로 사용 가능하다.


#### match : 시작부터 일치하는 패턴 찾기

```python
>>> import re
>>> source = 'Lux, the Lady of Luminosity'
>>> m = re.match('Lux', source)
>>> if m:
...   print(m.group())
...
Lux
```

`match()`는 시작부분부터 일치하는 패턴만 찾기 때문에, `Lady`라는 패턴으로는 찾을 수 없다.

```python
>>> m = re.match('.*Lady', source)
>>> if m:
...   print(m.group())
...
Lux, the Lady
```

위 결과는 다음을 의미한다.

- `.`은 문자 1개를 의미
- `*`는 해당 패턴이 0회 이상 올 수 있다는 의미이다
- 따라서 `.*Lady`는 앞에 아무 문자열(또는 빈) 이후 Lady로 끝나는 패턴을 의미한다

#### search : 첫 번째 일치하는 패턴 찾기

`*`패턴 없이 `Lady`만 찾을 경우, 문자열 전체에서 일치하는 부분을 찾는 `search()`를 사용한다.

```python
>>> m = re.search('Lady', source)
>>> if m:
...   print(m.group())
...
Lady
```

#### findall : 일치하는 모든 패턴 찾기

```python
>>> m = re.findall('y', source)
>>> m
>>> ['y', 'y']
>>> m = re.findall('y..', source)
>>> m
['y o']
```

끝자리의 `y`는 뒤에 문자가 더 없으므로 포함되지 않으므로, `?`를 추가한다.  
`.`은 문자 1개를 의미하며, `?`는 0 또는 1회 반복을 사용한다. `.?`은 문자가 0 또는 1회 올 수 있음을 의미한다.

```python
>>> m = re.findall('y.?.?', source)
>>> m
['y o', 'y']
```

#### split : 패턴으로 나누기

문자열의 `split()`메서드와 비슷하지만 패턴을 사용할 수 있다.

```python
>>> m = re.split('o', source)
>>> m
['Lux, the Lady ', 'f Lumin', 'sity']
```

#### sub : 패턴 대체하기

문자열의 `replace()`메서드와 비슷하지만 패턴을 사용할 수 있다.

```python
>>> m = re.sub('o', '!', source)
>>> m
'Lux, the Lady !f Lumin!sity'
```

#### 정규표현식의 패턴 문자

패턴|문자
---|---
\\d|숫자
\\D|비숫자
\\w|문자
\\W|비문자
\\s|공백 문자
\\S|비공백 문자
\\b|단어 경계 (\w와 \W의 경계)
\\B|비단어 경계

```python
>>> import string
>>> printable = string.printable
>>> re.findall('\w', printable)
>>> re.findall('\d', printable)
```

#### 정규표현식의 패턴 지정자 (Pattern specifier)

**expr**은 정규표현식을 말한다

패턴|의미
---|---
abc|리터럴 `abc`
(expr)|expr
expr1 \| expr2 | expr1 또는 expr2
`.` | `\n`을 제외한 모든 문자
`^` | 소스문자열의 시작
`$` | 소스문자열의 끝
expr`?` | 0 또는 1회의 expr
expr`*` | 0회 이상의 최대 expr
expr`*?`| 0회 이상의 최소 expr
expr`+` | 1회 이상의 최대 expr
expr`+?`| 1회 이상의 최소 expr
expr`{m}`| m회의 expr
expr`{m,n}`| m에서 n회의 최대 expr
expr`{m,n}?` | m에서 n회의 최소 expr
[abc] | a or b or c
[^abc] | not (a or b or c)
expr1(?=expr2) | 뒤에 expr2가 오면 expr1에 해당하는 부분
expr1(?!expr2) | 뒤에 expr2가 오지 않으면 expr1에 해당하는 부분
(?<=expr1)expr2 | 앞에 expr1이 오면 expr2에 해당하는 부분
(?<!expr1)expr2 | 앞에 expr1이 오지 않으면 expr2에 해당하는 부분

<br>

## 네임스페이스 (Namespace)

각 모듈은 독립된 네임스페이스(이름공간)를 가진다. 메인으로 사용되고 있는 모듈이 아닌 import된 모듈의 경우, 해당 모듈의 네임스페이스를 사용해 모듈 내부의 데이터에 접근한다.

- from을 사용해 모듈의 함수를 직접 import

`import 모듈명`의 경우, 모듈의 이름이 전역 네임스페이스에 등록되어 `모듈명.함수`로 사용가능하다.

모듈명을 생략하고 모듈 내부의 함수를 쓰고 싶다면, `from 모듈명 import 함수명`으로 불러들일 수 있다.

- from 모듈명 * 을 사용해 모듈 내 모든 식별자 (변수, 함수) import

- as로 별칭 할당

`from 모듈명 import` 또는 `import 모듈명`에서, 같은 모듈명이 존재하거나 혼동 될 수 있을 경우, 뒤에 `as`를 붙여 사용할 모듈명을 변경할 수 있다.

- 커맨드라인에서 인자 전달

프로그램 실행 시 인자를 전달 할 수 있다. 파이썬의 내장`sys`모듈의 `argv`리스트에서 확인 할 수 있다.

리스트의 첫 번째 항목은 모듈명이 전달되므로, 2번째 항목부터 전달 된 값을 확인 할 수 있다.

<br>
## 주가 parsing

- kind.krx.co.kr에서 유가증권 리스트를 엑셀로 다운받고 이를 csv로 변환
- stock.csv 파일에서 종목명과 code를 가져옴
- 다음 finance에 code를 검색하여 가격과 rate를 가져옴
- BeautifulSoup, urllib 라이브러리 활용
- user_agent 주지 않으면 HTTPError 발생 (사이트에서 막는듯)
- Timesleep 주지 않으면 URLError 발생 (사이트에서 막는듯)

코드 : 

```python
with open('stock.csv', 'r', encoding='utf-8') as f:
    stocks = f.readlines()[1:10]
    
interesting = []
user_agent = 'Mozilla/5.0 (iPhone; CPU iPhone OS 5_0 like Mac OS X) AppleWebKit/534.46'

for stock in stocks:
    col = stock.split(',')
    name, code = col[0], col[1]
    
    while len(code) < 6:
        code = "0" + code
        
    url = 'http://finance.daum.net/item/main.daum?code='+code
    request = urllib.request.Request(url, data=None, headers={'User-Agent': user_agent})  #block avoiding
    response = urllib.request.urlopen(request)
    content = response.read()
    text = content.decode('utf-8')  # ignore, replce, strict option
    soup = BeautifulSoup(text,"html5lib")
    soup_today = soup.select('.price')  # html sorcecode
    soup_rate = soup.select('.rate_fluc')
    
    today = soup_today[0].text
    rate = soup_rate[0].text
    
    fRate = float(rate[:-1])
    if abs(fRate)>5:   # +5% 이상이나 -5% 이하의 종목
        interesting.append((name,code,today,rate,fRate))
    
    print(name, code, today, rate)
    time.sleep(1)   # if too high speed, potal bolcking me
    
print("Today's intersting stocks :")
for i in interesting:
    print(i)
```

출력 : 

```
HDC현대산업개발 294870 66,300 -5.96%
애경산업 018250 63,600 +0.95%
셀트리온 068270 298,500 +6.61%
쿠쿠홈시스 284740 225,500 -4.85%
SK케미칼 285130 96,300 +5.71%
BGF리테일 282330 192,500 -3.27%
동양피스톤 092780 4,475 +0.45%
진에어 272450 30,000 -5.66%
케이씨텍 281820 24,050 -0.82%
Today's intersting stocks :
('HDC현대산업개발', '294870', '66,300', '-5.96%', -5.96)
('셀트리온', '068270', '298,500', '+6.61%', 6.61)
('SK케미칼', '285130', '96,300', '+5.71%', 5.71)
('진에어', '272450', '30,000', '-5.66%', -5.66)
```

## 오류 정리

>  urllib.request.urlopen(주소) 했을때 URLError 발생

아마 bot 사용을 차단하기 위해서 포털 사이트에서 block 하는것 같다.

```python
user_agent = 'Mozilla/5.0 (iPhone; CPU iPhone OS 5_0 like Mac OS X) AppleWebKit/534.46'
request = urllib.request.Request('http://finance.daum.net/item/main.daum?code=294870', data=None, headers={'User-Agent': user_agent})
```

이렇게 user_agent 설정하고 

```python
response = urllib.request.urlopen(request)
```
요청하면 오류 안남

> csv 파일 깨지는 오류

윈도우에서 다운받은 엑셀파일을 구글드라이브에 올리고 VirturBox의 우분투에서 다운받으면 한글이 깨지는 문제 발생  
`response.read().decode('utf-8')`에서 에러가 자꾸 발생하여 원인을 찾다가 발견함. ~~시간을 많이 잡아먹음~~

결국 VirturBox의 우분투에서 직접 사이트에 들어가 엑셀파일을 다운받아 해결함  
~~우분투를 영어로 깔아서 한글이 깨진것 같지만 정확하지 않음~~

> 구름 ide에서 turtle 모듈 import 안되는 오류

로컬의 python에서는 되지만 구름 서버의 우분투에서는 import가 안됨. ~~_tkinker에서 문제 발생한듯~~ 

VirturBox에서 anaconda깔고 가상환경에서 실행했을 때는 잘 되었다.






