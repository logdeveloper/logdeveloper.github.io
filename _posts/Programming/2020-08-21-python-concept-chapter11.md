---
title: "[Python] Chapter11 함수1 "
categories:   
  - Python
last_modified_at: 2020-08-21T11:00:00+09:00
toc: true
toc_sticky: true
toc_label: "목차"
tags:
  - 
  - 
  - 
sidebar:
  nav: posts

---

## Chapter11 함수1
### 함수 (Functions)
- 함수 (Functions) 는 특정 작업을 수행하는 명령어들의 모음에 이름을 붙인 것
- 함수는 작업에 필요한 데이터를 전달 받을 수 있으며 , 작업이 완료된 후에는 작업의 결과를 호출자에게 반환할 수 있음
- 자주 사용되는 부분 문제를 함수로 작성하면 코드를 반복 작성할 필요가 없기 때문에 편리하며 , 호출하여 재 사용하면 됨
- 파이썬에서 지원하는 세 종류의 함수
    ① 내장 (Built in) 함수 : Python 에서 제공하는 함수
    : python 설치 후 사용 가능 ( print(), input(), len (), type()..)
    ② 라이브러리 패키지 Python 에서 제공하는 모듈
    : 해당 모듈을 프로그램에 포함한 후에 사용할 수 있음 .
    ③ 사용자 정의 (User defined) 함수
    : 사용자가 자신의 필요에 따라 특정 기능의 함수를 직접 작성

- 함수 작성
  
```python
def function_name (parameters):
    """ docstring """ # 옵션.. 없어도 됨
    statements # 함수 기능에 필요한 statements
    return ret_values # 반환할 것이 없으면 생략 가능
```

    - def : 함수의 시작을 알림
    - 함수 이름 (function_name ) : identifier(변수 ) 규칙대로 이름 정의
    - parameters( 매개변수 )
        - 함수의 입력 (콤마로 분리 ), 필요하지 않으면 괄호만 표시
        - 함수 호출시 전달하는 데이터는 함수의 매개변수로 전달
        - 함수 호출시 전달하는 데이터를 인수 (argument) 라 함
    - """docstring""" : 주석 함수 설명 ), 생략 가능
    - return : 실행 결과를 호출한 코드로 반환 . 반환 값이 없으면 생략

### 함수 호출하기

```python
def checkOddEven ( N ) :# N 은 매개변수
    
    """
    docstring part
        Return True if N is even, else return False.
        by 20160000 홍길동
    """
    if N % 2 == 0 :
        return True # 값을 반환하며 함수 종료
    else:
        return False # return 문은 필요 시 여러 번 사용 가능
print ( checkOddEven (10) ) # True
M = 11
print ( checkOddEven (M) ) # False
```
- 입력 값과 반환 값이 모두 없는 함수 호출
  
    > func_name
    
    : 함수의 입력이 없으면 함수명 옆에 빈 괄호만 두며 , 반환값이 없기 때문에 값을 반환 받을 변수에 할당할 필요가 없음

- 반환 값이 있는 함수 호출

    > var_name = func_name
    
    : 함수가 값을 반환하면 함수 호출이 반환 값으로 대체

- 인수 전달 : 위치에 따라 인수가 매개변수로 전달

```python
def get_sum ( start, end ):
    sum = 0
    for i in range(start, end+1) :
     sum += i
    return sum
sum1 = get_sum (1, 10)
sum2 = get_sum (20,30)
print(sum1, sum2) # 55 275
```

- 인수 전달 : 매개변수의 이름을 명시적으로 지정해서 인수를 전달

```python
def nPrint (message, n):
    for i in range(0, n) :
        print(message)
nPrint ("Hello",3)# 정상적인 호출
print() #줄바꿈
nPrint (n = 2, message = "Hello") # 정상적인 호출
```
- 함수의 반환값
    - return 키워드를 사용하여 값 반환값 을 호출자에게 반환
    - 함수에 return 문 없이 반환 값이 없거나 , return 예약어만 있는 경우는 반환값이 없는 함수이므로 None 을 기본적으로 반환

```python
def calculate_area (radius):
    area = 3.14 * radius**2
    return area

c_area = calculate_area (5.0)
print( c_area ) #78.5
```
- 함수에서 return 문이 여러 번 나오는 경우
    : return 문이 여러 번 나오더라도 먼저 만나는 return 문에서 함수는 값을 반환하고 종료

```python
def get_max (a,b ):
    if a > b :
        return a # a > b 경우이므로 a 값을 반환하면서 종료
    else:
        return b # a <= b 경우이므로 b 값을 반환하면서 종료
max = get_max (10, 20)
print(max) # 20
```
- 반환값이 여러 개인 경우
    : 반환값이 2 개 이상인 경우 튜플로 묶어서 반환

```python
def add_multiply (x,y):
    sum = x + y
    mul = x * y
    return sum, mul # 반환값 2 개를 튜플로 반환 .
a = int (input('Enter a : '))
b = int (input('Enter b : '))
m, n = add_multiply (a,b ) # 변수 m 은 a+b 의 값 , 변수 n 은 a*b 의 값을 할당 받음
print( m,n)
```

