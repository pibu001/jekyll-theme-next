---
title: Python - 모두의 알고리즘 1
description:
categories:
 - tutorial
tags:
---

## 모두의 알고리즘

#### 하노이탑 움직인 횟수

> 입력

```python
def hanoi(n):
    if n == 1:
        return 1

    return 2*hanoi(n-1) + 1
```
> 출력

```	
hanoi(3)
7
```
	
	
#### 하노이탑 전체 이동

```python
def hanoi_move(n, a, b, c):  # a:from, b: to, c:help
    if n == 1:
        print(a,'->',b)
        return
    
    hanoi_move(n-1, a, c, b)
    print(a,'->',b)
    hanoi_move(n-1, c, b, a)
        
	hanoi_move(3, 1, 3, 2)
```

> 출력

```python
1 -> 3
1 -> 2
3 -> 2
1 -> 3
2 -> 1
2 -> 3
1 -> 3
```

#### Sequential seach

```python
def search_list(a, x): # a = list, x = find_var
    n = len(a)
    for i in range(n):
        if x == a[i]:
            return i
    
    return -1   

v = [17, 92, 18, 33, 58, 7, 33, 42]
search_list(v, 18)
2
```


