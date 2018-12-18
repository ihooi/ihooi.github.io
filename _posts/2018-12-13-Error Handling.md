---
title: Error Handling
key: 20181213
tags: python, Error Handling
---

### Error Handling
#### Try-Except를 통한 예외처리
- 프로그래밍을 하다보면 다양한 Error Message를 만나게 된다
- 하지만 예외도 있어야하기 때문에 예외처리 기법이 필요하다
- if/elif/else와 유사한 구조인데 try를 해서 오류가 발생하면 except를 수행한다
- 물론 try에서 오류가 발생하지 않으면 except도 수행되지 않는다

```python
def sqrt(x):
    try:
        return x ** 0.5
    except:
        print('x must be an int or float')
### try를 해보다가 에러나면 아래 스트링을 출력하라        

sqrt(4)
2.0

sqrt(10.0)
3.1622776601683795

sqrt('hi')
x must be an int or float
```

#### raise
- raise를 통해 지정된 에러를 실행시킬 수 있다.

```python
def sqrt(x):
    if x < 0:
        raise ValueError('x must be non-negative')
    try:
        return x ** 0.5
    except TypeError:
        print('x must be an int or float')
        
 
sqrt(-2)
Traceback (most recent call last):
  File "<input>", line 1, in <module>
  File "<input>", line 3, in sqrt
ValueError: x must be non-negative

sqrt('hi')
Traceback (most recent call last):
  File "<input>", line 1, in <module>
  File "<input>", line 2, in sqrt
TypeError: '<' not supported between instances of 'str' and 'int'
        
```