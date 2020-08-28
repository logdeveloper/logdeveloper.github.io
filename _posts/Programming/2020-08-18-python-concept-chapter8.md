---
title: "[Python] Chapter8 튜플 집합 사전 "
categories:   
  - Python
last_modified_at: 2020-08-18T11:00:00+09:00
toc: true
toc_sticky: true
toc_label: "목차"
tags:
  - 튜플
  - 집합
  - 사전
  - tuple
  - set
  - dict
sidebar:
  nav: posts

---

## Chapter8 튜플 집합 사전
### 튜플 (tuple)
- sequence 는 원소 사이에 순서가 있는 자료 구조를 말하며 리스트 뿐만 아니라 튜플도 해당
- 파이썬에서 시퀀스에 속하는 자료 구조에는 string, list, tuple, range 등이 있으며 동일한 연산을 지원함    
    - 인덱싱 (indexing), 슬라이싱 (slicing), +, *, in, not in 연산자    
- 튜플은 리스트와 유사 하지만 , 튜플의 원소는 추가 삭제 수정이 불가능 함    
    - 원소를 변경하면 에러 발생
- 값이 변하지 않는 iterable 한 데이터 저장에 효율적인 자료구조
    - 튜플을 사용하면 실수로 추가 , 삭제 , 변경되는 것을 막을 수 있음
    - 프로그램 수행 동안 변경하지 않는 데이터는 튜플로 저장하는 것이 효율적
- 리스트처럼 여러 데이터형을 저장할 수 있는 자료형
- 형식
  
    > 튜플명 = (원소1, 원소2, 원소3....)
    
    - ( ) 소괄호를 사용하여 표시 . 괄호는 생략 가능
    - 콤마를 사용하면 괄호가 없어도 튜플로 인식
    - 원소로 정수 , 문자열 , 튜플 , 리스트 등 가능

- 튜플의 원소는 추가 삭제 수정할 수 없음 . immutable 자료형
- 리스트에서의 indexing, slicing, operator, 내장 함수 등을 사용할 수 있음
    - slicing 으로 원소를 수정할 수는 없음
    - del 명령어로 튜플 자체 삭제만 가능 원소 삭제에는 사용 못함

- 빈 튜플 생성
    > t = ()
    > t = tuple()
- 튜플 생성
    - 튜플은 콤마를 사용하면 괄호가 없어도 튜플로 인식
    - 원소가 하나인 튜플을 만들 때도 콤마가 필요
    - 여러 가지 데이터를 튜플로 묶는 것을 튜플 packing
    - 반대로 , 튜플의 각 원소를 여러 개의 변수에 할당하는 것을 튜플 unpacking
    튜플의 원소의 수와 변수의 수가 일치해야 함
    : 튜플의 값들을 여러 변수에 동시에 할당하는 것이 가능

- 문자열 , 리스트와 동일하게 인덱싱 , 슬라이싱 사용
    : 다만 , 데이터 변경은 불가능
- + 연결 연산 , * 반복연산 , in 연산 , len () 함수 사용가능
- 튜플 객체의 메소드

Method | Description (T : 튜플 , x 임의의 object)
------- |  ---------------------------------
T.index (x)|  튜플에서 데이터 x 의 인덱스를 반환
T.count (x) |  튜플에서 데이터 x 의 개수를 반환

- 튜플의 원소가 리스트인 경우는 예외적으로 원소 값 수정이 가능

### 집합 (set)

- 데이터들을 순서 없이 모아둔 자료형
- 형식
  
    > 집합명 = {원소 1, 원소 2, 원소 3, ...}
    
    - 중괄호 {} 를 사용하여 표시 , 공집합도 가능
    - 값을 바꿀 수 없는 객체만 원소로 올 수 있음
    - 리스트처럼 내용 변경이 가능한 object 는 원소로 올 수 없음
- 집합 자료형의 특징
    - 중복 불가능
        - 집합에는 동일한 원소가 두 개 이상 있을 수 없음
        - 자료의 중복을 제거하기 위한 필터 역할로 활용될 수 있음
    - 순서가 없음 (unordered)
    
- 빈 집합 생성 공집합

    >s = set()
    >
    ># s = {} 명령어는 빈 사전 (dictionary) 생성

- 집합은 순서가 없기 (unordered) 때문에 출력하면 원소들이 임의의 순서로 출력되며 , 인덱싱이 지원되지 않음    
    - 집합의 원소를 인덱싱으로 참조하려면 리스트나 튜플로 변환한 후 인덱싱 사용
    
- 집합은 원소의 추가 / 삭제 가능
- membership 연산자 ( in, not in), loop 를 통한 원소 검색 가능
- set() 함수 이용 집합 생성
    
- set() 함수의 인수로 리스트 또는 문자열 , 튜플 ) 데이터를 입력하면 해당 원소들을 자신의 원소로하는 집합을 만듬
    
- 집합 객체의 메소드    

function |Description(A, B : 집합)
--------| ----------------|
A.add (x) | 데이터 x 를 A 의 원소로 추가
A.clear () | A 의 모든 원소를 제거 A 를 공집합으로 만듬
B = A.copy() | A 를 B 로 복사 (shallow copy)
A.discard (x) | 집합 A 에서 원소 x 를 제거 . 없는 원소를 삭제하려고 할 때에도 에러 발생하지 않음 (x A 이면 무시
A.remove (x) |집합 A 에서 원소 x 를 제거 . 없는 원소를 삭제하려고 하면 KeyError 가 발생 (x A 이면 KeyError)
A.pop () |집합 A 에서 임의의 원소를 하나 지우고 그 값을 반환 (A가 공집합이면 KeyError ). 순서가 없기 때문에 임의의 원소 가져옴
A.union(B) | A B 를 반환 (A | B 와 동일)
A.intersection(B)| A B 를 반환 (A & B 와 동일)
A.difference(B)| B 에는 없고 A 에만 있는 원소의 집합 반환 (A - B 와 동일)


### 사전 (dictionary)

- 사전은 키 (key) 와 값 (value) 의 쌍을 저장하는 순서가 없는 테이터 형
- 사전은 중괄호 {} 로 표시하며 , 원소들은 콤마로 분리
  
        > 사전명 = {키:값1, 키2:갑2}
    
- key 에는 정수 실수 문자열 튜플 같은 immutable 자료형만 허용되며 ,mutable 한 자료형 리스트 , 집합 , 사전 은 올 수 없음
- value 에는 어떤 객체도 가능
- key 값은 고유한 값만 올 수 있으며 , 중복되는 key 값을 설정하면 하나를 제외한 나머지 것들이 모두 무시됨

- 빈 사전 생성  
    > d = dict
    > d = {} # 빈 사전 (dictionary) 생성
    
- 사전은 key 값으로 이에 대응되는 value 값을 구하는 방식
- 인덱싱에서 [ ] 안에 인덱스 번호가 아닌 key 값을 주어 해당 value 값을 참조
- in, not in 연산자 , len () 함수는 사용 가능
- +, * 연산자는 사용할 수 없음
- 사전에 원소 (쌍 ) 추가하기

    > d[key] = value # d: 사전형 변수 key : value 쌍이 원소로 사전 d 에 추가

- 사전에서 원소 삭제하기

    > del d[key] # d: 사전형 변수 key 에 해당하는 {key: value} 쌍이 사전에서 삭제

사전의 Method | Description ( D : 사전)
------- |  ---------------------------------
D.clear ()| D 의 모든 원소를 삭제 . D = { 가 됨
D.items ()|key 와 value 의 쌍을 튜플로 묶은 값을 dict_items 객체로 반환 . 튜플 (key,value) 를 원소로 하는 리스트를 만들거나 (key,value) 가 필요한 반복문에서 사용
D.keys()|딕셔너리 D 의 Key 만을 모아서 dict_keys 객체로 반환 . 필요한 반복문에서 사용
D.values ()| value 로 구성된 dict_values 객체를 반환
D.get (key[,d])|key 에 대한 value 값 반환 . 존재하지 않는 key 이면 d 반환 , d 가 주어지지 않았으면 None 반환
D.pop (key[,d])|key 에 대한 value 반환하고 해당 원소를 삭제 .존재하지 않는 key 이면 d 반환 , d 가 주어지지 않았으면 KeyError
D.copy ()|D 를 복사하여 반환 (shallow copy).
D.update (other) | 존재하는 key 이면 value 를 갱신 없으면 쌍을 추가, 예 D.update ([(‘a’,2),(‘b’,3)]) #D 에 없으면 (‘a’, 와 (‘b’, 를 추가 .

- 반환값 dict_keys 객체는 list( a.keys 와 같은 명령어로 리스트로 변환 가능 . 리스트로 변환하지 않더라도 기본적인 반복문 예 : for 문 에 적용할 수 있음 dict_values , dict_items 객체도 동일


- 사전에서 key 로 value 얻기 d.get () 메소드 , d 는 사전 변수라고 가정
    - d.get (x) : 사전 d 에서 key 값 x 에 대응되는 value 반환
    - d[x] 와 동일한 결과값을 반환
    - x 가 존재하지 않는 key 값일 경우 , d.get ( 는 None 반환 . d[ 는 key 값 오류 발생
- 사전에서 항목 삭제하기
    - d.pop (x): 사전 d 에서 key 값 x 에 대응되는 value 를 반환하고 해당 원소 쌍 삭제

- 사전에서 key 값들 가져오기 ( d 는 사전 변수라고 가정
    - d.keys () : 사전 d 의 모든 key 값들을 dict_keys 객체로 반환
    - dict_keys 객체로 받은 값을 리스트와 같은 자료형으로 변환하여 사용 리스트의 메소드를 적용하는 것이 코딩에 유용하기 때문 )
- 사전에서 key 값 , value 값들 가져오기
    - d.items () : 사전 d 에서 key 와 value 의 쌍을 튜플로 묶은 값들을 dict_items 객체로 반환
- 사전에서 value 값들 가져오기 ( d 는 사전 변수라고 가정 )
    - d.values () : 사전 d 에서 value 값들을 dict_values 객체로 반환
- 사전에서 해당 key 가 존재하는지 검사
    - in 연산자 : membership 검사는 key 값만 가능
- 사전에서 모든 원소들 제거
    - d.clear () : 원소들만 제거하고 빈 사전만 남음

```python
    D = {'a' : 1, 'b' : 2, 'c' : 3, 'd' : 4}
    print( len ( D))# 4 (D 의 원소 수 계산)
    keyList = sorted( D)# D 의 key 값을 기준으로 정렬한 리스트
    print( keyList ))# ['a', 'b', 'c', 'd']
    print(D['b']) # 2 (key 가 'b' 인 원소의 value 를 반환)
    print( D.get ('b'))# 2 (D['b'])와 동일
    print( D.get ('e'))# None 사전에 없어 None 반환
    print( D.get ('e', 0))# 0 사전에 없어 0 반환 다른 값 가능
    #print(D['e'])# KeyError 사전에 없어 오류 --> 주석처리
    print(D.pop('c')) # 3 ('c') 의 value 반환 , ('c':3) 제거
    print(D) # {'a': 1, 'b': 2, 'd':4}
    print(D.pop('c', 1)) # 1 ('c') 가 없다면 1 반환
    #print(D.pop('c'))# KeyError 사전에 없어 오류 주석처리

```

