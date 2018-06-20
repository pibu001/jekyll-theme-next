---
title: Python - 시간복잡도와 빅오 표기법
description:
categories:
 - tutorial
tags:
---

## 시간복잡도와 빅오 표기법

알고리즘의 성능 및 효율성을 평가하는데 있어 크게 2가지의 기준이 있습니다. 
수행시간과 메모리 사용량을 평가기준으로 두는데 수행시간에 해당하는 것이 시간복잡도, 
메모리 사용량에 해당하는 것이 공간복잡도입니다. 그 중 시간복잡도에 대해 알아보겠습니다.

### 시간복잡도(time complexity)

알고리즘의 성능을 분석할 때 컴퓨터의 하드웨어나 프로그래밍 언어에 따라 명령어의 
실행 시간이 크게 달라질 수 있습니다. 시간복잡도는 알고리즘을 수행하는 데 연산(산술, 대입, 비교, 이동)들이 몇 번 
이루어지는지를 고려합니다.
연산의 개수를 입력한 데이터의 개수 n의 함수로 나타낸 것을 시간 복잡도 함수라고 말하며, 
수식으로는 `T(n)`으로 표기합니다.

> 시간복잡도 예시

```
#case1
sum = n*n

#case2
sum = 0
for i in range(n):
	sum +=i
```

`case1`의 경우 대입 연산 1번, 곱셈 연산 1번으로 명령어 실행 횟수는 **2**번 입니다.
`case2`의 경우 대입연산 n+1번, 곱셈연산 n번으로 연산 횟수는 **2n+1**번 입니다.
하나의 연산에 t시간이 소요된다고 가정하고, 덧셈과 곱셈 연산 시간이 동일하다고 가정하면 `case1`의 경우는 `2t`,
`case2`의 경우는 `(2n+1)`t만큼의 시간이 필요합니다.


> 빅오 표기법

빅오 표기법(big-oh notation)이란, 시간 복잡도 함수에서 상대적으로 
중요하지 않는 연산을 최대한 무시하고 알고리즘의 분석을 조금 더 간편하게 할 목적으로 시간 복잡도를 
표기하는 방법입니다.

![bigO_ex](https://github.com/pibu001/pibu001.github.io/blob/master/_posts/image/python_study/bigo_ex1.PNG?raw=true)
위 예와 같이 T(n)으로 표현한 함수의 최고차항의 차수가 빅오가 됩니다. 

- 빅오의 수학적 정의 

두개의 함수 `f(n)`과 `g(n)`이 주어졌을 때, 모든 `n >= n0` 에 대하여 
`|f(n)| <= c|g(n)|`을 만족하는 2개의 상수 `c`와 `n0`가 존재하면 `f(n) = O(g(n))`

![bigO_graph](https://github.com/pibu001/pibu001.github.io/blob/master/_posts/image/python_study/bigo_graph.PNG?raw=true)

빅오는 아래와 같은 순서로 커지며, `O(n^2)`이상의 복잡도를 가지는 알고리즘은 좋지 않습니다.
![bigO_graph2](https://github.com/pibu001/pibu001.github.io/blob/master/_posts/image/python_study/bigo_graph2.PNG?raw=true)