---
title: "[Python] Chapter12 함수2 "
categories:   
  - Python
last_modified_at: 2020-08-22T11:00:00+09:00
toc: true
toc_sticky: true
toc_label: "목차"
tags:
  - 함수
  - 지역 변수
  - 전역 변수
sidebar:
  nav: posts

---

## Chapter12 함수2
### 지역 (local) 변수 전역 (global) 변수
- 변수가 생성되는 시점은 변수에 값을 할당할 때이며 , 변수 참조 가능 영역을 기준으로 변수를 구분
- 스코프 ( 는 변수가 참조될 수 있는 프로그램의 영역을 일컫는 용어
- 전역 변수 (global variable)
    - 모든 함수의 외부에서 생성되며 , 모든 함수에서 접근 가능
    - 즉 , 프로그램 전체에서 사용 가능
    - 전역변수를 함수 안에서 수정하면 새로운 지역변수가 새로 생성
- 지역 변수 (local variable)
    - 함수 내에서 생성된 변수 및 매개변수 는 지역 변수
    - 함수 내에서만 사용 가능
    - 함수 종료 후 소멸
- 프로그램에서 변수를 참조할 때 찾는 순서는 지역 변수 → 전역 변수 순서로 찾음
- 전역변수와 같은 이름의 변수를 함수 안에서 할당 대입 , 저장 하면 같은 이름의 지역변수가 새로 생성됨

```python
def classify_var
    globalS = "I like only this!" # 지역변수 globalS
    localS = "It's local variable!"# 지역변수 localS
    print( globalS )# I like only this! 지역변수 globalS 의 값 출력
    print( localS )# It's local variable!
globalS = "I like all everything!" # 전역변수 globalS
classify_var()
print( globalS )# I like all everything! 전역변수 globalS 의 값을 출력
print( localS )# NameError : name localS ' is not defined
```

- 지역 변수 값은 함수 종료 후 소멸하므로 return 을 통하여 함수 밖에서 그 값 사용해야 함
- 값에 참조 접근 , 읽기 만 할 경우 지역변수 전역변수 순서로 찾아서 참조한다
- 이미 함수 내에서 변수를 지역변수로 사용 하고 있는 경우: 먼저 할당하고 난 뒤 참조해야 한다

### 인수 (argument) 전달
- 파이썬에서 모든 데이터는 객체이며 , 변수는 그 객체에 대한 참조 
- 함수를 호출하면 , 인수 객체의 참조 값 주소 값 이 매개변수로 전달 할당 , 복사
- 즉 , 인수와 매개변수가 동일한 객체를 가리키게 됨
- Immutable 객체의 참조 값을 매개변수로 전달한 후 변수를 수정하는 경우 
    - 매개변수는 지역 변수이기 때문에 함수 종료 시 변수 소멸
- 리스트 , 집합 , 사전 등 mutable object 를 인수로 해서 함수를 호출하면 , 아래 그림과 같음
    - 매개변수로 mutable object 의 원소를 수정하면 인수로 사용한 변수가 가리키는 object 도 변경됨
