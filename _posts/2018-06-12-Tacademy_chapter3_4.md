---
title: Python -  T아카데미 Python 강의 정리 chapter 3 and 4
description:
categories:
 - tutorial
tags:
---


## 함수 

> 함수란?

- 여러개의 문장(Statement)을 하나로 묶어줌
- 프로그램을 구조적, 물리적으로 만들어줌
- 규모가 큰 프로그램을 개발하는데 필요한 비용 줄여줌

> 함수 선언

- 함수를 선언하면 메모리에 함수 객체가 생성됨
- 함수 객체를 가리키는 레퍼런스가 생성
- 함수의 이름은 함수가 생성될 때 함수 객체를 참조하는 레퍼런스임
- 함수 레퍼런스는 다른 변수에 할당 할 수 있음

```python
> def Times(a,b):
... return a*b
> Times(10,10)
100
> myTimes = Times
> r = myTimes(10,10)
> r
100
```

함수 객체가 복사되는 것이 아니라 레퍼런스만 복사됨

> return

- return은 객은 여러개의 값을 튜플로 묶어서 값을 전달함
- return을 사용하지 않거나 return만 적을 때도 함수가 종료됨  

> 파이썬 함수에서 인수 전달

- Scoping rule
  
  - Name Space
    - 함수 내부 : Local scope
	- 함수 밖 전역 영역 : Global scope
	- 파이썬 자체에서 정의한 영역 : Bulit-in Scope
	
  - LGB 규칙 : Local -> Global -> Built-in 순서로 찾음 
  - `global`로 변수 선언지 전역 영역 변수값 변경 가능
  
> 파이썬 인수 모드
 
 - 기본 인수 값 : 함수 호출시 인수 지정하지 않아도 기본 값이 할당되도록 하는 방법
 
 ```python
 > def Times(a=10, b=20):
 ... return a+b
 > Times()
 200
 > Times(5)
 100
 ```
 
- 키워드 인수 : 순서와 상관없이 변수의 이름으로 인수를 전달
  - 키워드 인수는 일반 인수 뒤에 위치, 키워드 인수 
  - 이후에는 순서에 의한 인수 매칭 불가

- 가변인수 리스트
 - `*`를 사용하여 개수가 정해지지 않은 가변 인수를 전달
 - 인수는 튜플 형식으로 전달됨
 
 ```python
 > def union(*ar):
 ..  res = []
 ..  for item in ar:
 ..    if not x in res:
 ..      res.append(x)
 ..  return res
> union("HAM", "EGG")
['H','A','M','E','G']
```

- 정의되지 않은 인수 처리
 - `**`를 사용해서 정의되지 않은 인수를 딕셔너리 형식으로 전달
 - 인수들 중 가장 마지막에 와야 함
 
```python
> def userURI(server, port, **user):
..  str = "http://" + server + ":" + port + "/?"
..  for key in user.keys():
..    str += key + "=" + user[key] + "&"
..  return str
> userURI('test.com', '8080', id='userid', passwd='1234', name='mike', age = 20)
'http://test.com:8080/?passwd=1234&age=20&id=userid&name=mkie&'
```

> lambda 함수

- 함수는 이름이 없고 객체만 있을 뿐이다. 기본 레퍼런스를 이름이라고 부르고 있는 것임.
- C, C++ 에서는 함수는 이름이 있어야함
- 파이썬에서는 함수 객체만 존재하는 익명함수를 만들 수 있음, `return`구문 적지 않음
- 한 줄 실행한 결과값이 바로 리턴값
 
- 어디에 사용?
 - 한줄의 간단한 함수 필요
 - 가독성
 - 간단한 함수를 인수로 넘겨줄 때

```python
=======람다 함수 예시 정리할것=======
```
 
> 재귀적(recursive) 함수 호출 

- 함수 내부에서 계속 자신을 호출하는 방법 
- 변수를 조금씩 변경하면서 반복된 연산을 할 때 유용

```python
> def factorial(x):
..  if x == 1:
..    return 1
..  return x * factorial(x-1)
> factorial(10)
3628800
```

> pass 구문

- 아무것도 하지 않는 함수, 모듈 등을 만들어야 할 경우 사용


> help 함수로 함수의 설명 볼 수 있음

- `help(print)`
- `__doc__` 속성을 이용해 함수에 자세한 설명 추가 가능

```python
> plus.__doc__ = 'return the sum of parameter a,b'
> help(plus)
Help on function plus in module __main__:
plus(a,b)
    return the sum of parameter a,b
```

참고 : 람다, 이터레이터, 제너레이터 모두 *함수*임

> iterate

- 순회 가능한 객체의 요소를 순서대로 접근할 수 있는 객체 
- 이터레이터 안의 __next__()를 이용해 순회 가능한 객체의 요소에 하나씩 접근 가능

```python
> s = 'abc'
> it = iter(s)
> it
<iterator object>
> next(it)
'a'
> next(it)
'b'
> it.__next__()
'c'
> next(it)
~~~
StopItertaion
```

- `for` 구문은 이터레이터를 이용해 `StopIteration`을 만날때 까지 반복적으로 next를 수행함

> **Generator**

- Iterator를 만드는 간단하고 강력한 도구 
- 함수가 호출되면 지역변수와 코드가 스택에 적재되고 코드가 수행함
- 함수가 끝나면 결과값을 호출한 곳에 넘겨주고 함수 객체는 스택에서 사라짐
- 함수에 `return` 대신 `yeild`를 적어주면 함수를 끝내지 않고 호출한 곳에 값을 전달함

```python
> def reverse2(data):
..    for index in range(len(data) - 1, -1, -1):
..        yield data[index]
		
> for char in reverse2('golf'):
..    print(char)
f
l
o
g
```

- yeild는 호출한 곳에 값을 돌려주지만 함수는 메모리에 그대로 있다
- 다음번 reverse 함수가 호출되면 가장 최근에 호출된 상태로 실행된다.

참고 : range(시작값, 끝값, 증가값)

```python
>> def abc():
..     data = 'abc'
..     for char in data:
..         yield char
>> abc()
<generator object abc at 0x7fe4a0287518>
>> it = iter(abc())
>> next(it)
'a'
>> next(it)
'b'
>> next(it)
'c'
>> next(it)
---------------------------------------------------------------------------
StopIteration                             Traceback (most recent call last)
<ipython-input-18-bc1ab118995a> in <module>()
----> 1 next(it)

StopIteration: 
```

## 제어문

> if문
 
- 조건식을 평가하고 참인 경우에만 구문 수행함
- 들여쓰기로 블록 지정

> elif

- 필요한 만큼 사용 가능
- 2개 이상의 조건을 처리하는 경우 사용

> else

- 가장 마지막에만 사용 가능
- 어떤 조건에도 해당 안되는 경우

> Python의 조건식 표현 방법  

Python : `70 <= score < 80`  
다른 언어 : `score >= 70 and score < 80`

> 논리식 판별 순서

- 2개 이상일 경우 식의 왼쪽에서 오른쪽으로 판별
- 단축평가
 - 조건식 전체를 판단하지 않고 순차적으로 진행.
 - 좌변이 우변보다 먼저 단축평가

```python
>> a = 0
>> if a and 10/a : # 단축평가로 앞의 a가 False가 되어 else로 넘어감
..     print('a가 0')
.. else:
..     print('에러없이 통과')
에러없이 통과
```

> 참고
- 파이썬에서는 `&&`연산이 없다. `and` 
- `&`, `|`, XOR(`^`), NOT(`~`), Shift(`<<`, `>>`) 는 비트연산자


- 단축평가의 장점
 - 추가 판별 연산을 수행하지 않아 속도 향상
 - Runtime error 발생을 논리식으로 사전 차단 가능

> for문

- for문에 사용할 수 있는 자료 
 - 문자열, 리스트, 튜플, 사전, 이터레이터, 제너레이터 객체
 
 ```python
>> l = [10,20,30]
>> iterator = iter(l)
>> for i in iterator:
..     print(i)
10
20
30
```
 
- `break`를 만나면 반복문 내부 블록을 벗어남
- `continue`를 만나면 이후 내부 블록 수행하지 않고 다음 아이템을 선택하여 내부 블록 시작지점으로 이동


## 리스트 내장

> [<표현식> for <아이템> in <시퀀스객체> (if <조건식>]

- 기존 시퀀스 객체를 이용하여 추가적인 연산을 통해 새로운 리스트 객체 생성

```python
>> l = [1,2,3,4,5]
>> [ i**2 for i in l]
[1, 4, 9, 16, 25]
>> t= ('orange','apple','banana')
>> [len(i) for i in t]
[6, 5, 6]

>> [i for i in t if len(i)>5]
['orange', 'banana']

>> L1 = [3,4,5]
>> L2 = [1.5, -0.5, 4]
>> [x*y for x in L1 for y in L2 if y > 0]
[4.5, 12, 6.0, 16, 7.5, 20]
```

## 제어문 관련 유용한 함수

> filter

- 함수의 결과가 참인 시퀀스 객체의 iterator를 반환
- None이 오는 경우 필터링 X

```python
>> L = [10, 20, 30,40]
>> iterL = filter(None, L)
>> for i in  iterL:
..     print('Item : {}'.format(i))
Item : 10
Item : 20
Item : 30
Item : 40

 
>> def GetBiggerThan20(i):
..     return i > 20

>> list(filter(GetBiggerThan20, L))
[30, 40]

>> list(filter(lambda i:i>20, L))
[30, 40]
```

> range 함수

- 수열을 순회하는 이터레이션 가능한 이터레이터 객체 반환
- 시작값, 증가값은 생략 가능 (이때는 각각 0, 1이 할당됨)

```python
>> list(range(10,-1,-1))
[10, 9, 8, 7, 6, 5, 4, 3, 2, 1, 0]
```

> map 함수

- 시퀀스 객체를 순회하며 function 수행

```python
>> L = [10,20,30]
.. def Add10(i):
..     return i+10

>> for i in map(Add10, L):
..     print('Item : {}'.format(i))
Item : 20
Item : 30
Item : 40

>> X = [1,2,3]
>> Y = [2,3,4]
>> list(map(pow, X, Y)
[1, 8, 81]
```

***
#### 더 보충해야 할 내용
- lambda 함수 구조, 사용 예시
- iterator, generator 사용
- [map 함수 사용 예시](https://wikidocs.net/64)
***