---
title: Importing Data_Flat file and other file type
key: 20191122
tags: python, pandas, numpy
---

### Flat file
#### Text file 불러오기
- .txt과 같은 Plain한 텍스트 데이터

```python
filename = 'little_prince.txt'    # Working Directory에 파일이 있어야 할듯

file = open(filename, mode='r')    # 'r'은 Read only. 'w'은 Write

text = file.read()

file.close() # 종료시켜줘야 함
```

- Text가 길 경우에는 위와 같은 방식으로 출력하면 낭패일 수 있음
- 그럴 경우 한 줄씩 읽어올 필요가 있음

```python
### With ~ as를 활용 ###

with open('little_prince.txt') as file:
    print(file.readline())
    print(file.readline())
    print(file.readline())
```



#### CSV File 불러오기

- CSV(Comma-Seperated Values)로 쉼표나 탭 등으로 필드가 구분되어 있음
- Column: 열. 각 열은 속성으로 구분되어 있음
- Row: 행. 각 행은 Unique ID에 따른 값들로 구성되어 있음



### Numpy를 통한 Flat File 불러오기

~~~python
import numpy as np      #numpy를 불러오면서 이후에는 'np'라고 줄여서 호출
filename = 'MNIST.txt'
data = np.loadtxt(filename, delimiter=',', skiprows=1, usecols=[0,2], dtype=str)
#쉼표로 구분되어져 있다, 첫번째 행은 스킵한다, 열은 첫번째와 두번째만 사용한다, 데이터는 스트링으로 처리한다)
~~~



### Pandas를 통한 Flat File 불러오기

- R에서의 DataFrame 역할을 하는 패키지
- EDA, 데이터 전처리, 모델링, 시각화 등의 기능을 제공

~~~python
import pandas as pd
filename = 'winequality-red.csv'
data = pd.read_csv(filename)
~~~



### Pickled File

~~~python
import pickle

with open('data.pkl', 'rb') as file:
    d = picke.load(file)
    
print(type(d))
<class: 'dict'>
~~~



### Excel File

~~~python
import pandas as pd

file = 'battledeath.xlsx'

xls = pd.ExcelFile(file)  #pd.뒤에 명령어로 다양한 포멧의 파일을 열수 있음
print(xls.sheet_names)  #각 Sheet의 이름 확인

df1 = xls.parse('2004')  #'2004' Sheet의 내용을 파싱
df2 = xls.parse(1, usecols=[0], skiprows=[0], names=['Country'])
# Sheet명이 아니라 Sheet의 순서로 파싱, 특정컬럼만 사용, 특정행 스킵, 컬런네임 지정
~~~



### SAS File

- SAS 프로그램의 확장자

~~~python
import pandas as pd
from sas7bdat import SAS7BDAT #import할때는 대문자로

with SAS7BDAT('sales.sas7bdat') as file:
    df = file.to_data_frame()
~~~



### Stata File

- 'Statistics'+'data'

~~~python
import pandas as pd

df = pd.read_stata('disarea.dta')  # pd.read_ExcelFile()와 유사
~~~



### HDF5 File

- Hierarchical Data Format version 5
- 대용량 파일에 주로 사용

~~~python
import numpy as np
import h5py

file = 'LIGO_data.hdf5'
data = h5py.File(file, 'r')  #'r'은 read only

group = data['strain']  #서브세팅

for key in group.keys():
    print(key)

strain = data['strain']['Strain'].value
# Set variable equal to time series data: strain
~~~



### MATLAB file

~~~python
import scipy.io

mat = scipy.io.loadmat('data.mat')
print(mat.keys())

data = mat['ASA'][25, 5:]  #서브세팅
~~~

