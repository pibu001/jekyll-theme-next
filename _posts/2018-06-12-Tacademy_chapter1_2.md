---
title: Python -  T��ī���� Python ���� ���� chapter_1&2 
description:
categories:
 - tutorial
tags:
---

## ���̽� ����  

> Python Ư¡  

������, ǳ���� ���̺귯��, ������, �����ڵ�, ����, ����Ÿ����  

> 2.~ ������ 3.~ ������ ����  

- print ��ȭ
- long���� int�� ����
- int�� int ���� ���� float�� ó��
- string, unicode ü�� ����

> `#`�� �ּ����� �ν�  

�ҽ��ڵ� �κп��� ���� ��� �ҽ��ڵ� ���ڵ��� �����ϴ� �뵵�� ����  
`- # -*- coding: utf-8-*-`  
���� ���ϸ� �ƽ�Ű �ڵ尡 �⺻  
������ �ҽ��ڵ� ���ڵ��� �ۼ����� �ʰ� �ѱ� �ּ��� �� ��� ���ڵ� ������ �߻��� �� �ִ�.  

> `2to3`�� �̿��ϸ� ������ ���α׷��� ���� ��ȯ����  

ū ����� ��� �׽�Ʈ ���̽��� ���� ������ ���θ� �׽�Ʈ �ؾ���  


## �ڷ��� �� ������  

> complex (���Ҽ�)  

```python
> x = 3 - 4j
> type(x), x.imag, x.real, x.conjugate()
(<class 'complex>, -4.0, 3.0, (3+4j))
```

- ����������  

```python
> 5//2
2
```

> Escape ����  

`\n` : ����  
`\t` : ��  
`\r` : ĳ���� ����  
`\0` : ��(null)  
`\\` : ���� `\`  
`\'` : ���� �ο��ȣ(')  

> �ε��� & �����̽�

```python
> 'python'[0]
'p'
> 'python'[1:4]
'yth'
```

�ε����� �̿��� ���ڿ� ������ ������ ����  

�ٸ� ���ڿ� ��ü�� �ٽ� �Ҵ��� ���� ����  

> �����ڵ�  

��� string(���ڿ�)�� �����ڵ�  
�����ڵ� �̿��� ���ڵ��� �ִ� ���ڿ��� bytes�� ǥ��  

```python
> type('��')
<class 'str'>
> type('��'.encode('utf-8'))
<class 'bytes'>
```

> ����Ʈ  

- `append`, `insert`, `extend`, `+` �����ڸ� �̿��� ������ �߰��� �� �ִ� 
 
```python
> colors = ['green']
> colors.append('blue')
> colors
['green','blue']
> colors.extend(['white','gray'])
> colors
['green','blue','white','gray']
```
- index�� �̿��� �� ��ġ Ȯ��  

```python
> colors.index('green')
0
> colors.index('green',1)
4
```

- count, pop

```python
> colors.count('green')
1
> colors.pop()
'gray'
> colors
['green','blue','white']
```

- remove�� �� ����, sort�� ���� ����  

> Ʃ��

- Ʃ��(tuple)�� ����Ʈ�� ����, but �б� ����
- �ӵ��� �������� �����Ǵ� �Լ� ����
- count, index �޼��� ����
- Ʃ���� �̿��ϸ� ������ swap ����
`a,b = b,a`

> ��ųʸ�  

- Ű�� ������ �̷����
```python
> color = {'apple':'red', 'banana':'yellow'}
> color['cherry']='red'
> color
{'apple':'red', 'banana':'yellow', 'cherry':'red'}
```

- items() : ��ųʸ��� ��� Ű�� ���� Ʃ�÷� ���� ��ȯ

- keys() : Ű�� ��ȯ  
- values() : ���� ��ȯ  
- `del color['cherry']` : ����
- `color.clear()` : ��� ����

> �ο�(bool)

- �񱳿����� : `>`, `<`, `==`, `!=`, `>=`, `<=`

- �������� : and(&), or(|), not

> �������� vs ��������

- �������� : �ּҰ� ����Ǿ� ��ü�� ����
- �������� : ��ü�� �������� �ʴ� ���

�������� ��
```python
> a = [1,2,3]
> b = a
> a[0] = 38
> a
[38,2,3]
> b
[38,2,3]
> id(a) == id(b)
True
```

�������� ��
```python
> a = [1,2,3]
> b = a[:]
> id(a) == id(b)
False
> a[0] = 38
> a
[38,2,3]
> b
[1,2,3]
```

***
#### �� ������ ����
- ���۷����� �ּ�, �޸𸮿� ���� �� �ڼ��� �˾ƺ���
 - �������� ����� ���� ��������

***


