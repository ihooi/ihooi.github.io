---
title: Matplotlib Basic
key: 20181011
tags: python, Matplotlib
---

### Data Visualization
- 데이터 분석에서 시각화는 매우 중요한 부분
- 데이터를 탐색하거나 인사이트를 제공할 수 있다

### Matplotlib
- 손쉽게 그래프를 그릴 수 있는 Package
- Import 시 주의할 점은 Sub package를 부른다는 것

~~~python
import Matplotlib.pyplot as plt   # .pyplot에 주목하자
~~~

- plt.plot: 일반 선 그래프 생성
- plt.show(): 그래프 확인

~~~python
import matplotlib.pyplot as plt

year = [1990, 2000, 2010, 2018]

height = [59, 65, 78, 72]

plt.plot(year ,height)
plt.show()
~~~

![plot](./IMG/heightplot.png)

그래프 표현이 잘 안되고 있음
{:.warning}

- plt.scatter(): 산점도 그래프

~~~python
plt.scatter(year ,height)
plt.show()
~~~

![scatterplot](./IMG/heightscatter.png)

- plt.hist(): Histogram 분포도 그래프
  - 데이터 탐색 시 분포를 통해 idea를 얻을 수 있다
  - bins를 통해 단위를 지정할 수 있음

~~~python
x = [1,4,4,2,6,3,7,1,0,1,0,6,9,1,9,5,3,5,1,4,5,1,3,4,5,1,4]

plt.hist(x, bin =2)
~~~

![hist](./IMG/hist.png)

### Customization
- 그래프 관련 많은 기능들이 있다

~~~python
plt.xlabel('x축 레이블')
plt.ylabel('y축 레이블')
plt.title('그래프제목')

plt.yticks([0,2,4,6,8,10]) # y축 눈금 표시
plt.ytics([0,2,4,6,8,10],['0','2y','4y','6y','8y','10y']) #y축 눈금값을 일정 텍스트로 변경

year = [1980, 1985] + year # 데이터 추가
height = [45, 50] + heght  # 데이터 추가
~~~
