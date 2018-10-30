---
title: Python Tuple
key: 20181030
tags: python, Tuple
---

### Tuple
- List처럼 여러개의 Value를 가질 수 있다
- **Tuple은 Value를 수정할 수 없다**
- 소괄호를 써서 표현한다

~~~python
my_num = (1, 2, 3)

my_num
(1, 2, 3)

type(my_num)
tuple
~~~

- **여러 변수에 Tuple Value를 지정할 수 있다**

~~~python
a, b, c = my_num  # a, b, c 라는 각각의 변수에 Value를 지정했다. 낯선 표현방식이라 헷갈린다

print(a)
1

print(b)
2

print(c)
3
~~~

- list와 마찬가지로 인덱싱하여 끄집어 낼 수 있다.
- 역시 마찬가지로 인덱싱은 '0'부터 시작이다

~~~python
my_num[1]
2

my_num[0]
1

my_num[1]
2

my_num[2]
3

my_num[0:2]
(1, 2)

my_num[0:]
(1, 2, 3)
~~~
