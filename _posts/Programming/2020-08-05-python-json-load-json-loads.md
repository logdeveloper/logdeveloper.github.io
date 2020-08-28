---
title: "[Python] json parsing "
categories:
  - Python
last_modified_at: 2020-08-05T11:00:00+09:00
toc: true
toc_sticky: true
toc_label: "목차"
tags:
  - python
  - json
  - parsing
sidebar:
  nav: posts
---





파이썬에서 제공하는  json 모듈을 사용하면 쉽게 json 파싱 작업을 할 수 있다. 

자주 사용하는 2가지 방법이 있는데, 데이터 형태에 맞는 메소드를 사용해야 한다. 





## json load

- 용도 : json 데이터가 있는 `파일`을 읽어오려면 `json.load()`를 사용.

```python
import json

with open("json_data.json", "r") as content:
  print(json.load(content))
```



## json loads

- 용도 : `str` 타입의 데이터를 읽어 오려면 `json.loads()` 를 사용 

```python
import json
json.loads('["foo", {"bar":["baz", null, 1.0, 2]}]')
```



파일 타입에서 불러올지,  text 그대로  따라 불러올지 명확하게 사용해야한다. 그렇지 않으면 타입에러가 발생하니 유의하자.

ps. json.load(), json.loads()는 `s` 한글자 차이 여서 오타가 나면 해매기 쉽다.





> 참고 사이트 
>
> [jsonload-와-jsonloads-함수의-차이점]((https://www.it-swarm.dev/ko/python/jsonload-와-jsonloads-함수의-차이점은-무엇입니까/828495653/))