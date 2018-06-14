---
title: Python -  T아카데미 Python 강의 정리 chapter 9
description:
categories:
 - tutorial
tags:
---


## 문자열 method

> str

- 문자열을 다루는 기본 클래스 (내장 클래스임)  
- capitlize()
- count(keyword, [start, [end]])  

```python
>> `python is powerful'.count('p')
2
>> `python is powerful'.count('p',5) #[5:]로 슬라이싱한 효과
1
>> `python is powerful'.count('p',0,-1) #[0:-1]로 슬라이싱한 효과
2
```

> encode  

- str 클래스는 기본적으로 모두 유니코드
- 인코딩이란 : 특정 문자 집한 안의 문자들을 컴퓨터 시스템에서 사용할 목적으로 일정한 범위 안의 정수들로 변환하는 방법
- encode를 거치면 encoding이 있는 바이너리로 변환  

참고 : [Python에서 한글 인코딩과의 싸움](http://ifyourfriendishacker.tistory.com/5)

```python
>> '가나다'.encode('cp949') #윈도우에서 사용하는 'CP949'로 변환
b'\xb0\xa1\xb3\xaa\xb4\xd9'

>> '가나다'.encode('cp949') # UTF-8 로 변환
b'\xea\xb0\x80\xeb\x82\x98\xeb\x8b\xa4'
```

> encode([encoding, [error]])

```python
>> '가나다'.encode('latin1','strict')
---------------------------------------------------------------------------
UnicodeEncodeError                        Traceback (most recent call last)
<ipython-input-1-d4ec8ef41309> in <module>()
----> 1 '가나다'.encode('latin1','strict')

UnicodeEncodeError: 'latin-1' codec can't encode characters in position 0-2: ordinal not in range(256)
```

> endswith()  

```python
>> 'python is powerful'.endswith('ful')
True
>> 'python is powerful'.endswith('ful',5)
True
>> 'python is powerful'.endswith('ful',5,-1) #[5:,-1]로 슬라이싱한 효과, ~powerfu 에서 잘림
False
>> 'python is powerful'.endswith(('m','l')) #m이나 l로 끝나는지
True
```

> expandtabs([tabsize]) : 필요할 때 알아보자

> find(keyword, [start,[end]]) : 키워드를 문자열에서 찾음

> index(keyword, [start,[end]]) : find와 똑같이 동작하지만 키워드 못찾으면 에러 발생시킴

```python
>> 'python is powerful'.find('p')
0
>> 'python is powerful'.find('p',5,-1)
10
>> 'python is powerful'.find('pa')
-1
>> 'python is powerful'.index('pa')
---------------------------------------------------------------------------
ValueError                                Traceback (most recent call last)
<ipython-input-7-45cb52e28ce2> in <module>()
----> 1 'python is powerful'.index('pa')

ValueError: substring not found
```

> isalnum() : 문자열에 숫자, 문자를 제외한것이 존재하면 False 반환

> isalpha() : 알파벳 이외의 것이 존재하면 False

> islower() : 모든 문자열이 소문자이면 True (숫자 상관없음)

> isspace() : 모두 공백문자로 이루어져 있으면 True

> istitle() : 모든 문자열이 `대문자(한글자)+소문자(나머지)` 형태여야 True

> isupper() : 모두 대문자이면 True

> isdecimal(), isdigit() : 10진수로 이루어져 있으면 True

> isnumeric() : 숫자 여부 체크

> join(sequence)  
- 리스트에 특정 구분자를 추가해 문자열로 반환
- ~~조인은 이터러블 가능한 입력인 시퀀스형 변수로 지정된 문자열로 연결해서 반환~~ (무슨말인지 파악하기)>>

> lower() : 모든 영문자를 소문자로 반환~~

> lstrip() : 문자열의 왼쪽에서 공백이나 특정 문자열 제거
```python
>> '\t python'.lstrip()
'python'   #\t 가 제거됨
```

> rstip() : 문자열의 오른쪽에서 공백이나 특정 문자열 제거
```python
>> '>>> python <<<'.rstrip('<')
'>>> python ' 
```

> maketrans() : ~~필요할 때 찾아보기~~

> partition(separator) : 문자열을 separator 기준으로 나눔
```python
>> 'python is powerful'.partition('is')
('python', 'is', 'powerful')
```

> replce(old, new, [count]) : old를 new로 대체, count만큼 수행
```python
>> 'python is powerful'.replace('p','P',1)
'Python is powerful' #1번만 바뀜
```

> rfind(keyword, [start, [end]]) : find와 비슷한데 오른쪽(뒤)부터 수행
> rindex, rpartition 도 마찬가지

> rsplit(separator, [maxsplit]) : sperator 기준으로 뒤에서부터 나눔
```python
>> 'python is powerful'.rsplit()  #() 비면 공백 기준
['pyhton','is','powerful']
>> 'python is powerful'.rsplit('',1)  #() 비면 공백 기준
['pyhton is','powerful']
```

> rstrip : lstrip과 마찬가지, 우측 기준

> split(separator, [maxsplit]) : sperator 기준으로 나눔, rsplit과 비슷
```python
>> 'python is powerful'.rsplit('',1)  #() 비면 공백 기준
['pyhton', 'is powerful']
```

> startswith : endswith와 반대

> strip([chars]) : 문자열 양쪽 끝을 잘라냄. chars가 지정되면 chars의 모든 조합 제거
```python
>> '>>> python is powerful <<<'.strip('<>')
python is powerful
```

> swapcase() : 대소문자 swap

> title() : 첫문자는 대문자로, 나머지는 소문자로 변환

> upper() : 대문자로 변환


## 정규표현식

- 특정한 규칙을 가진 문자열을 표현하는데 사용되는 형식 언어
- 주어진 패턴으로 문자열을 검색/치환하는데 사용

> 정규표현식 문법

- `.` : 개행문자를 제외한 1자
- `^` : 문자열의 시작
- `$` : 문자열 종료
- `[]` : 문자의 집합
 - [abcd] 와 [a-d]는 의미가 같다
 - [$] : 순수 $를 의미
 - [^5] : 5를 제외한 모든 문자
- `|` : OR
- `()` : 괄호 안의 정규식을 그룹으로 만듬
 - 직접 ()를 매칭시키려면 \(\) 처럼 써줘야함
- `*` : 문자가 0회 이상 반복
- `+` : 문자가 1회 이상 반복
- `?` : 문자가 0 또는 1회 반복
- `{m}` : 문자가 m회 반복
- `{m,n}` : 문자가 m회부터 n회까지 반복되는 모든 경우
- `{m,}` : 문자가 m회부터 무한 반복되는 모든 경우

> 정규표현식 예제  

- ~~강의 다 본 뒤 pdf 보고 적기~~

> escape문자열  

- ~~강의 다 본 뒤 pdf 보고 적기~~
  
> re모듈  

- 예제 적어두고 필요할 때 찾아서 쓰면 될것같음

***  
#### 더 보충해야 할 내용
- 실제 사용 예는 15강까지 다 보고 필요한 부분 찾아서 적을것  

***  





