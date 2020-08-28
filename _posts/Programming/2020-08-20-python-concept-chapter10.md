---
title: "[Python] Chapter10 반복문 while"
categories:   
  - Python
last_modified_at: 2020-08-20T11:00:00+09:00
toc: true
toc_sticky: true
toc_label: "목차"
tags:
  - while
  - 정수의 각 자리수 합 계산
sidebar:
  nav: posts

---

## Chapter10 반복문 while
### while
- while 문은 조건을 정해놓고 반복을 하는 구조
- while statement syntax
- while 을 사용한 1 + 2 + …+ N 계산 프로그램

```python
N = 10
sum = 0 # sum 을 0 으로 초기화
i = 1 # range 대신 counter i 를 사용
while i <= N :
    sum = sum + i # sum 을 누적 (accumulation)
    i = i+1 # counter 1 증가
print("The sum is", sum) # 출력 : The sum is 55

```

- 정수의 각 자리수의 합을 계산하는 프로그램 ( 1234 라면 1+2+3+4 를 계산하는 것)

```python
number = 1234
sum = 0;
while number > 0 :
    digit = number % 10
    sum = sum + digit
    number = number // 10
print(" 자리수의 합은 %d 입니다 ." %sum)

# 출력 : 자리수의 합은 10 입니다
```

### break 
- break 명령어의 기능은 for 반복문과 같음
- 자연수 N이 소수(a prime number)인지 판단하는 코드

```python
N = int(input("N(> 1)? "))
k = 2
primeChk = True
while k < N :
    if N % k == 0 :
        primeChk = False
        break
    k = k + 1
if primeChk == True :
    print("prime")
else :
    print("not prime")
```

- 무한 루프와 break

    > while(True) : 무한 루프

- 0 이 아닌 임의의 자연수를 횟수에 상관없이 입력 받는 프로그램

```python
while(True) :
    n = int (input('Enter the number :'))
    if n==0 : #0 가 입력되면 loop 종료
        break
print(n)

```

### continue
- continue 명령어의 기능은 for 반복문과 같음
