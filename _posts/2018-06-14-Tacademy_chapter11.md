---
title: Python -  T아카데미 Python 강의 정리 chapter_11
description:
categories:
 - tutorial
tags:
---


## 숫자 다루기

> 내장함수

- 대부분 수학 관련 모둘이 `math`모듈에 존재
- 자주 사용되는 부분은 내장함수로 제공
- 내장함수 리스트
  - sum(iterable,[start]) : 순회 가능한(irable) 객체의 총 합계를 반환
  - max(iterable) : 순회 가능한 객체의 최댓값을 반환
  - min(iterable) : 순회 가능한 객체의 최솟값을 바환
  - abs(x) : x의 절대값을 반환
  - pow(x,y) : x의 y제곱을 반환
  - round(x) : x의 반올림 결과를 반환
  - divmod(a,b) : a/b의 몫과 나머지를 튜플 형태로 반환

```python
>>> l=list(range(0,10))
>>> sum(l)
45
>>> max(l)
9
>>> min(l)
0
>>> abs(-11)
11
>>> pow(2,10)
1024
```

> math 모듈의 수치 연산 함수

- math.ceil(x) : N >= x 를 만족하는 가장 작은 정수 N을 반환
- math.floor(x) : N <= x 를 만족하는 가장 큰 정수 N을 반환
- math.trunc(x) : x의 정수 부분만 반환
- math.copysign(x,y) : y의 부호만 x에 복사하여 반환
- math.fabs(x) : x의 절대값 반환
- math.factorial(x) : x의 factorial값 반환
- math.fmod(x,y) : 나머지 연산 수행 (x%y 와 값이 항상 동일한 것은 아님)
 - 정수 연산에는 %를 쓰고 부동소수점 연산에는 fmod 쓰는것을 권장
- math.fsum(iterable) : 입력받은 값의 합계 리턴
- math.modf(x) : 입력받은 x의 순수 소수부분과 정수부분으로 분리하여 튜플로 반환

> 지수, 로그 연산

- math.pow(x,y) : x의 y제곱 리턴
- math.sqrt(x) : x의 제곱근(square root)한 결과 리턴
- math.exp(x) : e의 x승을 리턴
- math.log(x[,base]) : 밑을 base로 하는 `log X`의 결과를 리턴

> 삼각함수 연산

- math.degrees(x) : 라디안 -> 60분법 변환
- math.radians(x) : 60분법 -> 라디안 변환

> Fraction 클래스

- 유리수 관련 연산을 처리할 수 있는 분수(fractions) 모듈
 - 분모 0인 경우 ZeroDivisionError 발생

```python
>>> fractions.Fraction(4, 16)
Fraction(1, 4)
>>> fractions.Fraction(3)
Fraction(3, 1)
>>> fractions.Fraction('3.14')
Fraction(157, 50)
>>> f = fractions.Fraction('3.14')
>>> math.floor(f)
3
>>> math.ceil(f)
4  
```

> 십진법(decimal) 모듈

- 실수를 표현하기 위해 float 자료형보다 보다 정확한 decimal 클래스 제공
- 컴퓨터에서 수치 표현하기 위해 정수 - 고정소수점 방식, 실수 - 부동소수점 방식 사용
- 부동소수점 방식 : 소수점의 위치를 고정하지 않고 그 위치를 나타내는 수를 따로 적는 방식
- 유효숫자를 나타내는 가수, 소수점 위치를 풀이하는 지수로 나누어 표현
- `[가수]*[밑수]^[지수]`와 같은 형태  

![실수 표현](https://drive.google.com/file/d/1zw59uw0o8haZUUp5u4BNv2jyTZHgNv1-/view?usp=sharing)

- float과 다르게 실수를 정확하게 표현 가능
- 양의 무한대, 음의 무한대 표현 가능
- 소수점 자리의 정밀도 조정 가능, 매우 큰 정밀도를 요하는 문제에 사용 가능

```python
>>> decimal.Decimal(3)
Decimal('3')

>>> decimal.Decimal('1.1')
Decimal('1.1')

 #튜플
>>> decimal.Decimal((0,(3,1,4), -2)) #튜플
Decimal('3.14')

 #무한대
>>> decimal.Decimal('infinity') #무한대
Decimal('Infinity')

>>> decimal.Decimal('NaN') #Not a Number
Decimal('NaN')
```

Decimal 객체의 연산  
```python
>>> a,b = decimal.Decimal('3.14'), decimal.Decimal('.04')
>>> a+b
Decimal('3.18')
>>> a-b
Decimal('3.10')
>>> a*b
Decimal('0.1256')
>>> a/b
Decimal('78.5')
>>> a**b
Decimal('1.046832472577719248090395663')
```

- max, min, sum 등의 내장함수 인자로 전달 가능한

> 참고 : 부동소수점의 문제  

- 부동소수점으로 표현된 수가 원래 실수를 정확히 나타내지 못하는 문제 발생
- 부동소수점 연산의 결과도 항상 동일하지 않음

> random method

- random.seed([x]) : 임의 숫자 생성기의 초기화
- random.random() : 0.0 <= F < 1.0 사이의 임의의 float 숫자를 반환
- random.uniforom(a,b) : 인자로 받은 두 값 사이의 임의의 float 숫자를 반환
- random.gauss(m,sb) : 가우스분포(정규분포)의 난수를 반환
- random.randint(a,b) : a,b 사이의 임의의 정수 반환
- random.choice(seq) : 입력받은 시퀀스 객체의 임의의 item 반환
- random.shuffle(x[,random]) : 입력받은 시퀀스 객체를 섞음
- random.randrange(x) : x 이내의 임의의 정수 리턴, 중복가능
- random.sample(seq, x) : seq 객체에서 x개 리턴, 중복불가

```python
>>> random.random()
0.3539264915279131

>>> random.uniform(4,5)
4.032628293528142

>>> for i in range(3):
...     a = random.gauss(1,1.0)
...     print(a)
-0.3308507469872488
0.48423322675838765
0.32961456819992807

>>> [random.randrange(10) for i in range(10)]
[9, 0, 8, 0, 4, 2, 2, 9, 2, 2]

>>> random.sample(range(10), 5)
[8, 3, 0, 1, 4]
```

> 임의의 시퀀스 예제

```python
>>> l = list(range(10))
>>> l
[0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
>>> [random.choice(l) for i in range(3)] #리스트 내장을 이용, 중복 가능
[2, 2, 9]
>>> random.sample(l,3) #중복 X
[1, 8, 2]
>>> l2 = list(range(10))
>>> l2
[0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
>>> random.shuffle(l2)
>>> l2
[4, 6, 0, 8, 2, 9, 1, 5, 7, 3]
```


***  
#### 더 보충해야 할 내용
- iterable 의 개념 확실하게 잡기
 - https://wikidocs.net/16068
***  





