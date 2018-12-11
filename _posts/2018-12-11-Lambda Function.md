---
title: Python Function
key: 20181211
tags: python, Lambda, Function
---

### Lambda Functions
#### Python 내장 함수(Built-in function)
- lambda를 이용하면 한 줄에 명령을 할 수 있다
- 모든 상황에 유용한 것은 아니지만 적절히 활용하면 편하게 쓸 수 있음

```python
power_num = lambda x, y: x**y
# lambda 다음에 argument를 정의하고 (:) 다음에 expression 정의한다
# 여기서는 x, y를 argument로 정의하고 x의 y제곱으로 정의했다

power_num(3,2)
9
```
