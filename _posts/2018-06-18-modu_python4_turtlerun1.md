---
title: Python - 모두의 파이썬 [프로젝트 네번째]
description:
categories:
 - tutorial
tags:
---

## Turtle RUN

- 하얀 거북이를 조종해 초록색 먹이를 최대한 많이 먹는 게임
- 붉은 거북이와 만나면 게임 종료
- `t.onkeypress(turn_up, 'Up')` 명령어가 재귀 함수 돌아가는 중간에 끼어들 수 있는 배경(이벤트인듯) 자세히 알아둘 것

```python
import random
import turtle as t

# 원래 예제에서 포탄 궤적 표시, 포탄 각도 표시

#turtle init

te = t.Turtle()  #enemy
te.shape('turtle')
te.color('red')
te.up()
te.goto(0,200)

ts = t.Turtle()  # food
ts.shape('circle')
ts.color('green')
ts.up()
ts.goto(0, -200)

def turn_up():
    t.setheading(90)


def turn_down():
    t.setheading(270)

    
def turn_left():
    t.setheading(180)

    
def turn_right():
    t.setheading(0)

    
def play():
    t.forward(11)
    ang = te.towards(t.pos())
    te.setheading(ang)
    te.forward(9)

    if t.distance(ts) < 10:   # ts.xcor(), tx.ycor() 나눌 필요 없음 
        ts.goto(random.randint(-230,230), random.randint(-230,230))
    
        
    if t.distance(te) >= 6:
        t.ontimer(play, 100)

    else:
        t.write('Game Over', False, 'center',('',30))

#ground
t.setup(500,500)
t.bgcolor('orange')
t.up()
t.goto(-230, -230)
t.down()
t.goto(230, -230)
t.goto(230, 230)
t.goto(-230, 230)
t.goto(-230, -230)
t.up()
t.goto(0,0)
t.shape('turtle')
t.color('white')
t.speed(0)
t.onkeypress(turn_up, 'Up')
t.onkeypress(turn_down, 'Down')
t.onkeypress(turn_left, 'Left')
t.onkeypress(turn_right, 'Right')  # 이벤트핸들러 더욱 자세히 알아두
t.listen()  # 이 코드로 인해 onkeypress 메소드가 동작
play()
```
#### 게임 화면

![turtlerun](./image/modu_python/turtlerun_1.png)