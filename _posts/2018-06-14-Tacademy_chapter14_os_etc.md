---
title: Python -  T아카데미 Python 강의 정리 chapter_14
description:
categories:
 - tutorial
tags:
---

## 운영체제 관련

#### os 모듈

- 운영체제(OS)에서 제공되는 기본적인 기능들을 제공

> os.getcwd(), os.chdir(path)

chdir() 함수는 현재 작업 디렉터리 위치를 변경하며, getcwd()함수는 현재 작업 디렉터리의 위치를 가져올 때 쓰입니다.

```python
>>> getcwd()
'C:\\Python3'
>>> chdir('Tools')
>>> getcwd()
'C:\\Python3\\Tools'
```

> os.access(path, mode)

입력받은 <path>에 대해서 <mode>에 해당하는 작업이 가능한지의 여부를 반환합니다.  
- 모드(mode)  
 - F_OK : 해당 path의 존재 여부를 확인  
R_OK : 해당 path의 읽기 가능여부 확인  
W_OK : 해당 path의 쓰기 가능여부 확인  
X_OK : 해당 path의 실행 가능여부 확인  
  
```python
>>> access('.', F_OK)    # existence
True
>>> access('.', W_OK | X_OK | R_OK) # write, exec, read
True
```

> os.listdir(path)

해당 경로(path)에 존재하는 파일과 디렉터리들의 리스트를 반환합니다.

```python
>>> listdir('.')
['DLLs', 'Doc', 'include', 'Lib', 'libs', 'LICENSE.txt', 'NEWS.txt', 'python.exe', 'pythonw.exe',
'README.txt', 'tcl', 'Tools', 'w9xpopen.exe']
```

> os.mkdir(path[, mode])

`path`에 해당하는 디렉터리를 생성합니다.
```python
>>> mkdir('test1')
>>> listdir('.')
['DLLs', 'Doc', 'include', 'Lib', 'libs', 'LICENSE.txt', 'NEWS.txt', 'python.exe', 'pythonw.exe',
'README.txt', 'tcl', 'test1', 'Tools', 'w9xpopen.exe']
```


> os.makedirs(path[, mode])

인자로 전달된 디렉터리를 재귀적으로 생성합니다.  
이미 디렉터리가 생성되어 있는 경우나 권한이 없어 생성할 수 없는 경우는 예외를 발생합니다.  

```python
>>> makedirs('test2/sub1/sub2/leaf')
>>> listdir('test2/sub1/sub2')
['leaf']
>>> makedirs('test2/sub1/sub2/leaf') # 이미 존재하는 디렉터리를 생성하는 경우 예외 발생
Traceback (most recent call last):
File "<pyshell#18>", line 1, in <module>
makedirs('test2/sub1/sub2/leaf')
File "C:\Dev\Python3\lib\os.py", line 152, in makedirs
mkdir(name, mode)
WindowsError: [Error 183] 파일이 이미 있으므로 만들 수 없습니다: 'test2/sub1/sub2/sub3'
```

> os.remove(path), os.unlink(path)

파일을 삭제 합니다.
```python
>>> remove('test.txt')
아래와 동일
>>> unilnk('test.txt')
```

> os.rmdir(path)

디렉터리를 삭제합니다. 단, 디렉터리는 비어있어야만 합니다.
```python
>>> mkdir('test1')
```

> os.utime(path, times)

경로에 해당하는 파일에 대해 액세스 시간(access time)과 수정 시간(modified time)을 times로
수정합니다. times가 None일 경우는 현재 시간으로 수정합니다. (유닉스의 touch 명령어와 유사)

```python
>>> stat('readme.txt')
nt.stat_result(st_mode=33206, st_ino=281474976762465, st_dev=0, st_nlink=1, st_uid=0,
st_gid=0, st_size=6788, st_atime=1321797957, st_mtime=1315094610, st_ctime=1315094610)
>>> utime('readme.txt', None)
>>> stat('readme.txt')
nt.stat_result(st_mode=33206, st_ino=281474976762465, st_dev=0, st_nlink=1, st_uid=0,
st_gid=0, st_size=6788, st_atime=1321950244, st_mtime=1321950244, st_ctime=1315094610)
```

> os.stat(path)  
  
경로에 해당하는 정보를 얻어옵니다.
아래의 예제와 같이 순차적으로 protection, inode, device, link, user id, group id, size,
last access time, last modified time, last change time 등을 나타냅니다.
(stat() 함수 결과 중 일부는 유닉스/리눅스 시스템에만 해당되는 것도 있습니다)
```python
>>> stat('python.exe')
nt.stat_result(st_mode=33279, st_ino=281474976762468, st_dev=0, st_nlink=1, st_uid=0,
st_gid=0, st_size=26624, st_atime=1321851747, st_mtime=1315097496, st_ctime=1315097496)
```

> os.walk(top[, topdown=True[, onerror=None[, followlinks=False]]])

top으로 지정된 디렉터리를 순회하며 경로, 디렉터리명을 순차적으로 반환합니다.  
다음의 구조로 test_walk, a, b 디렉터리를 만들어 놓고 walk를 실행

```python
>>> for path,dirs,files in walk('test_walk'):
...     print(path, dirs, files)

test_walk ['a', 'b'] []
test_walk\a [] []
test_walk\b [] ['readme.txt']
```
- topdown이 False로 설정된 경우에는 다음과 같이 디렉터리의 끝에서부터 위로 탐색

```python
>>> for path,dirs,files in walk('test_walk', topdown=False):
...     print(path, dirs, files)
   
test_walk\a [] []
test_walk\b [] ['readme.txt']
test_walk ['a', 'b'] []
```


> os.pipe()

파이프를 생성합니다. 함수를 실행하면 읽기, 쓰기 전용 파이프의 파일 디스크립터가 반환됩니다.  
(※ 파이프(pipe)란 프로세스 간 통신을 위한 공유 영역입니다. 여러 프로세스 간에 정보를 주고 받기
위해 만들어지는 공간이며, 하나의 프로세스가 정보를 쓰면 다른 프로세스에서 읽을 수 있습니다)

```python
>>> pipe()
(3, 4)
```


> os.fdopen(fd[, mode[, bufsize]])
 
파일 디스크립터를 이용해 파일 객체를 생성합니다.
(※ fdopen은 'from os import *'로 import가 안됩니다. fdopen의 경우 'from os import fdopen'으로 따로 import 해주어야 합니다)

```python
>>> from os import *
>>> from os import fdopen
>>> r,w = pipe()
>>> rd = fdopen(r)
>>> rd
<_io.TextIOWrapper name=3 mode='r' encoding='cp949'>
```

> os.startfile(path[, operation])
path를 os에서 지정된 프로그램으로 실행합니다.
또한 <operation>으로 명시적으로 수행할 프로그램을 지정할 수 있습니다.

참고 : [os 모듈](http://devanix.tistory.com/304)

## sys 모듈

> sys.argv

파이썬 스크립트로 넘어온 입력인자(argument)들의 리스트.
- 아래 예제와 같이 0번째는 스크립트 이름이 있으며, 그 이후부터 인자들이 설정
[ test_argv.py 예제코드 ]

```python
import sys

print("argv size :", len(sys.argv))

for i, arg in enumerate(sys.argv):

        print(i, arg)
```
 
[ 실행 결과 ]
```
> test_argv.py arg1
argv size : 2
0 C:\Python30\test_argv.py
1 arg1
```

> sys.exc_info()

현재 발생한 예외정보를 튜플로 반환 (예외가 없는 경우 None을 반환)

[ 예외가 없는 경우 ]
```python
>>> import sys
>>> sys.exc_info()
(None, None, None)
```

[ 예외가 발생한 경우 ]

```pyhton
>>> try:
...     1/0
... except:
...     exc_class, val, tb_ob = sys.exc_info()
...     print(exc_class)
...     print(val)
...     print(tb_ob)
...     print(dir(tb_ob))
...     print(tb_ob.tb_lineno)
<class 'ZeroDivisionError'>
division by zero
<traceback object at 0x00FFAAF8>
['tb_frame', 'tb_lasti', 'tb_lineno', 'tb_next']
2
```

> sys.exit([arg])

프로세스를 종료시킵니다. (arg가 0인 경우에는 정상 종료되며, 0이 아닌 경우에는 비정상종료 처리)

 
> sys.path

모듈을 찾을 때 참조하는 경로를 나타냅니다.

```python
>>> sys.path
['C:\\Python3\\Lib\\idlelib', 'C:\\WINDOWS\\system32\\python32.zip',
'C:\\Python3\\DLLs', 'C:\\Python3\\lib', 'C:\\Python3', 'C:\\Python3\\lib\\site-packages']
```

참고 : [sys 모듈](http://devanix.tistory.com/300?category=271929)

## 쓰레드 (Thread)

> Thread란?

파이썬 프로그램은 기본적으로 하나의 쓰레드(Single Thread)에서 실행된다. 
즉, 하나의 메인 쓰레드가 파이썬 코드를 순차적으로 실행한다. 코드를 병렬로 실행하기 위해서는 별도의 쓰레드(Subthread)를 생성해야 하는데, 
파이썬에서 쓰레드를 생성하기 위해서는 threading 모듈 (High 레벨) 혹은 thread 모듈 (Low 레벨)을 사용할 수 있다. 
일반적으로 쓰레드 처리를 위해서는 thread 모듈 위에서 구현된 threading 모듈을 사용하고 있으며, 
thread 모듈은 (deprecate 되어) 거의 사용하고 있지 않다.

파이썬(오리지날 파이썬 구현인 CPython)은 전역 인터프리터 락킹(Global Interpreter Lock) 때문에 
특정 시점에 하나의 파이썬 코드만을 실행하게 되는데, 이 때문에 파이썬은 실제 다중 CPU 환경에서 
동시에 여러 파이썬 코드를 병렬로 실행할 수 없으며 인터리빙(Interleaving) 방식으로 코드를 분할하여 실행한다. 
다중 CPU 에서 병렬 실행을 위해서는 다중 프로세스를 이용하는 multiprocessing 모듈을 사용한다.

> threading 모듈

파이썬에서 쓰레드를 실행하기 위해서는, threading 모듈의 threading.Thread() 함수를 호출하여
 Thread 객체를 얻은 후 Thread 객체의 start() 메서드를 호출하면 된다. 
 서브쓰레드는 함수 혹은 메서드를 실행하는데, 일반적인 구현방식으로 (1) 쓰레드가 실행할 함수 혹은 메서드를 작성하거나 
 또는 (2) threading.Thread 로부터 파생된 파생클래스를 작성하여 사용하는 방식 등이 있다.

먼저 첫번째 함수 및 메서드 실행 방식은 쓰레드가 실행할 함수 (혹은 메서드)를 작성하고 
그 함수명을 hreading.Thread() 함수의 target 아큐먼트에 지정하면 된다. 
예를 들어, 아래 예제에서 sum 이라는 함수를 쓰레드가 실행하도록 threading.Thread() 함수의
 파라미터로 target=sum 을 지정하였다. 여기서 한가지 주의할 점은 target=sum() 처럼 지정하면,
 이는 sum() 함수를 실행하여 리턴한 결과를 target에 지정하는 것이므로 잘못된 결과를 초래할 수 있다. 
 만약 쓰레드가 실행하는 함수(혹은 메서드)에 입력 파라미터를 전달해야 한다면, 
 args (혹은 키워드 아규먼트인 경우 kwargs)에 필요한 파라미터를 지정하면 된다.
 args는 튜플로 파라미터를 전달하고, kwargs는 dict로 전달한다. 아래 예제에서 
 sum() 함수는 두 개의 파라미터를 받아들이기 때문에 "args=(1, 100000)" 와 같이 입력파라미터를 지정하였다.

```python
import threading
 
def sum(low, high):
    total = 0
    for i in range(low, high):
        total += i
    print("Subthread", total)
 
t = threading.Thread(target=sum, args=(1, 100000))
t.start()
 
print("Main Thread")
```

threading.Thread 로부터 파생클래스를 만드는 방식은 Thread 클래스를 파생하여 
쓰레드가 실행할 run() 메서드를 재정의해서 사용하는 방식이다. Thread 클래스에서 run() 메서드는
 쓰레드가 실제 실행하는 메서드이며, start() 메서드는 내부적으로 이 run() 메서드를 호출한다. 
 예를 들어, 아래 예제(A)는 getHtml() 라는 함수를 사용한 방식인데 이를 예제(B)와 같이 파생클래스를 
 사용하는 방식으로 바꿔 쓸 수 있다. 예제(B)에서 t.start()는 HtmlGetter 클래스에서 재정의된 run() 메서드를 호출하게 된다.

예제(A)
```python
import threading, requests, time
 
def getHtml(url):
    resp = requests.get(url)
    time.sleep(1)
    print(url, len(resp.text), ' chars')
 
t1 = threading.Thread(target=getHtml, args=('http://google.com',))
t1.start()
 
print("### End ###")
```

예제(B)
```python
import threading, requests, time
 
class HtmlGetter (threading.Thread):
    def __init__(self, url):
        threading.Thread.__init__(self) 
        self.url = url
 
    def run(self):
        resp = requests.get(self.url)
        time.sleep(1)
        print(self.url, len(resp.text), ' chars')
 
t = HtmlGetter('http://google.com')
t.start()
 
print("### End ###")
```

> 데몬 쓰레드

Thread 클래스에서 daemon 속성은 서브쓰레드가 데몬 쓰레드인지 아닌지를 지정하는 것인데, 
데몬 쓰레드란 백그라운드에서 실행되는 쓰레드로 메인 쓰레드가 종료되면 즉시 종료되는 쓰레드이다.
 반면 데몬 쓰레드가 아니면 해당 서브쓰레드는 메인 쓰레드가 종료할 지라도 자신의 작업이 끝날 때까지 계속 실행된다.

***  
#### 더 보충해야 할 내용
- Thread 개념 잡기
- Thread 활용 예시 보면서 감잡기
***  





