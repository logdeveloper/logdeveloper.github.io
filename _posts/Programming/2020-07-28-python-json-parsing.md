---

title: "[Python] json format parsing"
categories:   
  - Python
last_modified_at: 2020-07-28T11:00:00+09:00
toc: true
toc_sticky: true
toc_label: "페이지 주요 목차"
tags:
  - Python
  - Json
  - jsonload
sidebar:
  nav: posts
---

python에서 json타입 파일을 parsing하는 방법에 대해서 알아보자.

## 1. json file 호출


```python
import json as js

with open('example.json') as json_file:
    json_data = js.load(json_file)
```


```python
# 데이터 확인
json_data
```
> {'json_string': 'string_example',
     'json_number': 100,
     'json_array': [1, 2, 3, 4, 5],
     'json_object': {'name': 'John', 'age': 30},
     'json_bool': True}


## 2. string type


```python
json_string = json_data["json_string"]
print(json_string)
```

> string_example



## 3. number type


```python
json_number = json_data["json_number"]
print(json_number)
```
> 100



## 4. Array type


```python
json_array = json_data["json_array"]
print(json_array)
```
> [1, 2, 3, 4, 5]



## 5. Object type


```python
json_object = json_data["json_object"]
print(json_object)
print(json_object["name"])
```
> {'name': 'John', 'age': 30}
    John


## 6. Boolean type


```python
json_bool = json_data["json_bool"]
print(json_bool)
```
> True

   