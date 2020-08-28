---
title: "[Python] Chapter2 데이터"
categories:   
  - Python
last_modified_at: 2020-08-12T11:00:00+09:00
toc: true
toc_sticky: true
toc_label: "목차"
tags:
  - 데이터
  - 파이썬
  - 자료형
sidebar:
  nav: posts

---

## Chapter2 데이터
### 자료형 (Data Types)
- 변수에 정수 , 실수 , 문자열 등의 다양한 형의 데이터를 대입하여 저장 가능
- python 에서는 기본적으로 다음과 같은 데이터형을 제공
    - 숫자 (numbers)
        - 정수 ( int): 7, 123, 256, etc.
        - 실수 (float) : 3.14, 1.2345, 3.0e+5 ,
        - 복소수 (complex) : 2.5+3.2j, 1+2j,
    - Boolean : True, False
    - 문자열 (string, str ) : "Hello", 'Hello', etc
    - 리스트 (list) : (5.5, 3, "Hello")
    - 집합 (set) : [1, 2.2, "Hello"]
    - 튜플 (tuple) : {1, 2, 3, 4,5}
    - 사전 (dictionary, dict ) : {'val1':1, 'val2':2}

- 문자열 형
    - 문자열은 양쪽을 큰따옴표 나 작은따옴표 로 감싼 문자들의 모임

### 변수(Variable)
- 변수는 객체를 가리키는 심볼
- Python 에서 symbol 은 수학에서의 equality 와 차이가 있음
- 할당 연산자의 오른쪽에 오는 변수는 반드시 값이 할당된 변수를 사용해야 함

### 자료형 확인
- 내장 함수 type( )
    - Object 의 데이터 형 (data type) 을 알려주는 함수

### 자료형 변환
- 정수 , 실수 , 문자열 등의 자료형들은 다른 자료형으로 변환될 수 있으며 , python 에서는 이를 위한 내장 함수를 제공
- int() 함수
    - 소수점이 없는 숫자 형태의 문자열을 정수로 변환
    - 실수 형태의 문자열은 정수로 변환할 수 없음 : error
    - 실수 값을 정수로 변환
- float() 함수
    - 실수 형태의 문자열이나 정수를 실수로 형 변환
- str() 함수
    - 실수나 정수를 문자열로 형 변환

### 기타 알아야 할 사항
- 하나의 statement 를 여러 줄을 사용하여 작성할 때는 backslash( \\) 를 사용한다
- 한 줄에 두 개 이상의 statement 를 넣을 때는 semicolon( ; ) 을 사용하여 구분한다

### 변수명 규칙
- 변수명은 영어 대소문자 , 숫자 , 밑줄 로만 이루어짐
    - Money$ : 문자 는 사용할 수 없음
- 변수명은 영어 대소문자 또는 밑줄로만 시작
-    7up, 5brothers : 숫자로 시작할 수 없음
- 파이썬 지정단어 (Keyword, Reserved 들은 사용 불가
- 파이썬에서는 대문자와 소문자를 구분
    - hour 와 Hour 는 다른 변수

- 잘못된 식별자 변수명    
    - 2nd_base # 숫자로 시작할 수 없음
    - #money # 과 같은 기호는 사용할 수 없음
    - varname $$# 특수 문자 를 사용할 수 없음
    - id name # 중간에 공백 문자를 사용할 수 없음
    - for # 예약어 for 를 변수명으로 사용할 수 없음`

