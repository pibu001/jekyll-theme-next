
***
title : Python -  T아카데미 Python 강의 정리 7강
***

## 예외처리

> 예외처리의 몇 가지 종류

- NameError : 선언하지 않은 변수에 접근

- ZeroDivisionError : 0으로 나눔

- IndexError : 리스트 접근 가능한 인덱스 넘음

- TypeError : 지원하지 않는 연산(ex : 정수를 문자열로 나눔)

- 


> raise

- pass

> 사용자 정의 예외

- pass

> assert 구문

- pass


- 인자로 받은 조건식이 거짓인 경우 AssertionError 발생

- __debug__가 True인 경우만 assert 구문 활성화

```python
Assert <조건식>, <관련 데이터>

이 코드는 아래와 같다

if __debug__:
  if not <조건식>:
    raise AssertionError(<관련데이터>)
```

예외에 대한 정보를 전달받는 예제

```python
>> def foo(x):
..   assert type(x) == int,
..   return x * 10
  
>> ret = foo('a')
>> print(ret)
---------------------------------------------------------------------------
AssertionError                            Traceback (most recent call last)
<ipython-input-4-7e6eb70a651c> in <module>()
----> 1 ret = foo('a')

<ipython-input-3-a8078d1f215e> in foo(x)
      1 def foo(x):
----> 2     assert type(x) == int, "Input value must be integer"
      3     return x*10

AssertionError: Input value must be integer
```

> sys.exc_info()


```python
try : 
  traverse('.', 0)   #
except UnknownObjectError as e:
  print('UnknownObjectError occurs', e.obj)
except:    #지정해준 예외 이외의 모든 예외
  exc, value, tb = sys.exc_info()  #예외클래스, 예외데이터, traceback정보
  print(exc, value, tb)
  traceback.print_exc()  #현재 traceback 객체의 정보를 화면에 출력
```
  

***  
#### 더 보충해야 할 내용
- raise, assert 사용 예시 보고 어떤 경우에 사용되는지 확인할것
- glob 를 활용해 폴더 dept 파악 및 파일 위치 확인하는 예제 코드 확인할것

***  





