
***
title : Python -  T아카데미 Python 강의 정리 12강
***

## 파일 시스템 - os.glob 모듈

> os.glob

- glob 모듈은 윈도우의 dir 명령어나 리눅스의 ls 명령어와 유사한 기능을 제공
 
참고 : [파이썬 os.glob 모듈](http://devanix.tistory.com/299?category=271929)

> glob.glob(path) 

- glob() 함수는 경로에 대응되는 모든 파일 및 디렉터리의 리스트를 반환합니다.
- '*'와 '?'도 사용가능하며 "["과"]"를 사용한 문자열 비교도 가능합니다.

```python
>>> from os.path import *
>>> glob.glob('*')
['DLLs', 'Doc', 'include', 'Lib', 'libs', 'LICENSE.txt', 'NEWS.txt', 'python.exe', 'pythonw.exe', 'README.txt', 'tcl', 'Tools', 'w9xpopen.exe']
>>> glob.glob('./[0-9].*')
['./1.gif', './2.txt']
>>> glob.glob('*.gif')
['1.gif', 'card.gif']
>>> glob.glob('?.gif')
['1.gif']
>>> glob.glob('*.exe')
['python.exe', 'pythonw.exe', 'w9xpopen.exe']
>>> glob.glob(abspath('.' + '\\*.exe'))  # `.`은 현재 디렉터리를 의미
['C:\\Python30\\python.exe', 'C:\\Python30\\pythonw.exe', 'C:\\Python30\\w9xpopen.exe']
```

> glob.iglob(path)

- glob과 동일 동작 수행하지만, 결과를 리스트가 아니라 이터레이터로 반환
- 한번에 모든 결과를 리스트에 담지 않으므로, 결과가 매우 많은 경우 유용하게 쓰일 수 있다.

```python
>>> glob.iglob('*')
<generator object iglob at 0x012230D0> #제너레이터 객체 리턴
>>> for i in glob.iglob('*'):
...     print (i)

DLLs
Doc
include
Lib
libs
LICENSE.txt
NEWS.txt
python.exe
pythonw.exe
README.txt
tcl
Tools
w9xpopen.exe
```

> Tree 예제

```python
>>> def traverse(dir, depth):
...     for obj in glob.glob(dir+'/*'):  #경로에 대응되는 파일 및 디렉터리 리스트 리턴
...         if depth==0:
...             prefix = '|--'
...         else:
...             prefix = '|' + ' '*depth + '+--'
...         if os.path.isdir(obj):  #디렉터리인 경우
...             print(prefix + os.path.basename(obj))
...             traverse(obj, depth+1)
...         elif os.path.isfile(obj):  #파일인 경우
...             print(prefix + os.path.basename(obj))
...         else:
...             print(prefix + 'unknown objext:', obj)

>>> traverse('./tree_test',0)
|--test1
| +--untitled2.txt
| +--untitled1.txt
|--test2
| +--test2_1
|  +--untitled2.txt
|  +--untitled1.txt
| +--untitled1.txt
```

- 예시 폴더 구조
![folder_structer](https://drive.google.com/file/d/10S3xFJKoP6nfg7Kyg4hkyIXyfeqzQ-ii/view?usp=sharing)

***  
#### 더 보충해야 할 내용
- tree 예제 파해치기
- 이미지 서치&다운로드 할때 os.path, os.glob 이용해 검색어별로 폴더에 정리하는 미니 프로젝트 작성해보기

***  





