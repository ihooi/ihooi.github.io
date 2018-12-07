---
title: Python Function
key: 20181031
tags: python, Function
---

### Functions
#### Python 내장 함수(Built-in function)
- Python은 반복적으로 사용되는 기능들에 대해서는 함수로 만들어 내장되어 있다

~~~python
#예시 함수
#절대값을 변환해주는 abs()
abs(-5)
5

#스트링으로 변환해주는 str()
x = str(5)

x
'5'

type(x)
str
~~~

#### User-defined Functions
- 개발자가 특정 함수를 만들어 사용할 수 있다
- *실질적인 프로그래밍은 함수 개발일 수도 있겠다*
- 기본적인 문법은 다음과 같다

~~~python
def name(parameter): #앞에 def를 붙여 함수임을 알리고 괄호에 Parameter가 들어왔을 때
  function body  # body에 있는대로 수행하라

# 물론 : 이나 Indentation은 기본이다
~~~

~~~python
# 예시 함수
def square(value): #square란 함수는 value를 하나 받고
  squared_value = value ** 2 #value가 들어오면 제곱하여 squared_value 변수로 지정하고
  print(squared_value) # 출력해라

square(2) #2의 제곱을 출력하라
4

square(6) #6의 제곱을 출력하라
36
~~~

- ```return```을 쓰면 출력하지 않고 결과값을 가지고 있게 된다

~~~python
def square(value): #square란 함수는 value를 하나 받고
  squared_value = value ** 2 #value가 들어오면 제곱하여 squared_value 변수로 지정하고
  return squared_value # 리턴하라

answer = square(6)
#36을 출력하지 않고 answer 값으로만 리턴함

print(answer)
36  
~~~
- docstrings를 써서 함수 내용을 정의해놓으면 향후 편리하게 이해할 수 있다. **주석이 중요하다**
- 큰따옴표 3개로 표기한다.

~~~python
def square(value):
  """ Value의 제곱값을 구해 Return하라"""
  squared_value = value ** 2
  return squared_value
~~~

#### Multi parameter
- 당연하게도 복수의 Parameter 사용이 가능하다

~~~python
def plus(val1, val2):
  """ val1과 val2를 더해서 return하라"""
  answer = val1 + val2
  return answer

result = plus(10, 5)

result
15
~~~

- 복수의 value를 뽑게 할 수도 있다

~~~python
def plus_avg(num1, num2):
  """두개의 값을 더하고, 평균을 구해 튜플로 지정하라"""
  value1 = num1 + num2
  value2 = value1 / 2

  tuple_value = (value1, value2)
  return tuple_value

result = plus_avg(10, 30)

print(result)
(40, 20.0)
~~~

#### Global / Local Scope
- def 안에 있는 variables는 def안에 종속되게 되어있다. (Local)

```python
new_num = 2

def double(value):
    new_num = value*2
    return new_num
    
double(2)
4

new_num  # 함수대로라면 new_num은 4가 되있어야 하지만 지역 변수이므로 함수 안에서만 적용된다
2
```

- 'global'을 이용하면 전역으로 사용 가능하다.

```python
new_num = 2

def double(value):
    global new_num
    new_num = value*2
    return new_num
    
double(2)
4

new_num
4
```

#### Nested Funtions
- 함수 안에 함수를 포함하는 것도 가능하다

```python
def three_repeat(w1,w2, w3):
    def inner(word):
        return word*3
    return (inner(w1), inner(w2), inner(w3))  #튜플로 리턴한다
    
print(three_repeat('a','b','c'))
('aaa', 'bbb', 'ccc')
```

- global과는 다르지만 non-local로 쓸 수 도 있다

```python
def outer():
    n = 1
    def inner():
        nonlocal n
        n = 2
        print(n)
    inner()
    print(n)
    
outer() 
2
2
 ###처음에 n이 1로 지정되었지만 inner에서 n은 2로 지정되었고 이는 nolocal로 지정되었다.
```
- 기계가 검색할 때는 LEGB 순서로 검색한단다.(Local-Enclosing Functions-Global-Built-in)

#### Default & Flexible argument
- 특정 argument의 디폴트 값을 지정할 수 있다
```python
def multiple (val, mul=1): # mul의 default값을 정해버렸다
    new_val = val*mul
    return new_val
    
multiple(2,3)
6
multiple(3,4)
12
multiple(4)
4
``` 

- '''args'''를 통해 argument를 유동적으로 할 수 있다
```python
def add(*args):
    sum_all = 0
    for num in args:
        sum_all += num
    return sum_all

add(1,2,3)
6

add(1,2,3,4,5,6,7,8,9)
45
```

- keyword/value로 구성된 argument는 '''**kwarg'''를 사용하자
```python
def print_fullname(**kwarg):
    for key, value in kwarg.items():
        print(key + ": "+ value)
        
print_fullname(last='Lee', first='Jack')
last: Lee
first: Jack
```

