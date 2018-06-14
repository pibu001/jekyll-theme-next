
***
title : Python -  T아카데미 Python 강의 정리 12강
***

## 파일 시스템 - os.path 모듈

> os.path

- os.path는 파일 경로를 생성 및 수정하고, 파일 정보를 쉽게 다룰 수 있게 해주는 모듈
- `from os.path import *` 하고 나서 실행
- 운영체제에 따라 따로 파일 경로에 대한 고민을 하지 않고 동일한 코드 작성 가능

참고 : [파이썬 os.path 모듈](http://devanix.tistory.com/298)


> os.path.abspath(path)  

현재 경로를 Prefix로 하여 입력받은 경로를 절대경로로 바꿔서 반환합니다.

```python
>>> abspath('tmp')
'C:\\Python30\\tmp'
```
 

> os.path.basename(path)  

입력받은 경로의 기본 이름(base name)을 반환합니다.
abspath() 함수와 반대되는 기능을 수행한다고 볼 수 있습니다.

```python
>>> basename('C:\\Python30\\tmp')
'tmp'
>>> basename('C:\\Python30\\tmp\\test.txt')
'test.txt'
```
 
> os.path.commonprefix(path_list)  

입력받은 path_list로부터 공통적인 Prefix를 추출해서 반환합니다. 그러나 이 결과는 문자열 연산에
의한 것이기 때문에 다음의 두 번째 예제와 같이 잘못된 경로가 나올 수도 있습니다.

```python
>>> commonprefix(['C:\\Python30\\Lib', 'C:\\Python30', 'C:\\Python30\\Tools'])
'C:\\Python30'
>>> commonprefix(['C:\\Python26\\Lib', 'C:\\Python25\\Tools'])
'C:\\Python2'
```
 

> os.path.dirname(path)  

입력받은 파일/디렉터리의 경로를 반환합니다.

```python
>>> dirname('C:\\Python30\\tmp\\test.txt')
'C:\\Python30\\tmp'
>>> dirname('C:\\Python30\\tmp')
'C:\\Python30'
```
 

> os.path.exists(path)  

입력받은 경로가 존재하면 True를 반환하고, 존재하지 않는 경우는 False를 반환합니다.
리눅스와 같은 OS에서는 파일이나 디렉터리가 존재하지만 읽기 권한이 없는 경우에도,
False를 반환할 수 있습니다.
```python
>>> exists('C:\\Python30')
True
>>> exists('C:\\Python30\\Devanix')
False
```

> os.path.expanduser(path)  

입력받은 경로안의 "~"를 현재 사용자 디렉터리의 절대경로로 대체합니다.
"~"에 붙여서 <사용자명>을 붙이면 원하는 사용자 경로로 대체됩니다.
(유닉스/리눅스의 홈디렉터리를 나타내는 '~'과 동일합니다)

```python
>>> expanduser('~\\devanix')
'C:\\Documents and Settings\\Administrator\\devanix'
```


> os.path.expandvars(path)  

path안에 환경변수가 있따면 확장합니다. (환경변수는 os.environ에 정의된 것을 참조)
```python
>>> expandvars('$HOME\\temp')
'C:\\Documents and Settings\\Administrator\\temp'
>>> expandvars('$SYSTEMROOT\\var')
'C:\\WINDOWS\\var'
```

> os.path.getatime(path)  

입력받은 경로에 대한 최근 접근 시간을 반환 (반환되는 값은 epoch(1970년 1월 1일) 이후
초단위로 반환됩니다. 파일이 없거나 권한이 없는 경우 os.error 예외 발생)
```python
>>> getatime('C:\\Python30\\python.exe')
1320966393.375
# 읽을 수 있는 형식으로 보려면 다음과 같이 하면 됩니다.
>>> import time
>>> time.gmtime(getatime('C:\\Python30\\python.exe'))
time.struct_time(tm_year=2011, tm_mon=11, tm_mday=10, tm_hour=23, tm_min=6, tm_sec=33, tm_wday=3, tm_yday=314, tm_isdst=0)
```
 
> os.path.getmtime(path)  

입력받은 경로에 대한 최근 변경 시간을 반환 (파일이 없거나 권한이 없는 경우 os.error 예외 발생)
```python
>>> getmtime('C:\\Python30\\python.exe')
1320966397.453125
```

> os.path.getctime(path)  
 
입력받은 경로에 대한 생성시간을 반환 (유닉스와 같은 운영체제에서는 생성시간이 아닌
최근 변경 시간을 반환할 수도 있습니다. 파일이 없거나 권한이 없는 경우 os.error 예외 발생)
```python
>>> getctime('C:\\Python30\\python.exe')
1320966393.0625    
```
 
> os.path.getsize(path)

입력받은 경로에 대한 바이트 단위의 파일크기를 반환.
(파일이 없거나 권한이 없는 경우 os.error 예외 발생)
```python
>>> getsize('C:\\Python30\\python.exe')
26624L
```
 
> os.path.isabs(path)

경로가 절대경로이면 True를 반환하고, 그 외의 경우에는 False를 반환.
(실제 해당 경로를 검사하지는 않으며 입력받은 문자열을 가지고 판단합니다.)
```python
>>> isabs('C:\\Python30\\python.exe')
True
```
 

> os.path.isfile(path)

경로가 파일인지 아닌지 검사합니다. 파일인 경우에는 True를 반환하고, 그 외의 경우 False를 반환.
(혹은 해당 경로가 존재하지 않은 경우에는 False를 반환합니다)
```python
>>> isfile('C:\\Python30\\python.exe')
True
>>> isfile('C:\\Python26\\python.exe')
False
```
 

> os.path.isdir(path)

경로가 디렉터리인지 아닌지 검사합니다. 디렉터리인 경우에는 True를 반환하고, 그 외의 경우에는
False를 반환합니다. 혹은 경로가 존재하지 않은 경우에는 False 반환합니다.
```python
>>> isdir('C:\\Python30\\python.exe')
False
>>> isfile('C:\\Python30\\Lib')
True
```

> os.path.join(path1[,path2[,...]])

해당 OS 형식에 맞도록 입력 받은 경로를 연결합니다. (입력 중간에 절대경로가 나오면 이전에
취합된 경로는 제거하고 다시 연결합니다)

```python
>>> join('C:\\Python30', 'Script', 'test.py')
'C:\\Python30\\Script\\test.py'

>>> join('C:\\Python30', 'D:\\Test', 'test.py')
'D:\\Test\\test.py'
```
 

> os.path.normcase(path)

해당 OS에 맞도록 입력 받은 경로의 문자열을 정규화 합니다. (윈도우와 같은 경우,
아래 예제와 같이 소문자로 바꾸고 '/'를 '\\'로 변경합니다)
```python
>>> normcase('C:\\Python30\\python.exe')
'c:\\python30\\python.exe'

>>> normcase('C:/Python30/python.exe')
'c:\\python30\\python.exe'
```
 
> os.path.normpath(path)

입력 받은 경로를 정규화합니다. (현재 디렉터리(".")나 상위 디렉터리("..")와 같은 구분자를 최대한 삭제)
```python
>>> normpath('C:\\Python30/./python.exe')
'C:\\Python30\\python.exe'

>>> normpath('C:\\Python30/./../python.exe')
'C:\\python.exe'
```
 
> os.path.split(path)

입력 받은 경로를 디렉터리 부분과 파일 부분으로 나눕니다.
단순한 문자열 연산이므로 실제 파일의 존재 여부는 확인하지 않습니다.
```python
>>> split('C:\\Python30\\python.exe')
('C:\\Python30', 'python.exe')
```
 
> os.path.splitdrive(path)

입력 받은 경로를 드라이브 부분과 나머지 부분으로 나눕니다.
단순한 문자열 연산이므로 실제 파일의 존재 여부는 확인하지 않습니다.
```python
>>> splitdrive('C:\\Python30\\python.exe')
('C:', '\\Python30\\python.exe')
```
 
> os.path.splitext(path)

입력 받은 경로를 확장자 부분과 그 외의 부분으로 나눕니다.
단순한 문자열 연산이므로 실제 파일의 존재 여부는 확인하지 않습니다.
```python
>>> splitext('C:\\Python30\\python.exe')
('C:\\Python30\\python', '.exe')
```

***  
#### 더 보충해야 할 내용
- 절대경로, 상대경로 개념 파악

***  





