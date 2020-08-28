---
title: "[Python] Chapter6 조건문"
categories:   
  - Python
last_modified_at: 2020-08-16T11:00:00+09:00
toc: true
toc_sticky: true
toc_label: "목차"
tags:
  - if 문
  - 조건문
  - 
sidebar:
  nav: posts

---

## Chapter6 조건문
### if
- 조건문 (Conditional 은 어떤 상황에 따라 실행해야 할 코드가
다를 때 사용
- if 조건문의 형식
    - 조건식 ( 이 참이면 같은 크기로 들여쓰기 되어 있는 명령어들 코드 블록 이 처리되고 , 거짓이면 실행하지 않음

### if else 
- 조건 ( 이 False 일 때도 수행할 일이 있다면 else 를 사용

### 조건(condition)
- if 조건문에서 조건 이란 참과 거짓을 판단하는 문장을 말함
- 조건을 판단하기 위해 사용되는 문장
    - 자료형의 참과 거짓 boolean
    - in 연산자 , not in 연산자
    - 관계연산자
    - 논리연산자
    
- 자료형의 값으로 참과 거짓을 결정

자료형  | 참 |거짓
------- | ------- | ------- | 
숫자  |0 이 아닌 숫자 | 0
문자열 | "abc"  |""
리스트 | [1,2,3]  | []
튜플 | (1,2,3) |()
딕셔너리 | {a":"b}  |{}

- Python 에서는 0 , 0.0 , 빈 문자열 ) 등은 모두 False 로 간주하고
나머지 값들은 모두 True 로 간주

### if else 예제
- 입력된 연도가 윤년인지 아닌지를 판단하는 프로그램

    ```
    year =int ( 연도를 입력하시오 : "))
    if ( (year % 4 ==0 and year % 100 != 0) or year % 400 == 0):
        print(year, "년은 윤년입니다")
    else :
        print(year, "년은 윤년이 아닙니다")
    ```

### if ~ elif ~ else 
- 다양한 조건을 판단하기 위해 사용
    - elif 는 앞 조건문이 거짓일 때 다시 조건을 검사하는 if 문
    - 마지막 else 는 불필요하면 생략 가능
      
      ```  
        if cond1 :
            statement1
        elif cond2 :
            statement2
        elif cond3 :
            statement3
        else :
            statement4
      ```

### 중첩 if
- 조건을 확인 후 또 다른 조건을 검사해야 하는 경우 , 중첩된 if else 구조를 사용
    - if 문의 코드 블록 안에 또 다른 if 문을 사용
