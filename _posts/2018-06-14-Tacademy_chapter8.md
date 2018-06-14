---
title: Python -  T아카데미 Python 강의 정리 chapter 8
description:
categories:
 - tutorial
tags:
---

## 입출력

> ### 출력 (Print)

- print 함수의 입력인자로 구분자(sep), 끝라인(end), 출력(file) 지정 가능  

```python
>> print('welcome to', 'pyhton', sep='~', end='!', file=sys.stderr)
welcom to~python!
```
- 위 예제와 같이 file을 이용해 출력을 표준오류(Standard Error)로 변경하거나 파일로 바꿀 수 있음  
- 이 경우 표준에러에 welcome to~python! 이 출력됨.   ~~(무슨말인지 모르겠음. 찾아볼것)~~
- 구분자 기본값 : 공백, end 기본값 : 줄바꿈  

> 포멧팅 (fomatting)  

- 문자열 내에 값이 들어갈 곳을 `{}`로 표시함

```python
>> print('{} is {}'.format('apple','red'))
apple is red

>> print('{0} is {1}'.format('apple','red'))
apple is red
```

- 포맷팅(formatting)의 인자로 key, value 사용가능  

```python
>> print('{item} is {color}'.format(item='apple', color='red')
apple is red

>> dic = {'item':'apple', 'color':'red'}
>> print('{0[item]} is {0[color]}'.format(dic))
apple is red

** 기호 사용하면 dictionary를 입력받은 것으로 판단
>> print('{item} is {color}'.format(**dic))
apple is red
```

- f-string 방법 (python 3.6 버전에 추가됨)  

```python
>> fruit = 'apple' ; color = 'red'
>> print(f'{fruit} is {color}')
apple is red
```

> 포맷팅 - 정렬과 부호 표현법  

- 정렬에 사용되는 기호  
 - >, <, ^, =  
- 부호를 나타내는 기호  
 - +, -, =  
- 진수 표현법
 - b(2진수), d(10진수), x(16진수), o(8진수), c(문자열)
 - #x, #o, #b 로도 표현 가능, 앞에 진수 정보가 표시됨
- 실수 표현법
 - e : 지수표현, f : 실수표현, % : 퍼센트 표현법
 
 
 
> ### 입력  

- input() 함수를 이용해서 사용자 입력 받음
- input 입력인자로 화면에 출력할 prompt 줄 수 있다
- 결과값으로 문자열 객체를 반환

```python
>> a = input('insert key: ')
.. insert key: test
>> print(a)
test
```

> ### 파일 입출력 - open

- open(file, mode)

- r:읽기모드(기본), w:쓰기모드, a:쓰기+이어쓰기, +:일기+쓰기, b:바이너리, t:텍스트(기본)

```python
>> f = open('test.txt', 'w')
>> f.write('hello pyhton')
12
>> f.close()

>> f = open('test.txt')  #기본인 텍스트 모드로 열림
>> f.read()
'hello python'
>> f.close()
>> f.closed
True
```

- 텍스트 모드에서는 일반 문자열과 같이 encoding이 적용되기 때문에, binary data 다룰 때에 오류발생
- binary data는 반드시 바이너리 모드를 사용

> 파일 입출력 관련 함수를

- readline() : 호출할 때 마다 한 줄씩 읽은 문자열 반환
- readlines() : 파일의 모든 내용을 줄 단위로 잘라 리스트로 반환
- tell() : 파일 어디까지 읽고 썼는지 위치 반환
- seek() : 사용자가 원하는 위치로 포인터 이동

- with ~ as 를 이용하면 파일이 자동으로 닫힘  

```python
>> with open('test.txt') as f:
..  print(f.readlines())
..  print(f.closed)
['hello python']
False 

>> f.closed
True
```

> pickle 사용

```python
>> colors = ['red','green','blue']
>> import pickle
>> f = open('colos', 'wb')
>> pickle.dump(colors, f)
>> f.close()
```

```python
>> del colors
>> f = open('colors', 'rb') #pickle로 파일에 읽고 쓸때는 binary 모드로 파일을 열어야함
>> colors = pickle.load(f)
>> f.close()
>> colors
['red', 'green', 'blue']
```

> pickle - 사용자 정의 클래스

```python
>> class test:
..   var = None

>> a = test()
>> a.var = 'Test text'
>> f = open('test2', 'wb')
>> pickle.dump(a, f)
>> f.close()
>> f = open('test2', 'rb')
>> b = pickle.load(f)
>> f.close()
>> b.var
'Test text'
```






***  
#### 더 보충해야 할 내용
- raise, assert 사용 예시 보고 어떤 경우에 사용되는지 확인할것

***  





