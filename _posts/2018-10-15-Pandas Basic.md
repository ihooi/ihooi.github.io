---
title: Pandas Basic
key: 20181015
tags: python, Pandas
---

### Pandas
- DataFrame을 다루기 위해서는 Pandas Package를 사용한다
- Numpy가 2차원 행렬을 다룬다면 Pandas를 통해 보다 수준높은 데이터 연산이 가능해진다

~~~python
dict = {
        "name" : ["Jack", "Phillip", "Robert", "Adam"],
        "last": ["lee", "song", "kim", "park"],
        "age" : [26, 32, 45, 55],
        "height": [180.2, 169.8, 175.3, 192.1]
        } # Dictionary 만드는 방법도 참고

import pandas as pd

friend = pd.DataFrame(dict)

friend

      name      last  age  height
0     Jack       lee   26   180.2
1  Phillip      song   32   169.8
2   Robert       kim   45   175.3
3     Adam      park   55   192.1

friend.index = ["JL", "PS", "RK", "AP"]  # 인덱스 Name을 변경할 수 있다.

friend

       name      last  age  height
JL     Jack       lee   26   180.2
PS  Phillip      song   32   169.8
RK   Robert       kim   45   175.3
AP     Adam      park   55   192.1

~~~

- CSV 파일을 읽어서 작성하면 더 편리하다

~~~python
friend = pd.read_csv("c:/Users/hoseok/Documents/friend.csv") # 역슬래시(\)로 위치 지정했더니 오류남

friend
  Unnamed: 0     name  last  age  height
0         JL     Jack   lee   26   180.2
1         PS  Phillip  song   32   169.8
2         RK   Robert   kim   45   175.3
3         AP     Adam  park   55   192.1

friend = pd.read_csv("c:/Users/hoseok/Documents/friend.csv", index_col=0) #인덱스 컬럼의 위치 지정

friend
       name  last  age  height
JL     Jack   lee   26   180.2
PS  Phillip  song   32   169.8
RK   Robert   kim   45   175.3
AP     Adam  park   55   192.1
~~~

### Data Selection
- 만들어진 DF는 []로 select 할 수 있다

~~~python
friend["last"]

JL     lee
PS    song
RK     kim
AP    park
Name: last, dtype: object

type(friend["last"])
pandas.core.series.Series  # 1차원 labelled 행렬을 의미

friend[["name", "last"]] # 대괄호 두개를 통해 DF 형태로 Select.
       name  last
JL     Jack   lee
PS  Phillip  song
RK   Robert   kim
AP     Adam  park

friend[1:3] #friend의 1 row 부터 2 row 까지 호출
       name  last  age  height
PS  Phillip  song   32   169.8
RK   Robert   kim   45   175.

~~~

### loc / iloc
- 대괄호를 통한 방법은 한계가 있음
- Pandas에는 loc와 iloc가 있음
  - loc (label-based) ~~'Label of Colume 인가?'~~
  - iloc (inter position-based)

#### loc
- label로 데이터를 불러온다

~~~python
friend

       name  last  age  height
JL     Jack   lee   26   180.2
PS  Phillip  song   32   169.8
RK   Robert   kim   45   175.3
AP     Adam  park   55   192.1

type(friend)
pandas.core.frame.DataFrame

friend.loc["JL"]  #레이블 명으로 데이터를 호출한다

name       Jack
last        lee
age          26
height    180.2
Name: JL, dtype: object

friend.loc[["JL", "AP"]]  #대괄호를 두개 써서 복수의 레이블을 부를 수도 있다

    name  last  age  height
JL  Jack   lee   26   180.2
AP  Adam  park   55   192.1

friend.loc[:, ["age", "height"]]  ## 모든 레이블값을 가져오되 특정 컬럼만 가져오기

    age  height
JL   26   180.2
PS   32   169.8
RK   45   175.3
AP   55   192.1
~~~

#### iloc
- loc와 동일하다 index number로 호출한다

~~~python
friend.iloc[0]

name       Jack
last        lee
age          26
height    180.2
Name: JL, dtype: object

friend.iloc[[0,3]]

    name  last  age  height
JL  Jack   lee   26   180.2
AP  Adam  park   55   192.1

friend.iloc[:, [2,3]]

    age  height
JL   26   180.2
PS   32   169.8
RK   45   175.3
AP   55   192.1
~~~
