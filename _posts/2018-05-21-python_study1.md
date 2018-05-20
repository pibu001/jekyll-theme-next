---
title: Python 스터디 1
description: ipythton 사용 및 파이썬 용어
categories:
 - tutorial
tags:
---

# 파이썬 사용해보기

**파이썬 프로젝트 폴더에서 아래 명령어 실행**  
> projects/python 폴더 생성 후 여기서 작업

```
(fc-python) ➜  Python git:(master) ✗ ipython
Python 3.6.5 (default, May 17 2018, 17:08:07)
Type 'copyright', 'credits' or 'license' for more information
IPython 6.4.0 -- An enhanced Interactive Python. Type '?' for help.

In [1]:
```

> Python버전이 3.6.5으로 정확히 출력되는지 확인



## 각종 용어

**리터럴**  
변하지 않는 고정된 데이터 자체의 표현  

- 5 (정수형 데이터)
- "Fastcampus" (문자열 데이터)
- 1.4937 (부동소수점 데이터)

**표현식(expression)**  
값을 의미하는 표현 또는 값을 반환하는 표현

```python
>>> sec = 60
>>> 365*24*sec	# 표현식
525600				# 정수 525600의 리터럴 값
```

**구문(statement)**  
값의 의미를 지니지 않으며, 어떠한 목적을 수행하는 코드

```python
>>> for char in '안녕하세요':		# 구문 (제어문)
...   print(char)
...
안
녕
하
세
요
```
