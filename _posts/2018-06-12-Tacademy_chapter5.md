---
title: Python -  T아카데미 Python 강의 정리 chapter 5
description:
categories:
 - tutorial
tags:
---

## 클래스

> 기본 개념

- 데이터와 데이터를 변형하는 함수를 같은 [네임스페이스](https://ko.wikipedia.org/wiki/%EC%9D%B4%EB%A6%84%EA%B3%B5%EA%B0%84)에 묶고 이를 클래스라고 지칭
- 클래스의 이름공간에 속한 멤버함수를 메서드라고 부름
- 클래스의 인스턴스 객체를 생성해서 사용
- 정보은닉 : 데이터와 클래스 내부에서 사용하는 함수를 외부에서 접근할 수 없게 함
- 추상화 : 공통 부분을 추출하여 기본 클래스로 작성하는 작업
- 다형성 : 동일한 인터페이스에 대해 각 인스턴스는 다른 작업을 수행해야 함.

- `.` : 속성접근자
 - 클래스 객체와 인스턴스 객체 모두 각 맴버변수와 멤버메서드에 접근하기 위해서 `.`을 사용
 - 인스턴스의 멤버변수와 메서드의 접근 권한은 public임(외부에서 모든 클래스의 내용을 쉽게 확인, 변경 가능)
 - 검색순서 : 인스턴스 객체 영역 -> 클래스 객체 영역 -> 전역 영역
 

> isinstance 함수

- 인스턴스가 어떤 클래스로부터 생성되었는지 확인
- 자식 클래스의 인스턴스 객체는 부모 클래스의 인스턴스로 평가됨
- 클래스 객체 정의시 상속을 받지 않더라도 암묵적으로 `object` 객체를 상속받고 있는 것임

```python
>> class Person:
..     pass

>> class Student(Person):
..     pass

>> p, s = Person(), Student()
>> print(isinstance(p, Person))
True

>> print(isinstance(s, Person))
True

>> print(isinstance(p, object))
True
```

> 생성자와 소멸자

- 생성자
 - 클래스 생성 시 초기화 작업 수행
 - 인스턴스 객체가 생성될 때 자동으로 호출
 - __init__()
- 소멸자
 - 인스턴스 객체의 참조 카운터가 0이 될 때 호출
 - __del__()

```python
>> class Myclass: 
..     def __init__(self, value):
..         self.value = value
..         print("Class 생성! 값 : ", value)
..         
..     def __del__(self):
..         print("Class is deleted")
        
>> def foo():
..     a = Myclass(10)
    
>> foo()
Class 생성! 값 :  10
Class is deleted
```

> 정적(static) 메서드  

- 인스턴스 객체를 통하지 않고, 클래스를 통해 직접 호출할 수 있는 method
- self 인자 필요X

> 클래스 메서드

- 클래스 영역의 데이터에 직접 접근 할 수 있는 메소드
- 첫 인자로 클래스 객체가 전달

## 연산자 오버로딩(Operator Overloading)
- 인스턴스 객체끼리 서로 연산을 할 수 있도록 기존에 있는 연산자의 기능을 바꾸어 중복으로 정의하는 것을 말함
- `__sub__` 와 같이 정의함. 연산자 중복을 위해 미리 정의한 특별함 method

```python
>> class NumBox:
   def __init__(self, num):
       self.Num = num
    
>> n = NumBox(40)
>> n + 100
Traceback (most recent call last):
  File "<pyshell#5>", line 1, in <module>
    n + 100
TypeError: unsupported operand type(s) for +: 'NumBox' and 'int'
```
인스턴스 객체 n에 `+` 연산자를 사용해 100을 더하려는 코드가 보이는데 
이는 지원되지 않는 연산 타입이므로 NumBox와 int간의 연산을 수행하기 힘들다.  
연산자 오버로딩이란 기법을 이용하면 + 연산자로 인스턴스 객체를 더할 수 있게 된다.  
파이썬에서는 인스턴스 객체의 연산을 위해 여러가지 연산자를 미리 정의해두었다.

![연산자 오버로딩](https://drive.google.com/file/d/12ku7F3_9baFgwXz3Tnb5nuirQe7Ov4qg/view?usp=sharing)

파이썬에서 미리 정의된 함수를 중복 정의하여 우리가 정의한 동작을 수행하게 할 수 있다.  
아래 예제에서는 +와 - 연산자를 오버로딩하여 인스턴스 객체에 연산자를 사용한다.

```python
>> class NumBox:
   def __init__(self, num):
       self.Num = num
   def __add__(self, num):
       self.Num += num
   def __sub__(self, num):
       self.Num -= num

>> n = NumBox(40)
>> n + 100
>> n.Num
140
>> n - 110
>> n.Num
30
```

`n+100`은 사실 우리가 중복 정의한 함수가 호출되는 것이다.  
이는 `n.__add__(100)` 과 같다.  

## 상속

- 부모 클래스의 모든 속성(데이터, 메소드)를 자식 클래스로 물려줌
- 클래스의 공통 속성을 부모클래스에 정의하고 자식 클래스에는 특화된 메서드와 데이터 정의

- 장점
   - 클래스마다 동일 코드가 작성되는것을 방지
   - 유지보수 용이
   - 각 개별 클래스에 특화된 기능을 공통된 인터페이스로 접근 가능
   
 
 
 
 한개 이상 다중상속 받는 경우 `Student(Person, Human)` 처럼 `,`로 구분
 
 - `issubclass(자식 클래스, 부모 클래스)` : 두 클래스가 상속관계인지 확인
   
   
> 상속관계 검색의 원칙

클래스객체와 인스턴스객체의 이름공간에서는  
[인스턴스객체영역 -> 클래스객체영역 -> 전역영역] 이와 같은 규칙으로 멤버변수나 함수의 이름을 찾는다.  

여기서 클래스간의 상속관계가 포함되면 아래와 같이 규칙이 확장된다.  
[인스턴스객체영역 -> 클래스객체간 상속을 통한영역(자식클래스영역 -> 부모클래스영역) -> 전역영역]

이러한 규칙을 "상속관계 검색의원칙(Princeples of the inheritance search)"이라고 한다.

즉, 클래스의 상속관계에서 속성(멤버데이터, 메서드)의 이름을 검색할때 개별적으로 독립된 영역을 가지고 있는 클래스간의 상속관계 순서로 이름을 찾는다. 

또한 자식클래스가 상속받은 멤버 메서드에 대해서 재정의를 하지 않거나 멤버데이터에 새로운값을 할당하지 않은 경우, 
자식클래스 내부의 이름공간에 그 데이터와 메서드를 위한 저장공간을 생성하는 대신에 
단순히 부모클래스의 이름공간에 존재하는 데이터와 메서드를 참조한다.

이렇게 하는 이유는 중복된 데이터와 메서드를 최소화하여 메모리사용의 효율성을 높이기 위해서이다.

출처: http://hwangyoungjae.tistory.com/102 



***
#### 더 보충해야 할 내용
- 정적메서드, 클래스메서드 더 자세히 파악할것, 차이점은?
- 연산자 중복 자세히 알아볼것
 - http://hwangyoungjae.tistory.com/101?category=643693
- 상속관계 검색의 원칙 부분 쉽지 않음

***