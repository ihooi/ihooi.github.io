---
title: Python (2)
key: 20181017
tags: python, Comparison, Boolean, conditional
---

### Comparison Operators (비교연산자)
- 산수시간에 배운 비교 연산자를 동일하게 사용하면된다
  - 같은 경우는 '''=='''
  - 같지 않은 경우 '''!='''
  - 크거나 같은 경우 '''>=''' , 작거나 같은 경우 '''<='''

### Boolean Operators (참/거짓)
- 'and', 'or', 'not' 개념으로 기본 수학 명제 개념과 동일하다
  - True and True = True
  - True and False = False

  - True or False = True
  - False or True = True

  - not True = False
  - not False = True
- 가장 확실한 방법은 노트에 써보면서 해보면 실수가 없다

### Numpy에서의 Boolean
- Numpy에서 and, or, not을 쓰면 에러

~~~python
import numpy as np

height = np.array([168, 179, 172, 189, 153])

height
array([168, 179, 172, 189, 153])

height > 160
array([ True,  True,  True,  True, False])

height < 180
array([ True,  True,  True, False,  True])

height > 160 and height < 180
ValueError: The truth value of an array with more than one element is ambiguous. Use a.any() or a.all()
~~~

- logical_and() / logical_or() / logical_not() 을 써야함

~~~python
np.logical_and(height > 160, height < 180)
array([ True,  True,  True, False, False])
# logical_or(), logical_not()도 동일하게 비교하고자 하는 값들을 콤마로 구분하여 넣으면 된다

height[np.logical_and(height > 160, height < 180)]
array([168, 179, 172])
~~~

### Conditional Statement (조건문)
- 조건문도 영어의 'if', 'elif(else if)', 'else' 로 간단히 이해할 수 있다.
- 작성 요령이 중요함

~~~python
if 조건 :
  수행
# 만약 조건이 참이라면 수행해라.
# if 다음에 콜론 ':' 잊지말 것
# 콜론 다음에 indentation 잊지말 것

x = 100

if x % 2 == 0 : #2로 나눈 나머지가 0이면 수행
    print(str(x)+ ' is even')   
100 is even
~~~

- elif 나 else를 쓰면 여러 조건을 처리할 수 있음
- 위 라인부터 순서대로 된다는 것을 잊지 말것

~~~python
y = 5
if y % 2 == 0 : #false
    print('y is even') # 미실행
elif y % 2 == 1 : #True
    print('y is odd') # 실행
else:
    print('y is zero') #미실행

y is odd
~~~

### Padas를 통한 실습
- 지난번 실습 자료를 다시 보자

~~~python
import pandas as pd

friend = pd.read_csv("c:/Users/hoseok/Documents/friend.csv", index_col=0)

friend
       name  last  age  height
JL     Jack   lee   26   180.2
PS  Phillip  song   32   169.8
RK   Robert   kim   45   175.3
AP     Adam  park   55   192.1
~~~

- 여기서 키가 180이 넘는 사람만 선택하려면 다음의 단계가 필요함
  1. height 컬럼을 선택하고
  2. 컬럼에서 조건에 맞는지 비교하고
  3. 조건에 부합하는 row를 불러온다


- 먼저, 데이터를 불러서 살펴보자

~~~python
friend.loc[:, 'height']  # .iloc[:, 3] 혹은 freind['height'] 도 동일한 결과가 나온다
Out[29]:
JL    180.2
PS    169.8
RK    175.3
AP    192.1
Name: height, dtype: float64

#180이 넘는 것은 JL과 AP임을 알 수 있다
~~~

- 180이 넘는 사람들만 서브셋 데이터 프레임을 만든다

~~~python
tallguy = friend['height'] > 180 #height가 180보다 크면 tallguy로 지정하여 서브셋 데이터프레임을 만든다

tallguy
JL     True
PS    False
RK    False
AP     True
Name: height, dtype: bool

# JL, AP가 지정된 걸 확인할 수 있다.
~~~

- 서브셋 DF에 부합하는 row를 불러온다

~~~python
friend[tallguy]
    name  last  age  height
JL  Jack   lee   26   180.2
AP  Adam  park   55   192.1
~~~

- 사실 이 과정을 한번에 할 수도 있다

~~~python
friend[friend['height'] > 180]
    name  last  age  height
JL  Jack   lee   26   180.2
AP  Adam  park   55   192.1
~~~

- boolean까지 적용하여 180이 넘으면서 30이 안된 사람을 선택하려면?

~~~python
import numpy as np

np.logical_and(friend['height'] > 180, friend['age'] < 30)

JL     True
PS    False
RK    False
AP    False
Name: height, dtype: bool

friend[np.logical_and(friend['height'] > 180, friend['age'] < 30)]

    name last  age  height
JL  Jack  lee   26   180.2
~~~
