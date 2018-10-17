---
title: Python Loop
key: 20181017
tags: python, loop, while, for
---

### While loop
- 앞서 정리한 if문은 일회성 코드로 순서에 따라 한번만 수행한다
- 반복적으로 하기 위해서는 Loop 가 필요하다.
- while loop는 if문을 반복적으로 수행하는 것이다
- 수학적 반복 모델

~~~python
while 조건 :
  수행
# 조건이 맞을 때까지 수행을 계속한다
~~~

- 예제

~~~python
n = 1

while n < 10: #1에서 시작해서 10보다 작은동안 n을 출력한 다음에 2를 더해라
    print(n)
    n += 2

1
3
5
7
9 # 그 다음은 11이므로 더이상 수행하지 않고 while 문을 끝낸다
~~~

- loop는 잘못 짜면 무한루프가 생길 수 있다. 그럴땐 ctr+c

### For loop
- for문은 시퀀스내에 변수를 모두 실행한다

~~~python
for 변수 in 시퀀스 :
  수행
~~~


~~~python
friend = [180, 173, 156, 169]

for height in friend: #height는 임의로 지정한다. 앞에 변수로 지정할 필요없다
    print(str(height)) # friend를 변수스트링을 하나씩 출력하라

180
173
156
169
~~~

~~~python
for i in "coffee" :
   print(i.capitalize())

C
O
F
F
E
E
~~~

### 데이터 구조에서의 loop 적용
#### Dictionary
- Key:value 구조에 맞게 loop를 적용할 수 있다

~~~python
friend = { "Jack": 42, "Phillip": 35, "Robert": 50 }

for name, age in friend :
    print(name + "'s age is " + str(age))
ValueError: too many values to unpack (expected 2)
# dictionary에 적합한 함수를 써야 함

for name, age in friend.items(): # .items()에 주목하라
    print(name + "'s age is " + str(age))

Jack's age is 42
Phillip's age is 35
Robert's age is 50
~~~

#### Numpy Array
- 행렬도 마찬가지로 합당한 함수를 써야한다.

~~~python
import numpy as np

np_height = np.array([1.68, 1.77, 1.80])

np_weight = np.array([70, 98, 80])

bmi = np_weight / np_height**2

for v in bmi: # 각 항별로 bmi를 계산해서 출력
    print(v)

24.801587301587304
31.28092182961473
24.691358024691358
~~~

- 2차원 Array에도 적용 가능하다

~~~python
np_height = np.array([1.68, 1.77, 1.80])

np_weight = np.array([70, 98, 80])

body = np.array([np_height, np_weight])

for v in body:
    print(v)

[1.68 1.77 1.8 ]
[70. 98. 80.]
~~~

- `np.nditer(array)`를 쓰면 행렬 모든 값에 적용할 수 있다. (결과는 행렬이 아니게 된다)

~~~python
np_height = np.array([1.68, 1.77, 1.80])

np_weight = np.array([70, 98, 80])

body = np.array([np_height, np_weight])

for v in np.nditer(body):
    print(v)

1.68
1.77
1.8
70.0
98.0
80.0    
~~~

### 예제를 통한 실습
- 일단 또 불러보자

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

- 각 컬럼의 제목만 뽑자

~~~python
for v in friend:
    print(v)

name
last
age
height
~~~

#### .iterrows()
- `.iterrows()`를 통해 row별 iteration 할수 있다

~~~python
for label, row in friend.iterrows():
    print(label)
    print(row)

JL
name       Jack
last        lee
age          26
height    180.2
Name: JL, dtype: object
PS
name      Phillip
last         song
age            32
height      169.8
Name: PS, dtype: object
RK
name      Robert
last         kim
age           45
height     175.3
Name: RK, dtype: object
AP
name       Adam
last       park
age          55
height    192.1
Name: AP, dtype: object
~~~

- 특정 값만 뽑아서 프린트 하자면

~~~python
for label, row in friend.iterrows():
    print(label + "-- " + row["last"]+" "+row["name"])

JL-- lee Jack
PS-- song Phillip
RK-- kim Robert
AP-- park Adam
~~~

- `iterrows()`를 써서 컬럼을 늘릴기

~~~python
for label, row in friend.iterrows():
   friend.loc[label, "name_length"] = len(row["name"]) # name_length라는 컬럼은 name의 길이다
print(friend)


      name  last  age  height  name_length
JL     Jack   lee   26   180.2          4.0
PS  Phillip  song   32   169.8          7.0
RK   Robert   kim   45   175.3          6.0
AP     Adam  park   55   192.1          4.0
~~~

#### .apply
- `.apply` 함수로 조금 더 용이하게 적용할 수 있다.

~~~python
friend["last_length"] = friend["last"].apply(len)

print(friend)
       name  last  age  height  name_length  last_length
JL     Jack   lee   26   180.2          4.0            3
PS  Phillip  song   32   169.8          7.0            4
RK   Robert   kim   45   175.3          6.0            3
AP     Adam  park   55   192.1          4.0            4
~~~
