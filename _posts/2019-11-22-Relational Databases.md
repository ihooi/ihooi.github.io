---
title: Relational Databases in Python
key: 20191122
tags: python, pandas, numpy, sql
---



### Relational Database

- 여러개의 테이블이 연결된 구조라고 이해하면 됨
- 예를 들어 주문테이블에 고객ID, 직원ID가 있다면 그와 연관된 고객정보가 들어간 테이블과 직원정보가 들어간 테이블이 있어서 서로 연결되어 있음
- PostgreSQL, MySQL, SQLite 등 많은 시스템이 존재
- 그 중에서 SQLite이 심플하고 빨라서 파이썬에서 잘 돌아가는 듯
- SQLAlchemy 패키지 활용

~~~python
from sqlalchemy import create_engine

engine = create_engine('sqlite:///Chinook.sqlite')

table_names = engine.table_names()
~~~



### SQL Query

~~~py
SELECT FROM WHERE ORDER BY INNER JOIN # 기본적인 명령어임
~~~

- 기본적인 방법

~~~python
from sqlalchemy import create_engine
import pandad as pd

engine = create_engine('sqlite:///Chinook.sqlite')  #엔진 생성
con = engine.connect()  #엔진 커넥션 생성
rs = con.execute("SELECT * FROM Orders") #쿼리 실행하여 저장
df = pd.DataFrame(rs.fetchall()) #DataFrame 형태로 저장, 전체를 다 땡겨옴(Fetch all)
con.close #커넥션 종료
~~~

- 다른 방식으로 

~~~python
from sqlalchemy import create_engine
import pandad as pd

engine = create_engine('sqlite:///Chinook.sqlite')  #엔진 생성

with engine.connect() as con:
    rs = con.execute("SELECT LastName, Title FROM Employee")
    df = pd.DataFrame(rs.fetchmany(size=5)) # 범위를 지정하여 당겨올 수 있음
    df.columns = rs.keys() #dataframe의 컬럼값을 rs에서 키값으로 지정
~~~

- 위와 같은 구조에서 쿼리만 바꿔본다면

~~~
"SELECT * FROM Employee WHERE EmployeeId >= 6"  #특정 조건을 걸어서 추출할 때 WHERE
"SELECT * FROM Employee ORDER BY BirthDate"  #정렬 조건을 걸때 ORDER BY
~~~

- Pandas를 쓰면 조금더 심플하게

~~~python
from sqlalchemy import create_engine
import pandas as pd


engine = create_engine('sqlite:///Chinook.sqlite')

df = pd.read_sql_query("SELECT * FROM Employee WHERE EmployeeID >= 6 ORDER BY BirthDate", engine)
# 위의 방식과 비교하면 한줄로 처리됨을 알 수 있다
# WHERE가 ORDER BY 보다 먼저
~~~

- INNER JOIN은 유심히 봐야한다

~~~python
with engine.connect() as con:
    rs = con.execute("SELECT Title, Name FROM Album INNER JOIN Artist on Album.ArtistID = Artist.ArtistID")

### Title과 Name을 선택하는데 Album 과 Artist 테이블에서 ArtistID를 조인해서
    df = pd.DataFrame(rs.fetchall())
    df.columns = rs.keys()
~~~

- 한번 더

~~~python
df = pd.read_sql_query("SELECT * FROM PlaylistTrack INNER JOIN Track on PlaylistTrack.TrackID = Track.TrackID WHERE Milliseconds < 250000", engine)

### 전체를 선택하는데 PlaylistTrack과 Track 테이블의 TrackID가 같은 것들을 조인하고 Millisecond가 250000보다 작은 아이들로
~~~

