---
title: Numpy Basic
key: 20181008
tags: python, Numpy
---

### 기본 개념
- 일반 Python에서는 리스트와 Int 간 연산이 불가하다

~~~python
height = [1.68, 1.77, 1.80]

weight = [70, 98, 80]

bmi = weight/height**2
TypeError: unsupported operand type(s) for ** or pow(): 'list' and 'int'
~~~

- 이러한 문제를 Numpy로 해결할 수 있다
- Numpy의 주요 개념
  - Numeric Python 패키지
  - Array(행렬)을 만들어서 List의 한계를 해결할 수 있다
  - Array간 계산이 가능하다

~~~bash
> pip install numpy
~~~

- 위의 BMI 계산을 Numpy로 해결해보자

~~~python
import numpy as np

height = [1.68, 1.77, 1.80]

weight = [70, 98, 80]

np_height = np.array(height) # np를 통해 numpy를 호출한다. 'as np'를 기억하라

np_weight = np.array(weight) #.array()를 통해  리스트를 행렬로 변환

bmi = np_weight / np_height**2

bmi
array([24.8015873 , 31.28092183, 24.69135802]) #각 행렬의 항끼리 계산되었다(1.68/70**2, 1.77/98**2, 1.80/80**2)
~~~

- Numpy Array는 한가지 타입으로만 구성할 수 있다
- 리스트끼리와의 계산과 행렬끼리의 계산은 다르다
  - 리스트1+리스트2 = 리스트1 출력 후 리스트2 출력
  - Array1+Array2 = Array1과 Array2의 각 행렬 값끼리 더한다
- Array의 subsetting도 가능하다

~~~python
bmi
array([24.8015873 , 31.28092183, 24.69135802])

bmi[0]
24.801587301587304

bmi > 30
array([False,  True, False]) #bmi 30 초과에 대해 Boolean으로 표기

bmi[bmi > 30]
array([31.28092183]) #bmi 30초과된 값 찾기
~~~

### 2D Array
- 콤마(,)를 통해 2차원 Array 생성

~~~python
np_2d = np.array([[167, 170, 175, 165], [65, 72, 70, 59]]) #전체를 대괄호로 싸고 각 차원별 리스트도 대괄호로 싸야한다

np_2d
array([[167, 170, 175, 165],
       [ 65,  72,  70,  59]])

np_2d.shape #행렬의 구조 파악
(2, 4) #2행 4열, 2rows, 4columes

np_2d[1] #1row 행렬 호출
array([65, 72, 70, 59])

np_2d[1][3] #1row,3columes 호출
[31]: 59

np_2d[1,3] # 같은 결과
[32]: 59

~~~
- 아래 테이블을 보면 조금 더 이해하기 쉽다.

| |0 col|1 col|2 col|3 col| |
|---|---|---|---|---|---|
array|167|170|175|165|**0 row**|
  ||65|72|70|59|**1 row**|

### 주요 함수
- np.mean()
- np.median()
- np.corrcoef()
- np.std()
- np.sum()
- np.sort()

~~~python
np_2d
array([[167, 170, 175, 165],
       [ 65,  72,  70,  59]])

np.mean(np_2d[:,0])
116.0

np.median(np_2d[:,0])
116.0

np.corrcoef(np_2d[:,0], np_2d[:,1])
array([[1., 1.],
       [1., 1.]])

np.std(np_2d[:,0])
51.0
~~~
