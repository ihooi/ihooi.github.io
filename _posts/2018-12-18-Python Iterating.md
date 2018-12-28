---
title: Python Iterating
key: 20181218
tags: python, Iterating,
---

### Iterators
#### 복습
- 앞서 Loop를 배웠다([이전포스팅](https://ihooi.github.io/2018/10/18/Python-Loop.html))
- 다시 복습해보면

```python
family = ['Jack', 'Mary', 'Jane']

for member in family:
    print(member)

Jack
Mary
Jane
```

```python
for letter in 'Jack Lee':
    print(letter)
    
J
a
c
k
 
L
e
e
```

#### Iterable
- 순차적인 반환이 가능한 객체들 (list, strings, dictionary, tuple, file connection )
- iter()를 쓰면 순차적으로 호출할 수 있다
- next()를 통해 하나씩 불러올 수 있다
- 더 이상 호출한 것이 없으면 에러 메시지

```python
name = 'Jack'
it = iter(name)
next(it)
'J'
next(it)
'a'
next(it)
'c'
next(it)
'k'
next(it)
Traceback (most recent call last):
  File "<input>", line 1, in <module>
StopIteration

```

- '*'를 쓰면 한번에 호출할 수도 있다.

```python
name = 'Jack'
it = iter(name)
print(*it)
J a c k
print(*it)
# 에러는 안나지만 출력될 것도 없다
``` 

- dictionary도 iterating 가능하다

```python
member = {'Jack':'Lee', 'Calson':'Kim'}
for first, last in member.items():
    print(first, last)
    
Jack Lee
Calson Kim

```

- file 도 가능하다

```python
file = open('file.txt')
it = iter(file)
print(next(it))
First line
print(next(it))
last line
```

#### enumerate()
- 사전 뜻은 '열거하다'
- 해당 함수를 쓰면 list로 만들고 순서도 출력한다

```python
classroom = ['Jack', 'Janet', 'Johnson', 'Jacob']
e = enumerate(classroom)
print(e)
<enumerate object at 0x03C7C558>

print(list(e))
[(0, 'Jack'), (1, 'Janet'), (2, 'Johnson'), (3, 'Jacob')]
```
- 조금 더 활용하면 더 다양하게 쓸 수 있다

```python
classroom = ['Jack', 'Janet', 'Johnson', 'Jacob']
for index, name in enumerate(classroom):
    print(index, name)
    
0 Jack
1 Janet
2 Johnson
3 Jacob
```

- 시작 번호도 지정할 수 있다. 
```python
for index, name in enumerate(classroom, start=100):
    print(index, name)
    
100 Jack
101 Janet
102 Johnson
103 Jacob
```


####zip()
- 말그대로 2개의 연속형을 붙이는 기능

```python
firstname = ['Jack', 'Lynette', 'Brian']
lastname = ['Lee', 'White', 'McCoy']

fullname = zip(firstname, lastname)
list_fullname = list(fullname)

print(list_fullname)
[('Jack', 'Lee'), ('Lynette', 'White'), ('Brian', 'McCoy')]
```

- for문으로 풀어서 쓸 수도 있다.

```python
firstname = ['Jack', 'Lynette', 'Brian']
lastname = ['Lee', 'White', 'McCoy']

for z1, z2 in zip(firstname, lastname):
    print(z1, z2)

Jack Lee
Lynette White
Brian McCoy
```
- '*'를 쓰는 것도 가능하다

```python
firstname = ['Jack', 'Lynette', 'Brian']
lastname = ['Lee', 'White', 'McCoy']

fullname = zip(firstname, lastname)

print(*fullname)

('Jack', 'Lee') ('Lynette', 'White') ('Brian', 'McCoy')

```

#### 빅데이터 처리를 위한 Iterator 활용
- 데이터가 너무 크면 메모리에 다 올릴 수가 없다
- 이럴때는 데이터를 Chunk 단위로 끊어서 로드할 수 있다
- Pandas에서 chunksize를 지정할 수 있다.

```python
import pandas as pd

result= []  # 빈 리스트 생성

for chunk in pd.read_csv('data,csv', chunksize=500): # reda_csv를 이용해 csv파일를 불러오되 chunksize는 500으로 
    result.append(sum(chunk['x'])) # chunk의 sum을 구해 append
    
total = sum(result)
print(total)
42525

```

- 빈리스트가 아니라 이니셜 수를 넣으면 더 간단하다

```python
import pandas as pd

total = 0 # 초기값 세팅

for chunk in pd.read_csv('data.csv', chunksize=500):
    total += sum(chunk['x'])
    
print(total)
42525

```

