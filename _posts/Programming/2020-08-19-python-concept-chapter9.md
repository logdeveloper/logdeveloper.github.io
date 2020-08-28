---
title: "[Python] Chapter9 반복문 for"
categories:   
  - Python
last_modified_at: 2020-08-19T11:00:00+09:00
toc: true
toc_sticky: true
toc_label: "목차"
tags:
  - 구구단 출력
  - for 문
  - 자음 모음 집계
  - list for 활용
sidebar:
  nav: posts

---

## Chapter9 반복문 for 
### for
- 반복 ( 은 동일한 문장을 여러 번 반복시키는 구조
- 컴퓨터는 인간과 다르게 반복적인 작업을 실수 없이 빠르게 할 수 있으며 , 이것이 컴퓨터의 가장 큰 장점
- 만약 1000 번의 같은 명령어를 반복해야 한다면 다음과 같이 작성 해야함
- 파이썬에서는 2 가지 형태의 반복문 지원
    - for 문 정해진 횟수만큼 반복
    - while 문 어떤 조건이 만족되는 동안 반복
- for 문 형식

    > for a in iterable
    
    iterable : string, list, range( ) 등 셀 수 있는 데이터 모임 순서열 형식 데이터
    a : iterable 의 원소 값을 갖는 변수
    for 문 iterable 의 모든 원소값을 차례로 a 로 참조 하여 , for 내의 명령을 반복 수행 .
    
- 수행 순서
    ① 예약어 in 다음에 지정되어 있는 iterable object 에서 차례로 데이터를 참조
    ② 참조한 데이터를 예약어 for 다음에 명시한 변수 a 에 저장함
    ③ 코드 블록을 수행 . iterable object 에서 참조할 더 이상의 원소가 없으면 반복을 종료    
### for 문과 리스트

```python
L = [1, 3, 6]
for x in L :
    print (x, end="") # 출력 : 1 3 6
print ("")
```

### for 문과 문자열
- 문자열에 대한 반복

```python
for char in "Seoul" :
    print(char, end='#')
```

    ① 변수 char 에 첫번째 문자 S” 할당
    ② 출력문 실행
    ③ 문자열에 있는 문자들이 차례로 변수 char 에 할당되어 출력문 실행을 반복
    ④ 마지막 문자 "l" 까지 할당하여 반복코드를 수행 후 for 문을 종료

- 문자열을 입력 받아 모음을 전부 없애는 코드

```python
s = input(' 문자열을 입력하시오 :')
vowels = " aeiouAEIOU"
result = ""
for letter in s:
    if letter not in vowels:
        result += letter
print(result)
```

- 문자열을 입력 받아 자음과 모음의 개수를 집계하는 코드

```python
string = input(' 문자열을 영어로 입력하시오 :')
vowels = 0
consonants = 0
if len (string) > 0 :# 빈 문자열이 입력된 경우 검사
    for char in string :
        if char.isalpha () :# 영어 대소문자인 경우만
            if char in ' aeiouAEIOU ':
                vowels += 1
            else:
                consonants += 1
                print(" 모음의 개수 ",vowels)
                print(" 자음의 개수 ",consonants)
else :
    print (" 빈 문자열입니다")  

```


### for 문과 range()
- range() 함수
    - object type 이 range 인 일련의 정수 sequence 를 생성 하는 함수 . 
    - 함수 단독으로는 사용이 어려우며 , 주로 for loop 와 함께 사용
    - range(start, end, step)
    - start 부터 end 1 까지 step 씩 증가 하면서 sequence 생성
    - 슬라이싱에서의 start, end, step 가 같은 의미
    
    ```
    range (5)# sequence 0, 1, 2, 3, 4
    range (1, 6)# sequence 1, 2, 3, 4, 5
    range (4, 10, 2)# sequence 4, 6, 8
    range (5, 1, 2)# sequence 5, 3, 1
    range (9, 0)# empty sequence(9 > 0) 이므로
    
    L = [1, 3, 6]
    for i in range len (L)) :# i 0,1,2
    L[ i ] = L[i]**2 # L[i] 값이 바뀜
    print ( L) # 출력 : [1,9,36]
    
    ```

- range() 함수가 생성한 sequence 를 list, tuple, set 등 다른 데이터 형으로 변환하여 사용
- range() 함수가 생성한 sequence 를 반복문의 반복 횟수 제어에도 사용
    
### 리스트 내포 (list comprehension)

```python
a = [1, 2, 3, 4]
result = [ ]
for num in a:
    result.append(num *3)
print(result) # [3, 6, 9,12]

```

### continue
- continue 명령어는 현재 loop 에서 continue 문 다음 명령어들 코드 블록 내에서 을 실행하지 않고 반복문의 처음 으로 돌아감
- 프로그램 흐름
    - if 문을 이용해서 continue 문을 실행할 조건 체크
    - 조건이 True 이면 continue 문이 실행되어 반복문의 처음으로 돌아가고 , False 이면 코드 블록내의 나머지 명령어들을 실행
    - 조건이 True 일때 continue 문 전에 실행할 명령어가 있다면 추가 가능

- 1 부터 20 까지의 수 중에서 3 이나 4 로 나누어지는 수를 제외한 숫자들을 차례로 출력하는 코드
  
```python
for x in range(1, 21) :
    if x % 3 == 0 or x % 4 == 0 :
        continue
    print(x, end=" ")
print()
```

### break
- break 명령어는 현재 loop 에서 반복문을 종료하며 loop 을 빠져나옴
- 프로그램 흐름
    - if 문을 이용해서 break 문을 실행할 조건 체크
    - 조건이 True 이면 break 문이 실행되어 loop 을 빠져 나가고 , False 이면 코드 블록 내의 나머지 명령어들을 실행
    - 조건이 True 일때 break 문 전에 실행할 명령어가 있다면 추가 가능

```python
for v in iterable :
    statements
    if condition
        statements
        break
    ...
    statements
statements

```

- 자연수 N 이 소수 (a prime number) 인지 판단하는 코드

```python
N = int (input ("N(> 1)?"))
primeChk = True
for k in range (2, N) :
    if N % k == 0 :
        primeChk = False
        break # N-1까지 안돌아도 됨.
if primeChk == True :
    print("prime")
else :
    print("not prime")

```

### pass
- pass 명령어는 프로그램에 미완성 부분이 있을 때 , 이를 지금 작성하지 않고 나중에 작성하려 할 때 사용
- 프로그램을 테스트해가며 점차적으로 작성할 때 , 또는 해당 부분을 다른 사람에게 작성을 부탁할 때 사용
  
    ```    
    for x in range( 1, 11 ) :
        pass # 나중에 작성하고자 할 때 사용
    ```
    
### Nested for loop
- for loop 안에 또 다른 for loop 가 포함
- loop 안에 if 문 , while 문 등 어떤 것도 올 수 있음
- 각 코드 블럭은 확실하게 들여쓰기를 해서 구별해야 함
- * 기호를 삼각형 모양으로 출력하는 프로그램
```python
for x in range(1, 6):
    for y in range(x):
        print("*", end="")
print("") # 내부 반복문이 종료될 때마다 줄바꿈 실행

```

- 구구단 출력하는 프로그램
```python
for x in range(1,10) :
    for y in range(1,10) :
        print('%d*%d = %2d' % (x, y, x*y), end=' ')
print()

```

- 개수를 모르는 데이터 입력 받는 파이썬 코드
    > L=list( int (x) for x in input("Numbers? ").split())