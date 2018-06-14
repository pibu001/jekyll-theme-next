
***
title : Python -  T아카데미 Python 강의 정리 3
***

## 모듈

> 모듈을 사용하는 이유

- 코드 재사용성
- 코드를 이름공간으로 구분하고 관리할 수 있음
- 다양한 모듈 지원되고 있음 (string, date, time, decimal, random, file, os, sys...)

> import

- 모듈을 현재 이름공간으로 가져오는 역할
- dir() 함수로 모듈에 어떤 함수, 데이터가 들어있는지 알 수 있음

```python
>> dir(math)
['__doc__',
 '__file__',
 '__loader__',
 '__name__',
 '__package__',
 '__spec__',
 'acos',
 'acosh',
 'asin',
 'asinh',
...]
```

> 모듈 만들기

- 큰 프로젝트의 경우 모듈 단위로 일을 진행하기도 함
- <모듈이름>.py

- from <모듈> import <attribute> : 모듈 안에 정의된 attribute중 이름에 해당하는 attribute를 현재 이름공간으로 import
  - 이미 이름공간에 있는 명칭이라면 이전에 있던 함수가 사라질 수도 있으므로 주의해서 사용
- from <모듈> import * : `_`로 시작하는 attribute를 제외하고 모든 attribute를 현재 이름공간으로 import
- import <모듈> as <별칭> : 모듈 명을 별칭으로 변경하여 import

> 모듈 import 파헤치기

- sys.path에 등록된 디렉토리에서 모듈을 찾음
- 모듈에 바이트코드가 있으면 이를 import
- 만약 바이트코드가 없다면 해당 모듈의 인터프리터를 이용해 바이트코드로 만듬
  - 바이트코드는 일종의 중간파일
  - 모듈파일이 `simple.py` 일때 `import simple` 실행하면 `simple.pyc` 라는 바이트코드 생성
  - pyc 파일이 생성된 다음 import 실행하면 별도의 인터프리킹 없이 attribute를 현재 이름공간으로 가져오거나 모듈의 이름을 현재 이름공간으로 가져옴
  - 해당 코드를 메모리에 로딩한 뒤 모듈의 코드가 실행됨
- 한번 메모리에 로딩되면 프로그램이나 파이썬 인터프리터가 끝나기 전까지 변경되지 않음

> 직접 실행했을 때 import 할 경우와 다르게 동작하려면?

- __name__ 어트리뷰트로 이를 구분할 수 있다. __name__은 모듈 자신의 이름
- 모듈이 직접 실행되면 __name__은 '__main__'

```python
if __name__ == '__main__':
  print("모듈 직접 실행")
else:
  print("import 함")
```

> 패키지

- 모듈의 모음. 모듈의 이름공간을 구조화 하는 방법
- package의 디렉터리에는 `__init__.py`가 존재. 패키지를 초기화하는 코드들이 들어있음

- `import xml` 을 수행하면 xml 디렉터리의 모듈 또는 xml 디렉터리의 `__init__.py`에 정의된 것들만 참조할 수 있다.

- `from .. import formats` 하면 부모 디렉터리
- `from . import echo` 하면 현재 디렉터리


***

#### 더 보충해야 할 내용
- 패키지 구조, import 방법 더 상세히 알기
- 바이트 코드 부분
***