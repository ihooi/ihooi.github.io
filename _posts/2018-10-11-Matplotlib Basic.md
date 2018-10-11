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
