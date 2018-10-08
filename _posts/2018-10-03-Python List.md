---
title: Python List
key: 20181003
tags: python
---

### File type
- float: 실수(real number)
- int: 정수(integer number)
- str: string, text
- bool: boolean (True, False)
<br>
<br>
- 각 변수는 하나의 value를 나타낸다
- type()을 통해 변수의 타입을 알 수 있다

~~~python
height = 168
type(height)
<class 'int'>
~~~

### Python List
- 값들의 집합
- 대괄호[]로 정의한다
- 어떠한 타입도 저장 가능
- 다른 타입들도 함께 저장 가능


~~~python
family = ["Jack", 168, "SY", 153, "Mom", 160, "Dad", 180]
~~~

- 리스트안에 리스트를 넣을 수 있다

~~~python
family2=[["Jack", 168], ["SY", 153], ["Mom", 160], ["Dad", 180]]
~~~

- Subsetting list도 만들 수 있다
  - 리스트는 '0'부터 카운트 한다. 거꾸로 셀 때는 끝에서부터 '-1'이다.
  - 대괄호[]를 써서 리스트의 특정값만 불러올 수 있다

~~~python
family[2]
'SY'

family[-1]
180
~~~

- List slicing
  - [여기서부터:여기전까지]
  - __뒷부분 순서는 포함되지 않는다__

~~~python
family
["Jack", 168, "SY", 153, "Mom", 160, "Dad", 180]

family[1:4]
[168, "SY", 153]

family[6:]
["Dad", 180]

family[:2]
["Jack", 168]
~~~

- List Manipulation
  - 리스트의 값을 바꿀 수 있다
  - 리스트에 값을 추가할 수 있다
  - 리스테에 값을 없앴을 수 있다

~~~python
# 리스트 수정
family = ["Jack", 168, "SY", 153, "Mom", 160, "Dad", 180]

family[1] = 175

family
["Jack", 175, "SY", 153, "Mom", 160, "Dad", 180]

family[2:4] = ["Sooyoon", 155]

family
["Jack", 175, "Sooyoon", 155, "Mom", 160, "Dad", 180]

# 추가
family + ["Sam", 188]
["Jack", 175, "Sooyoon", 155, "Mom", 160, "Dad", 180, "Sam", 188]

# 삭제
del(family[0:2])
["Sooyoon", 155, "Mom", 160, "Dad", 180, "Sam", 188]
~~~
