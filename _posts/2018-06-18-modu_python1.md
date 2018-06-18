---
title: Python - 모두의 파이썬 정리 1
description:
categories:
 - tutorial
tags:
---

## 문자열로 된 파이썬 코드 실행

#### eval 함수
`eval(expression[, globals[, locals]])`
여기서 global은 전역 영역 사전, local은 지역 영역 사전이다. 이들 인수는 선택적이다.
eval() 내장 함수는 문자열로 된 파이썬 식(Expression) 을 실행한다.
※ evaluation = "값을 구함" 이란 뜻.

```python
>>> a = '3 + 4' 
>>> eval(a) 
7 
>>> b = eval(a) 
>>> b 
7
```

#### exec 함수
`exec code [ in globals[, locals]]`
exec는 문자열로 된 문(Statement)을 수행한다.
```
>>> cmd = 'a = 3 + 4'
>>> exec(cmd)
>>> a          # a 라는 변수가 생김.
7
```

#### Compile 함수
compile (string, filename, kind)
여기서 string은 코드문자열, filename은 코드 문자열이 저장된 파일명, kind는 컴파일할 코드의 종류
`exec`라면 여러 개의 문들을 컴파일하고,`eval`이면 하나의 식을, `single`이면 하나의 대화적 문을 컴파일한다.
`compile()` 내장함수는 문자열을 컴파일하여 파이썬 코드를 리턴한다.

```python
>>> cmd = 'print 3333*23' 
>>> cc = compile(cmd, '<string>', 'exec') 
>>> exec(cc) 
76659 

>>> cmd2 = '33 + 44' 
>>> cc2 = compile(cmd2, '<string>', 'eval') 
>>> eval(cc2) 
77
```

