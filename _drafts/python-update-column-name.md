---
title: "[Python] 데이터 과학을 위한 통계 6-1"
categories:
  - Python
last_modified_at: 2020-07-23T11:00:00+09:00
toc: true
toc_sticky: true
toc_label: "페이지 주요 목차"
tags:
  - 
  - 
  - 
  - 

sidebar:
  nav: posts

---



```python
df1 = pd.DataFrame([['부산', '부산', '부산', '부산', '서울', '서울', '서울'],
    ['apple', 'orange', 'banana', 'banana', 'apple', 'apple', 'banana'],
    [100, 200, 250, 300, 150, 200, 400],
    [1, 2, 3, 4, 5, 6, 7]])
df1 = df1.T
df1
```

![1596762711063](python-update-column-name.assets/1596762711063.png)

```python
# 특정 컬럼 하나만 수정
df1.rename(columns={0:'city'}, inplace=True)
df1
```

![1596762723162](python-update-column-name.assets/1596762723162.png)

```python
# 복수개의 컬럼 이름 설정 
df1.rename(columns={1:'fruits', 2:'price'}, inplace=True)
df1
```

![1596762734587](python-update-column-name.assets/1596762734587.png)



> 참고 사이트 
>
> [pandas-docs](<https://pandas.pydata.org/pandas-docs/stable/reference/offset_frequency.html>)
>
> [Python Pandas 데이터 분석](<https://ponyozzang.tistory.com/291>)