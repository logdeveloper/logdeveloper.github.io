---
title: "[Python] Chapter7 리스트 "
categories:   
  - Python
last_modified_at: 2020-08-17T11:00:00+09:00
toc: true
toc_sticky: true
toc_label: "목차"
tags:
  - 리스트
sidebar:
  nav: posts

---

## Chapter7 리스트
### 리스트
- 같은 의미의 여러 데이터를 순서대로 저장하고 관리해야 할 때 사용
- 순서 있는 데이터를 저장하기 위한 object
- 어떠한 데이터 형도 원소 값이 될 수 있음
- 문자열처럼 인덱싱 (indexing) 과 슬라이싱 (slicing) 이 가능
- 형식
    
> 리스트명 = [원소 1, 원소 2, 원소 3, ...]
    
- 대괄호 [] 안에 콤마로 구분하여 원소들을 표시
- 리스트의 각 원소는 변수이며 그 값은 변경가능

- 리스트 example

    ```
    userAges = [21, 22, 23, 24,25]
    a = [1, 2.2, 'python']
    b = [ [" mouse", [8, 4, 6]]# 문자열과 리스트가 원소
    c = list ()# 빈 리스트 c 를 생성
    d = [] # 마찬가지로 빈 리스트 d 를 생성
    ```

### 리스트 indexing
- 인덱스 값을 통해 리스트의 각 원소가 가리키고 있는 값에 접근할 수 있음
- indexing 범위 문자열과 동일하게 적용
    - n : 리스트의 크기 , 내장함수 len () 을 통해 구할 수 있음
    - Positive indexing : 0 ~ n 1
    - Negative indexing : n ~ 1
- 대괄호 [ ] 안에 첨자 (Index) 번호 입력하여 특정 요소의 값을 참조

### 리스트 slicing
- 문자열과 동일하게 적용
- 형식 (L 을 n 개의 원소를 갖는 list 라고 가정)

    > L[ b : e : s ] # b = begin, e = end, s = step 을 의미

- Slicing Rule (b, e  0 인 경우로 설명)
    - s > 0 ( b < e 이어야 함 . 아니면 빈 리스트 생성 )
        - index 를 b 부터 e  1 까지 s 씩 증가하며 리스트를 참조    
    - s < 0 ( b > e 이어야 한다 . 아니면 빈 리스트 생성)  
        - index 를 b 부터 e 까지 s씩 감소하며 리스트를 참조

### slicing 을 이용한 리스트 원소 제거
- 리스트 a = [0, 1, 2, 3, 4]
- 원소의 제거

    ```
    a[1:3] = [] # a[1], a[2] 제거
    print(a) # [0,3,4]
    a[0] = 1 # a[0] 값을 1 로 변경 (slicing 아님)
    print(a) # [1,3,4]
    a[1:2] = [] # a[1] 제거
    print(a) # [1,4]
    a[1] = [] # a[1] 에 empty list [ ] 를 assign
    print(a) # [ 1, [] ]
    del a[:2] # a[0],a[1] 제거
    print(a) # []
    # del a[:] 는 리스트의 모든 원소를 삭제하고 빈 리스트로 만듦
    ```

### slicing 을 이용한 리스트 원소 교체
- 리스트 a = [0, 1, 2, 3, 4]
- 원소의 교체

    ```
    a[1::2] = [9,9] # 홀수 인덱스 원소 값을 모두 9 로 교체
    # (item 의 수가 같아야 함 ) [0,9,2,9,4]
    a[1:3] = [1] # a[ 과 a[2] 를 1 로 교체
    print(a) # [0, 1, 9,4]
    a[2:3] = [5, 6] # a[ 를 5, 6 으로 교체
    print(a) # [0,1, 5, 6,4]
    a[3:] = [8,9,10] # a[3] 부터 순서대로 원소를 8,9,10 로 교체
    print(a) # [0,1,5,8,9,10]
    ```

- 리스트에서 하나의 원소를 수정 : 인덱스 사용
- 리스트에서 연속된 원소들 수정 슬라이싱 사용

### slicing 을 이용한 리스트 원소 추가
- 원소의 추가

    ```
    a[1:1] = [' a','b ']# index 1 에 a','b 추가 끼워 넣기
    print(a)# [0,'a','b',1,2,3,4]
    a[1:1] = [ ['A','B'] ]# index 1 에 리스트 ['A','B'] 추가
    print(a) # [0,['A','B'],'a','b',1,2,3,4]
    a[5:5]= [5] # a[5] 에 추가
    # [0, ['A','B'], 'a', 'b', 1, 5, 2, 3, 4]
    a[ len (a)]= [ 10]# 리스트 끝에 새 원소 10 을 추가
    # [0, ['A','B'], 'a', 'b', 1, 5, 2, 3,4,10]
    ```

### 리스트 복사
- 리스트 참조 복사하기 (‘=’ 이용 )
- 참조를 복사 . 즉 , 동일한 객체를 다른 이름으로 참조하게 됨

### 리스트 복사 (slicing)
    A = ['ab', 'cd', ' ef]
    B = A[:] # B = A.copy ()
    print(id(A), id(B)) # id 가 다름 다른 객체
    B[2] = 10
    print(A, B)

### 리스트 연산자
- Concatenation operator + ( 리스트의 연결 연산)
    : 리스트들을 연결하여 새로운 리스트로 만듬
- Repetition Operator * ( 리스트의 반복 연산 )
    : list * n 은 list 의 item 들을 n 번 반복하여 새로운 list 를 만듬
- Membership operator in, not in ( 문자열에서와 동일)

### 리스트 메소드

method |Description (x: 리스트 , a: 임의의 객체)
--------| ----------------|
x.append(a} |  데이터 a 를 리스트 x 의 끝에 추가
x.extend (L)| 리스트 L 의 모든 원소를 리스트 x 의 마지막에 추가
x.insert (i , a) |a 를 리스트 x 의 index i 에 추가
x.remove (a}|리스트 x 에서 원소 값이 데이터 a 인 첫 원소 제거(반환 값 없음)
x.pop( ) | x 의 마지막 원소 제거 및 반환
x.pop( i)| x[i] 를 x 에서 제거하고 그 값을 반환
x.clear() |리스트 x 의 모든 원소를 삭제 . 빈 리스트가 됨
x.index(a)| 리스트 x 에서 원소 값이 a 인 첫 번째 원소의 index 를 반환
x.count(a)| 리스트 x 에서 a 값과 같은 원소의 개수를 반환
x.sort ()|x 의 원소들을 오름차순으로 정렬, 내림차순으로 정렬하려면 x.sort (reverse= True) 사용
x.reverse ()| x 의 원소들을 역으로 재 배치 (정렬과 다름)
x.copy ()| a shallow copy of the list (y = x[:] 와 동일)


### 리스트 관련 내장 함수 
- 문자열 , 튜플 , 집합 , 사전 등도 사용 가능 .

function |Description( 인수 x : 리스트)
--------| ----------------|
all(x) | x 의 모든 원소가 True( i.e. != 0) 이거나 , 또는 x 가 빈 리스트이면 True 반환
any(x) | x 에 True 인 (i.e. != 0 인 ) 원소가 한 개라도 있으면 True, 또는 x 가 빈리스트이면 False 반환
enumerate(x) | x 의 모든 원소에 대해 튜플 (index, 원소 값) 을 얻을 수 있는 enumerate object 를 반환 . index = 0, 1, 2,
len (x) | x 의 원소 개수를 반환
list(y)| Iterable 한 y 를 리스트로 변환하여 반환
max(x)| x 의 원소 중 최대 값 반환 비교 불가이면 TypeError
min(x)| x 의 원소 중 최소 값 반환 비교 불가이면 TypeError
sorted(x) |x 의 원소를 정렬한 리스트 반환 x 는 불변이고 오름차순 또는 내림차순으로 정렬 sorted(x, reverse=True)
sum(x) | x 의 원소 합을 반환 더할 수 없으면 TypeError
