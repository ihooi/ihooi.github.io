---
title: Importing Data_Flat file
key: 20190211
tags: python, List Comprensions, Generator
---

### Flat file
#### Flat file 불러오기
- .txt, .csv 과 같은 Plain한 데이터

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

