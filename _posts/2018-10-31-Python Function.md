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
