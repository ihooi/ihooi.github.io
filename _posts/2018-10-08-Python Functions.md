---
title: Python Functions
key: 20181008
tags: python, Functions
---

### Functions
- 미리 만들어 놓은 코드
- 매번 코드를 쓸 필요 없이 Function을 이용
- 반복적으로 사용되는 특정 task를 수행하는 function으로 만들어 놓음

~~~python
height = [168, 175, 180, 159]

max(height)
180
~~~

- round() 예시
~~~python
round(168.2582, 1)
168.3

round(168.2582, 2)
168.26

round(168.2582, 3)
168.258

round(168.2582, 4)
168.2582
~~~
- 일반적인 Task라면 function이 있을 가능성이 높으니 검색해보는 것이 좋다

## Methods
> Method: Functions that belong to object <br>
> _(Data Camp)_

- Method는 object가 반드시 있어야 함
- _Function과 Method의 차이가 아직 명확하게 이해되지 않음_

~~~python
family = ["Jack", 168, "SY", 153, "Mom", 160, "Dad", 180]

family.index("SY") #family에 index()을 호출
2

~~~

~~~python
wife = 'suyoon'

wife
'suyoon'

wife.capitalize() #대문자변환
'Suyoon'

wife.replace("u", "oo") #일부 스트링 변환
'sooyoon'
~~~

- Object는 타입에 따라 Method가 연결되어 있음

~~~python
family
Out[27]: ['Jack', 168, 'SY', 153, 'Mom', 160, 'Dad', 180]

family.replace('SY', 'Sooyoon')
AttributeError: 'list' object has no attribute 'replace'
~~~

## Package
- 모든 Function을 모두 built-in 할 수는 없음
- 따라서 특정 목적에 따른 function, method, type들을 모아 package로 만든다
  - Numpy
  - Matplotlib
  - pandas
  - tensorflow
- pip 등을 통해 package 다운로드

~~~bash
pip install numpy
~~~

- package를 설치한 이후에는 `import`를 활용하여 호출

~~~python
import numpy as np #이후 부터는 np뒤에 numpy method를 호출하게 된다
~~~
