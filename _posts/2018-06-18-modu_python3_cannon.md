---
title: Python - 모두의 파이썬 [프로젝트 세번째]
description:
categories:
 - tutorial
tags:
---

## 거북이 대포 게임 만들기 (응용)

- 대포를 발사해 목표 지점을 맞추는 게임
- `t.onkeypress(turn_up, 'Up')` 명령어가 재귀 함수 돌아가는 중간에 끼어들 수 있는 배경(이벤트인듯) 자세히 알아둘 것

```python
import random
import turtle as t

def turn_up():
    t.left(2)

def turn_down():
    t.right(2)

def fire():
    ang = t.heading()

    while t.ycor() > 0:    #Repeated while the turtle is in the air
        t.forward(20)
        t.right(5)

    d = t.distance(target, 0)
    t.up()
    t.sety(random.randint(10, 100)) #location of message

    if d < 25:
        t.color('blue')
        t.write('Good!', False, 'center', ('',15))

    else:
        t.color('red')
        t.write('Bad', False, 'center', ('',15))
        t.color('gray')
        #t.up()
        t.goto(-200, 10)
        t.setheading(ang) #Reverted to the first angle
        t.down()

#ground

t.goto(-300,0)
t.down()
t.goto(300,0)

#target

target = random.randint(0,250)
t.pensize(3)
t.color('green')
t.up()
t.goto(target-25, 2)
t.down()
t.goto(target+25, 2)


#turtle init

t.color('black')
t.up()
t.goto(-200,10)
t.setheading(20)
t.pensize(1)
t.color('gray')
t.down()

#turtle setting

t.onkeypress(turn_up, 'Up')
t.onkeypress(turn_down, 'Down')
t.onkeypress(fire, 'space')
t.listen()
```

![cannon_img](https://drive.google.com/open?id=1pQ7MYASxLryHiTOmvq_qaYwxMSQuu8Rw)