---
title: Python Random Numbers
key: 20181017
tags: python, RandomNumber, Algorithm
---

> 이 부분은 임의의 코드를 짜기보다는 강의를 따라하는 것이 좋을 것 같아 부득이하게 DataCamp 강의 내용을 인용했다.
<br>
> All of code in this post is from DataCamp. because I guess this example would be more efficient way to understand random numbers

### Randon Generators
- Numpy의 `np.random.rand()`함수를 통해 랜덤 숫자를 뽑을 수 있다.
- 매번 다른 숫자가 랜덤으로 나온다

~~~python
import numpy as np

np.random.rand()
0.2640266117997808

np.random.rand()
0.6419753427498596
~~~

- `np.random.seed()`를 사용하면 같은 랜덤 숫자를 반복적으로 뽑을 수 있다

~~~python
np.random.seed(1)

np.random.rand()
0.417022004702574

np.random.rand()
0.7203244934421581

#Seed를 지정하면 랜덤 숫자가 동일하게 재현된다
np.random.seed(1)

np.random.rand()
0.417022004702574

np.random.rand()
0.7203244934421581

~~~

### 예제를 통한 이해
#### 동전 던지기
- 동전을 던져서 '0'이면 head, '1'이면 tails로 지정해보자
- 동전을 10번 던져서 결과를 뽑아보자

~~~python
np.random.seed(111) #Seed를 먼저 지정하여 재현성을 확보

result = [] #빈 리스트를 만든다

for n in range(10): #range(범위)
    coin = np.random.randint(0, 2) # random integer(최소값, 초과값(2는 나올수 없다))
    if coin == 0:
        result.append("heads") # .apped() 함수의 활용!!
    else:
        result.append("tails")
print(result)


['heads', 'heads', 'heads', 'heads', 'heads', 'tails', 'tails', 'heads', 'heads', 'heads']
~~~

- tails가 나올 때마다 카운트를 늘려간다면?

~~~python
np.random.seed(123)

tails = [0]

for x in range(10) :
    coin = np.random.randint(0,2)
    tails.append(tails[x] + coin) #tails 리스트에 coin으로 랜덤 숫자를 더해서 리스트에 추가
print(tails)

[0, 0, 1, 1, 1, 1, 1, 1, 2, 3, 3] # 결국 tails 즉, '1'이 3번 나왔다는 이야기가 된다
~~~

- 그럼 10번 던지기를 100번 했을 경우

~~~python
np.random.seed(1)

final_tails = []

for x in range(100):
    tails = [0]
    for x in range(10):
        coin = np.random.randint(0,2)
        tails.append(tails[x] + coin)
    final_tails.append(tails[-1])
print(final_tails)


[7, 4, 3, 5, 8, 5, 6, 5, 6, 6, 5, 5, 7, 5, 5, 4, 4, 4, 2, 5, 5, 5, 6, 7, 7, 5, 5, 5, 4, 4, 4, 7, 4, 8, 1, 4, 3, 4, 6, 3, 6, 3, 6, 5, 7, 1, 5, 4, 6, 3, 7, 5, 3, 5, 3, 3, 7, 3, 3, 5, 3, 7, 4, 4, 2, 2, 6, 6, 2, 4, 6, 8, 6, 2, 5, 6, 4, 4, 4, 8, 7, 6, 5, 3, 3, 3, 6, 5, 4, 8, 5, 6, 5, 3, 5, 5, 7, 7, 2, 2]
~~~

- 일반화를 위해 10번 던지기를 10,000번하고 그래프를 그려보자

~~~python
import numpy as np
import matplotlib.pyplot as plt

np.random.seed(1)

final_tails = []

for x in range(10000):
    tails = [0]
    for x in range(10):
        coin = np.random.randint(0,2)
        tails.append(tails[x] + coin)
    final_tails.append(tails[-1])

plt.hist(final_tails, bins = 10)
plt.show()
~~~

![coin_hist](/IMG/coin_hist.png)


#### 주사위 던지기 조건
- 주사위를 100번 던진다
- '1', '2'가 나오면 한칸 뒤로 물러선다 (-1)
- '3'~'5'가 나오면 한칸 전진한다 (+1)
- '6'이 나오면 다시 던지고 __나온 숫자만큼 이동한다__
- '0' 이하로 물러설 수 없다
- 시뮬레이션을 통해 분산을 확인
