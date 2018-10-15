---
title: Dictionary
key: 20181012
tags: python, dictionary
---

### 개념
- 리스트에서 특정 값을 다른 변수로 지정할 수는 있지만 불편하다
- dictionary는 말 그대로 표제어:뜻 처럼 key:Value 형태로 만들 수 있다
- 리스트는[ ]이지만 dictionary는{ }이다

~~~python
cars = [100, 330, 204, 403]
city = ['인천', '일산', '수원', '서울']
# 위와 같이 할 수 있겠지만 나중을 생각하면 불편하다

carsincity = {'인천':100, '일산':330, '수원':204, '서울':403}
carsincity['서울']
403

carsincity = {'인천':100, '일산':330, '수원':204, '서울':403, '일산':350} #키를 중복으로 입력하면 나중 것으로 Value가 바뀐다. key가 두 개 생기지 않는다!!

carsincity
{'인천': 100, '일산': 350, '수원': 204, '서울': 403}

# 키가 Dictionary에 있는지 확인 가능하다
'서울' in carsincity
True

# 키를 지우면 Value도 함께 삭제된다
del(carsincity['인천'])
carsincity
{'일산': 350, '수원': 204, '서울': 403}
~~~
