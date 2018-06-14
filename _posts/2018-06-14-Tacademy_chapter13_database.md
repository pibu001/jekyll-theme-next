---
title: Python -  T아카데미 Python 강의 정리 chapter_12_database
description:
categories:
 - tutorial
tags:
---

## 데이터베이스

> SQLite3

- 디스크 기반의 가벼운 데이터베이스 라이브러리
- 서버가 필요하지 않아 자원을 적게 사용
- 트랜젝션 지원, 예기치 못한 운영체제상의 문제 or 비정상 종료시에도 데이터 무결성 보장

> SQLite3 모듈 함수

- sqlite3.connect(database) : SQLite3 DB에 연결
 - sqlite3.connect(database[timeout, isolation_level, detect_types, factory])
- sqlite3.complete_statement(sql) : 세미콜론으로 끝나는 SQL 문장에 대해 True 반환(문장이 올바른지는 확인안함)
- sqlite3.register_adapter(tpye,callable) : 사용자 정의 파이썬 자료형을 SQLite3에서 사용하도록 등록
- sqlite3.register_converter(typename, callable) : SQLite3에 저장된 자료를 사용자 정의 자료형으로 변환하는 함수를 등록

> Connection 클래스

- 연결된 DB를 동작시키는 역할을 함
- Connection.cursor() : Cursor 객체 생성
- Connection.commit() : 현재 트랜젝션의 변경내역을 DB에 반영(commit)
- Connection.rollback() : 트렌젝션 변경내용을 DB에 반영하지 않음
- Connection.close() : DB 연결 종료
- Connection.isolation_level : 트랜젝션 격리 수준 확인, 설정


```python3
>>> import sqlite3

>>> conn = sqlite3.connect('test_sqlite3_2.db') #데이터베이스에 대한 연결 설정
	# 모듈을 사용하려면 먼저 데이터베이스를 나타내는 Connection 객체를 만들어야 함
>>> curs = conn.cursor() #데이터 전달을 위한 cursor 생성

>>> curs.execute('create table employee(name, age)') #execute는 sql문을 입력받아 수행함
<sqlite3.Cursor at 0x7fe570e8fab0>
>>> curs.execute('insert into employee values("Ali","28")')
<sqlite3.Cursor at 0x7fe570e8fab0>

>>> values = [('Brad',54), ('Ross', 34), ('Muhammad', 28), ('Bilal', 44)]
>>> curs.executemany('insert into employee values(?,?)', values) #여러 값 실행
<sqlite3.Cursor at 0x7fe570e8fab0>

#레코드 조회
>>> curs.execute('select * from employee')
<sqlite3.Cursor at 0x7fe570e8fab0>
>>> curs.fetchall()
[('Ali', '28'), ('Brad', 54), ('Ross', 34), ('Muhammad', 28), ('Bilal', 44)]
또는
>>> curs.execute('select * from employee')
>>> for row in curs:
...     print(row)
('Ali', '28')
('Brad', 54)
('Ross', 34)
('Muhammad', 28)
('Bilal', 44)

>>> conn.commit()  #변경사항 커밋, commit을 하지 않으면 변경 사항이 DB에 반영되지 않음
>>> conn.close()  #데이터베이스 연결 닫기
```

> 사용자가 임의로 정렬 방식을 변경하는 경우

- 함수 만들고 create_collation으로 함수 등록, ~~필요할 때 찾아보기~~

> 내장/집계 함수

- abs(x) : 절대값 리턴
- length(x) : 문자열 길이 리턴
- lower(x) : 소문자 리턴
- upper(x) : 대문자 리턴
- min(...) : 최소값 리턴
- max(...) : 최대값 리턴
- random(*) : 임의의 정수 반환
- count(x) : NULL이 아닌 튜플의 개수를 반환
- count(*) : 튜플의 개수 반환
- sum(x) : 합을 반환

> 자료형

- SQLite3 자료형과 대응되는 Python 자료형

![자료형 대응](https://drive.google.com/file/d/1ArftwoNrhGpZzn4QH5JeZ4b7dBesYP1s/view?usp=sharing)

```python
>>> cur.execute("create table tbl_1(name TEXT, age INTEGER);")
>>> cur.execute("create table tbl_2(name str, age int);")
위 코드와 아래 코드는 실행 결과가 같다
```

> 데이터베이스 덤프 만들기  

- ~~필요할 때 다시 찾아보기~~


> #### 명령어 프롬프트에서 SQL 관리하기  

- 입력받은 SQL 구문 실행
-  Select 문을 입력받은 경우 fetch를 사용해서 결과 출력

```python
import sqlite3
import sys

if len(sys.args) == 2:
    path = sys.argv[1]
else:
    path = ":memory:"

con = sqlite3.connect(path)
con.isolation_level = None  #오토커서 ?? 확인할것
cur = con.cursor()

while True:
    sql = input(">>").strip()
	if sql == "":
	    break
	if sqlite3.complete_statement(sql):
	    try:
		    cur.exectue(sql)
			if sql.upper().startswith('select'):
			    print(cur.fetchall())
			except sqlite3.Error as e:
			    print("Error:", e.args[0])
			else:
			    print("success")
		else: 
		    print("Invalid sql statement")
		
    con.close()
	print("quit")
```


참고 : [SQLite 설명](https://code.tutsplus.com/ko/tutorials/database-handling-in-python--cms-25645)  
참고 : [SQLite 설명2](http://pythonstudy.xyz/python/article/204-SQLite-%EC%82%AC%EC%9A%A9)



***  
#### 더 보충해야 할 내용
- callable : 한개 인자를 받아서 파이썬에서 사용 가능한 자료형으로 변환? -> 자세히 알아두기
- Cursor 객체?

***  





