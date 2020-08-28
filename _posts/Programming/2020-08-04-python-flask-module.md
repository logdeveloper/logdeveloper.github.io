---
title: "[Python] python flask 모듈 "
categories:
  - Python
last_modified_at: 2020-07-31T11:00:00+09:00
toc: true
toc_sticky: true
toc_label: "목차"
tags:
  - flask
  - module
  - marshal
  - marshal_with  
sidebar:
  nav: posts
---

## marshal 

- marshal 모듈 원시데이터(dict, list, object 형식) 및 필드 dict를 사용하여 해당 필드를 기반으로 데이터를 출력하고 필터링함.
- 바이너리 형식으로 파이썬 값을 읽고 쓸수 있는 함수를 포함.
- `직렬화` 하는 것을 의미

### 매개변수 

- data : 필드를 가져 오는 실제 객체
- fields : 최종 직렬화 된 응답 출력을 구성하는 키의 기준
- envelope : 직렬화 된 응답을 감싸는 데 사용될 선택적 키 



```python
from flask_restful import fields, marshal

data = {'a':100, 'b':'foo'}
mfields = {'a':fields.Raw}
```


```python
marshal(data, mfields)
```




    OrderedDict([('a', 100)])




```python
# data라는 키워드에 한번 감싸서 출력
marshal(data, mfields, envelope='data')
```




    OrderedDict([('data', OrderedDict([('a', 100)]))])



## marshal_with
- 메소드의 리턴 값에 마샬링을 적용하는 데코레이터


```python
from flask_restful import fields, marshal_with
mfields = {'a':fields.Raw}

@marshal_with(mfields)
def get():
    return {'a':100, 'b':'foo'}

get()

```




    OrderedDict([('a', 100)])



## marshal_with_field(필드)
- 단일 필드로 메소드의 리턴 값을 형식화하는 데코레이터


```python
from flask_restful import marshal_with_field, fields

# 리스트의 원소들을 Integer 타입으로 마샬링(직렬화)
@marshal_with_field(fields.List(fields.Integer))
def get():
    return ['1', 2, 3.0 ]

get()
```




    [1, 2, 3]



## abort

- 주어진 http_status_code에 대해 HTTPException을 발생 시킴
- 나중에 처리할 수 있도록 키워드 인수를 예외에 첨부 
