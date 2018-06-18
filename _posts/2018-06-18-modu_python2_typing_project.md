---
title: Python - 모두의 파이썬 [타자게임]
description:
categories:
 - tutorial
tags:
---

## 타자 게임 만들기

```python

import random
import time


word_list = ['cat','dog','fox','monkey','panda','wolf','frog','mouse','snake']
n = 0

input('준비되면 엔터를 눌러주세요')
start = time.time()

now_word = random.choice(word_list)

while n < 5:
    print(n+1,'번째 word : ', now_word)
    input_word = input('입력 단어 : ')

    if input_word == now_word:
        print('통과')
        n += 1
        now_word = random.choice(word_list)

    else:
        print('다시 입력하세요')     


end = time.time()

total_time = end - start

total_time = format(total_time, '.2f')

print('total time : ', total_time,'초')
```

```python
1번째 word : cat
cat
통과
2번째 word : panda
panda
통과
...
...
```
