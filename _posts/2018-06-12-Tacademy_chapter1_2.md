---
title: Python -  T아카데미 Python 강의 정리 chapter_1&2 
description:
categories:
 - tutorial
tags:
---

## 파이썬 개요  

> Python 특징  

가독성, 풍부한 라이브러리, 접착성, 유니코드, 무료, 동적타이핑  

> 2.~ 버전과 3.~ 버전의 차이  

- print 변화
- long에서 int로 통일
- int와 int 나눈 값이 float로 처리
- string, unicode 체계 변경

> `#`은 주석으로 인식  

소스코드 부분에서 사용될 경우 소스코드 인코딩을 지정하는 용도로 사용될  
`- # -*- coding: utf-8-*-`  
설정 안하면 아스키 코드가 기본  
적절한 소스코드 인코딩을 작성하지 않고 한글 주석을 달 경우 인코딩 에러가 발생할 수 있다.  

> `2to3`를 이용하면 간단한 프로그램을 쉽게 변환가능  

큰 모듈의 경우 테스트 케이스를 만들어서 오동작 여부를 테스트 해야함  


## 자료형 및 연산자  

> complex (복소수)  

```python
> x = 3 - 4j
> type(x), x.imag, x.real, x.conjugate()
(<class 'complex>, -4.0, 3.0, (3+4j))
```

- 정수나누기  

```python
> 5//2
2
```

> Escape 문자  

`\n` : 개행  
`\t` : 탭  
`\r` : 캐리지 리턴  
`\0` : 널(null)  
`\\` : 문자 `\`  
`\'` : 단일 인용부호(')  

> 인덱싱 & 슬라이싱

```python
> 'python'[0]
'p'
> 'python'[1:4]
'yth'
```

인덱싱을 이용한 문자열 변경은 허용되지 않음  

다만 문자열 전체를 다시 할당할 때는 가능  

> 유니코드  

모든 string(문자열)은 유니코드  
유니코드 이외의 인코딩이 있는 문자열은 bytes로 표현  

```python
> type('가')
<class 'str'>
> type('가'.encode('utf-8'))
<class 'bytes'>
```

> 리스트  

- `append`, `insert`, `extend`, `+` 연산자를 이용해 값들을 추가할 수 있다 
 
```python
> colors = ['green']
> colors.append('blue')
> colors
['green','blue']
> colors.extend(['white','gray'])
> colors
['green','blue','white','gray']
```
- index를 이용해 값 위치 확인  

```python
> colors.index('green')
0
> colors.index('green',1)
4
```

- count, pop

```python
> colors.count('green')
1
> colors.pop()
'gray'
> colors
['green','blue','white']
```

- remove로 값 제거, sort로 정렬 가능  

> 튜플

- 튜플(tuple)은 리스트와 유사, but 읽기 전용
- 속도는 빠르지만 제공되는 함수 적다
- count, index 메서드 제공
- 튜플을 이용하면 간단히 swap 가능
`a,b = b,a`

> 딕셔너리  

- 키와 쌍으로 이루어짐
```python
> color = {'apple':'red', 'banana':'yellow'}
> color['cherry']='red'
> color
{'apple':'red', 'banana':'yellow', 'cherry':'red'}
```

- items() : 딕셔너리의 모든 키와 값을 튜플로 묶어 반환

- keys() : 키만 반환  
- values() : 값만 반환  
- `del color['cherry']` : 삭제
- `color.clear()` : 모두 삭제

> 부울(bool)

- 비교연산자 : `>`, `<`, `==`, `!=`, `>=`, `<=`

- 논리연산자 : and(&), or(|), not

> 얕은복사 vs 깊은복사

- 얕은복사 : 주소가 복사되어 객체를 공유
- 깊은복사 : 객체를 공유하지 않는 경우

얕은복사 예
```python
> a = [1,2,3]
> b = a
> a[0] = 38
> a
[38,2,3]
> b
[38,2,3]
> id(a) == id(b)
True
```

깊은복사 예
```python
> a = [1,2,3]
> b = a[:]
> id(a) == id(b)
False
> a[0] = 38
> a
[38,2,3]
> b
[1,2,3]
```

***
#### 더 보충할 내용
- 레퍼런스와 주소, 메모리에 대해 더 자세히 알아보기
 - 포인터의 개념과 연관 있을지도

***


