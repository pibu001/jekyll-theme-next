---
title: Python -  T��ī���� Python ���� ���� chapter 3 and 4
description:
categories:
 - tutorial
tags:
---


## �Լ� 

> �Լ���?

- �������� ����(Statement)�� �ϳ��� ������
- ���α׷��� ������, ���������� �������
- �Ը� ū ���α׷��� �����ϴµ� �ʿ��� ��� �ٿ���

> �Լ� ����

- �Լ��� �����ϸ� �޸𸮿� �Լ� ��ü�� ������
- �Լ� ��ü�� ����Ű�� ���۷����� ����
- �Լ��� �̸��� �Լ��� ������ �� �Լ� ��ü�� �����ϴ� ���۷�����
- �Լ� ���۷����� �ٸ� ������ �Ҵ� �� �� ����

```python
> def Times(a,b):
... return a*b
> Times(10,10)
100
> myTimes = Times
> r = myTimes(10,10)
> r
100
```

�Լ� ��ü�� ����Ǵ� ���� �ƴ϶� ���۷����� �����

> return

- return�� ���� �������� ���� Ʃ�÷� ��� ���� ������
- return�� ������� �ʰų� return�� ���� ���� �Լ��� �����  

> ���̽� �Լ����� �μ� ����

- Scoping rule
  
  - Name Space
    - �Լ� ���� : Local scope
	- �Լ� �� ���� ���� : Global scope
	- ���̽� ��ü���� ������ ���� : Bulit-in Scope
	
  - LGB ��Ģ : Local -> Global -> Built-in ������ ã�� 
  - `global`�� ���� ������ ���� ���� ������ ���� ����
  
> ���̽� �μ� ���
 
 - �⺻ �μ� �� : �Լ� ȣ��� �μ� �������� �ʾƵ� �⺻ ���� �Ҵ�ǵ��� �ϴ� ���
 
 ```python
 > def Times(a=10, b=20):
 ... return a+b
 > Times()
 200
 > Times(5)
 100
 ```
 
- Ű���� �μ� : ������ ������� ������ �̸����� �μ��� ����
  - Ű���� �μ��� �Ϲ� �μ� �ڿ� ��ġ, Ű���� �μ� 
  - ���Ŀ��� ������ ���� �μ� ��Ī �Ұ�

- �����μ� ����Ʈ
 - `*`�� ����Ͽ� ������ �������� ���� ���� �μ��� ����
 - �μ��� Ʃ�� �������� ���޵�
 
 ```python
 > def union(*ar):
 ..  res = []
 ..  for item in ar:
 ..    if not x in res:
 ..      res.append(x)
 ..  return res
> union("HAM", "EGG")
['H','A','M','E','G']
```

- ���ǵ��� ���� �μ� ó��
 - `**`�� ����ؼ� ���ǵ��� ���� �μ��� ��ųʸ� �������� ����
 - �μ��� �� ���� �������� �;� ��
 
```python
> def userURI(server, port, **user):
..  str = "http://" + server + ":" + port + "/?"
..  for key in user.keys():
..    str += key + "=" + user[key] + "&"
..  return str
> userURI('test.com', '8080', id='userid', passwd='1234', name='mike', age = 20)
'http://test.com:8080/?passwd=1234&age=20&id=userid&name=mkie&'
```

> lambda �Լ�

- �Լ��� �̸��� ���� ��ü�� ���� ���̴�. �⺻ ���۷����� �̸��̶�� �θ��� �ִ� ����.
- C, C++ ������ �Լ��� �̸��� �־����
- ���̽㿡���� �Լ� ��ü�� �����ϴ� �͸��Լ��� ���� �� ����, `return`���� ���� ����
- �� �� ������ ������� �ٷ� ���ϰ�
 
- ��� ���?
 - ������ ������ �Լ� �ʿ�
 - ������
 - ������ �Լ��� �μ��� �Ѱ��� ��

```python
=======���� �Լ� ���� �����Ұ�=======
```
 
> �����(recursive) �Լ� ȣ�� 

- �Լ� ���ο��� ��� �ڽ��� ȣ���ϴ� ��� 
- ������ ���ݾ� �����ϸ鼭 �ݺ��� ������ �� �� ����

```python
> def factorial(x):
..  if x == 1:
..    return 1
..  return x * factorial(x-1)
> factorial(10)
3628800
```

> pass ����

- �ƹ��͵� ���� �ʴ� �Լ�, ��� ���� ������ �� ��� ���


> help �Լ��� �Լ��� ���� �� �� ����

- `help(print)`
- `__doc__` �Ӽ��� �̿��� �Լ��� �ڼ��� ���� �߰� ����

```python
> plus.__doc__ = 'return the sum of parameter a,b'
> help(plus)
Help on function plus in module __main__:
plus(a,b)
    return the sum of parameter a,b
```

���� : ����, ���ͷ�����, ���ʷ����� ��� *�Լ�*��

> iterate

- ��ȸ ������ ��ü�� ��Ҹ� ������� ������ �� �ִ� ��ü 
- ���ͷ����� ���� __next__()�� �̿��� ��ȸ ������ ��ü�� ��ҿ� �ϳ��� ���� ����

```python
> s = 'abc'
> it = iter(s)
> it
<iterator object>
> next(it)
'a'
> next(it)
'b'
> it.__next__()
'c'
> next(it)
~~~
StopItertaion
```

- `for` ������ ���ͷ����͸� �̿��� `StopIteration`�� ������ ���� �ݺ������� next�� ������

> **Generator**

- Iterator�� ����� �����ϰ� ������ ���� 
- �Լ��� ȣ��Ǹ� ���������� �ڵ尡 ���ÿ� ����ǰ� �ڵ尡 ������
- �Լ��� ������ ������� ȣ���� ���� �Ѱ��ְ� �Լ� ��ü�� ���ÿ��� �����
- �Լ��� `return` ��� `yeild`�� �����ָ� �Լ��� ������ �ʰ� ȣ���� ���� ���� ������

```python
> def reverse2(data):
..    for index in range(len(data) - 1, -1, -1):
..        yield data[index]
		
> for char in reverse2('golf'):
..    print(char)
f
l
o
g
```

- yeild�� ȣ���� ���� ���� ���������� �Լ��� �޸𸮿� �״�� �ִ�
- ������ reverse �Լ��� ȣ��Ǹ� ���� �ֱٿ� ȣ��� ���·� ����ȴ�.

���� : range(���۰�, ����, ������)

```python
>> def abc():
..     data = 'abc'
..     for char in data:
..         yield char
>> abc()
<generator object abc at 0x7fe4a0287518>
>> it = iter(abc())
>> next(it)
'a'
>> next(it)
'b'
>> next(it)
'c'
>> next(it)
---------------------------------------------------------------------------
StopIteration                             Traceback (most recent call last)
<ipython-input-18-bc1ab118995a> in <module>()
----> 1 next(it)

StopIteration: 
```

## ���

> if��
 
- ���ǽ��� ���ϰ� ���� ��쿡�� ���� ������
- �鿩����� ��� ����

> elif

- �ʿ��� ��ŭ ��� ����
- 2�� �̻��� ������ ó���ϴ� ��� ���

> else

- ���� ���������� ��� ����
- � ���ǿ��� �ش� �ȵǴ� ���

> Python�� ���ǽ� ǥ�� ���  

Python : `70 <= score < 80`  
�ٸ� ��� : `score >= 70 and score < 80`

> ���� �Ǻ� ����

- 2�� �̻��� ��� ���� ���ʿ��� ���������� �Ǻ�
- ������
 - ���ǽ� ��ü�� �Ǵ����� �ʰ� ���������� ����.
 - �º��� �캯���� ���� ������

```python
>> a = 0
>> if a and 10/a : # �����򰡷� ���� a�� False�� �Ǿ� else�� �Ѿ
..     print('a�� 0')
.. else:
..     print('�������� ���')
�������� ���
```

> ����
- ���̽㿡���� `&&`������ ����. `and` 
- `&`, `|`, XOR(`^`), NOT(`~`), Shift(`<<`, `>>`) �� ��Ʈ������


- �������� ����
 - �߰� �Ǻ� ������ �������� �ʾ� �ӵ� ���
 - Runtime error �߻��� �������� ���� ���� ����

> for��

- for���� ����� �� �ִ� �ڷ� 
 - ���ڿ�, ����Ʈ, Ʃ��, ����, ���ͷ�����, ���ʷ����� ��ü
 
 ```python
>> l = [10,20,30]
>> iterator = iter(l)
>> for i in iterator:
..     print(i)
10
20
30
```
 
- `break`�� ������ �ݺ��� ���� ����� ���
- `continue`�� ������ ���� ���� ��� �������� �ʰ� ���� �������� �����Ͽ� ���� ��� ������������ �̵�


## ����Ʈ ����

> [<ǥ����> for <������> in <��������ü> (if <���ǽ�>]

- ���� ������ ��ü�� �̿��Ͽ� �߰����� ������ ���� ���ο� ����Ʈ ��ü ����

```python
>> l = [1,2,3,4,5]
>> [ i**2 for i in l]
[1, 4, 9, 16, 25]
>> t= ('orange','apple','banana')
>> [len(i) for i in t]
[6, 5, 6]

>> [i for i in t if len(i)>5]
['orange', 'banana']

>> L1 = [3,4,5]
>> L2 = [1.5, -0.5, 4]
>> [x*y for x in L1 for y in L2 if y > 0]
[4.5, 12, 6.0, 16, 7.5, 20]
```

## ��� ���� ������ �Լ�

> filter

- �Լ��� ����� ���� ������ ��ü�� iterator�� ��ȯ
- None�� ���� ��� ���͸� X

```python
>> L = [10, 20, 30,40]
>> iterL = filter(None, L)
>> for i in  iterL:
..     print('Item : {}'.format(i))
Item : 10
Item : 20
Item : 30
Item : 40

 
>> def GetBiggerThan20(i):
..     return i > 20

>> list(filter(GetBiggerThan20, L))
[30, 40]

>> list(filter(lambda i:i>20, L))
[30, 40]
```

> range �Լ�

- ������ ��ȸ�ϴ� ���ͷ��̼� ������ ���ͷ����� ��ü ��ȯ
- ���۰�, �������� ���� ���� (�̶��� ���� 0, 1�� �Ҵ��)

```python
>> list(range(10,-1,-1))
[10, 9, 8, 7, 6, 5, 4, 3, 2, 1, 0]
```

> map �Լ�

- ������ ��ü�� ��ȸ�ϸ� function ����

```python
>> L = [10,20,30]
.. def Add10(i):
..     return i+10

>> for i in map(Add10, L):
..     print('Item : {}'.format(i))
Item : 20
Item : 30
Item : 40

>> X = [1,2,3]
>> Y = [2,3,4]
>> list(map(pow, X, Y)
[1, 8, 81]
```

***
#### �� �����ؾ� �� ����
- lambda �Լ� ����, ��� ����
- iterator, generator ���
- [map �Լ� ��� ����](https://wikidocs.net/64)
***