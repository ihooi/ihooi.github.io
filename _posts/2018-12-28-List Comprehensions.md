---
title: List Comprehensions / Generator
key: 20181228
tags: python, List Comprensions, Generator
---

### List Comprehensions
#### 복습
- 리스트를 만들기 위해 `for`문을 사용했다

```python
number = [1, 2, 3, 4, 5]

new_n = []

for i in number:
    new_n.append(i + 1)
    
print(new_n)
[2, 3, 4, 5, 6]
```

#### Listi Comprehension 개념
- List Comprehension을 쓰면 한 문장으로 가능하다
- iterable / iterable valiable / output expression 이 충족되어야 한다
- 위에 내용과 비교해보자
- *느낌상 아무때나 쓰면 안될 것 같다*

```python
number = [1, 2, 3, 4, 5]

new_n = [i+1 for i in number ]   #expression 적고 뒤에 for 내용 적음

print(new_n)
[2, 3, 4, 5, 6]
```

- `range` 를 써 보자

```python
m = [i for i in range(11)]

print(m)
[0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
```

#### Nest loop에 대한 List Comprehension
- `for`문이 중복으로 적용된 문구도 List Comprehension 적용이 가능하다.

```python
# Nested Loop

mate = []

for num1 in range(0,2):
    for num2 in range(6,8):
        mate.append(num1, num2)
        
print(mate)
[(0, 6), (0, 7), (1, 6), (1, 7)]
```

```python
#list comprehension
mate_1 = [(num1, num2) for num1 in range(0,2) for num2 in range(6,8)]

print(mate_1)
[(0, 6), (0, 7), (1, 6), (1, 7)]
```

#### 조건문을 활용한 Comprehension
- `for` 다음에 `if`를 적용할 수 있다

```python
[num + 1 for num in range(11) if num % 2 == 0]
### range 11 사이의 수를 2로 나누어 나머지가 0이면, num에 +1 하라 ###
[1, 3, 5, 7, 9, 11]
```

- `else`까지 적용해보자
- 이때는 `for`보다 먼저 나온다.

```python
[num + 1 if num % 2 == 0 else 100 for num in range(11)]
### range 11 사이의 수를 2로 나눠서 나머지가 0이면 +1하고 아니면 100을 출력해라 ###

[1, 100, 3, 100, 5, 100, 7, 100, 9, 100, 11]
```

#### Dictonary Comprehension
- dictionary에도 적용 가능하다
- __대괄호를 쓰자__

```python
num_double = {num: num*2 for num in range(5)}
print(num_double)
{0: 0, 1: 2, 2: 4, 3: 6, 4: 8}
```

### Generator
#### 기본 개념
- 리스트 중괄호가 아닌 튜플 소괄호를 쓴다.

```python
(num**2 for num in range(11))
<generator object <genexpr> at 0x03A8CD30>
```

#### List Comprehesion과의 차이
- LC는 리스트로 반환하지만 Generator는 Object로 반환한다
- LC는 잘못 코드를 짜서 실행시키면 리소스 과다로 뻗을 수 있지만 Generator는 Object로 반환하기 때문에 그렇지 않다

```python
### 일반 Generator 출력
gen = (num for num in range(11))

for num in gen:
    print(num)
       
0
1
2
3
4
5
6
7
8
9
10

### 리스트로 바꿔서 출력해보자
gen = (num for num in range(11))

print(list(gen))
[0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
```

- `next`를 사용할 수도 있다

```python
gen = (num for num in range(11))

print(next(gen))
0
print(next(gen))
1
print(next(gen))
2

...
```

#### 조건문을 활용한 Generator
- 물론 조건문 사용이 가능하다

```python
even_nums = (num for num in range(11) if num % 2 == 0)

print(list(even_nums))
[0, 2, 4, 6, 8, 10]

```