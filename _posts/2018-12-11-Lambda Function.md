---
title: Python Function
key: 20181211
tags: python, Lambda, Function
---

### Lambda Functions
#### 기본 정의
- lambda를 이용하면 한 줄에 명령을 할 수 있다
- 모든 상황에 유용한 것은 아니지만 적절히 활용하면 편하게 쓸 수 있음

```python
power_num = lambda x, y: x**y
# lambda 다음에 argument를 정의하고 (:) 다음에 expression 정의한다
# 여기서는 x, y를 argument로 정의하고 x의 y제곱으로 정의했다

power_num(3,2)
9
```

#### map()
- map(funtion, sequence)로 사용한다.
- 입력받은 자료형의 각 요소가 function을 수행한다
- double이라는 함수가 각 리스트의 값을 모두 두배로 곱하는 함수라면, 'map()'을 쓰면 다음과 같이 할 수 있다

```python
list(map(double, [1,2,3,4])) # [1,2,3,4]의 각 요소를 double함수를 돌려서 list로 만들어라
[2,4,6,8]
```

- 이를 위해서는 double이라는 함수를 먼저 정의해야 하는데 lambda를 쓰면 더 간략하게 만들 수 있다

```python
list(map(lambda a: a*2, [1,2,3,4]))
[2,4,6,8]
```

#### filter()
- 리턴값이 참인 경우만 걸러셔 돌려줌
```python
forth_grade = ['Jack', 'Martin', 'Jane', 'Sarah']

result = filter(lambda member: len(member) > 5, forth_grade) #forth_grade에서 길이가 5자보다 큰 것만 필터링
print(list(result))
['Martin']
```

#### reduce()
- functools 모듈에 있는 함수

```python
from functools import reduce

forth_grade = ['Jack', 'Martin', 'Jane', 'Sarah']

result = reduce(lambda item1, item2: item1 + item2, forth_grade)
print(result)
JackMartinJaneSarah
```