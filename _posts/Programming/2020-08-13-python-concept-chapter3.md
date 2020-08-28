---
title: "[Python] Chapter3 연산자 "
categories:   
  - Python
last_modified_at: 2020-08-13T11:00:00+09:00
toc: true
toc_sticky: true
toc_label: "목차"
tags:
  - 연산자
  - 산술 연산자
sidebar:
  nav: posts

---

## Chapter3 연산자
### 산술 연산자
- 수식은 피연산자들과 연산자의 조합
- 피연산자가 모두 정수형이 아닐 경우 , 결과는 항상 실수형

연산자 | 	연산 
------------ | -------------
+	| 덧셈
-	| 뺄셈
*	| 곱셈
/	| 나눗셈 결과는 항상 실수
//	| 몫 구하기
%	| 나머지 구하기
** | 지수승

- += 처럼 대입 연산자와 다른 연산자를 합쳐 놓은 연산자

assngment | 	예 | 설명
------------ | -------------| -------------
+	|x += y	|x = x + y 와 동일
-	|x --= y|	x = x y 와 동일
*	|x *= y	|x = x * y 와 동일
/	|x /= y	|x = x/y 와 동일
//	|x //= y|	x = x // y 와 동일
%	|x %= y	|x = x % y 와 동일
**	|x **= y	|x = x ** y 와 동일

### 내장 함수

함수 | 	설명 
------------ | -------------
abs()  | 절대값 반환
round() | 반올림 계산, 자릿수 지정하지 않으면 정수 반환
divmod(x,y) | x 를 y 로 나눈 몫과 나머지 반환 , ( x//y, x%y ) 쌍을 반환

### math Module
- math 모듈 의 함수를 사용하기 위한 import 문 (3 가지 방법)
    - 함수명으로만 호출
    from math import * # 이 경우 모듈 이름이 불필요
    a = sqrt (2.0) # sqrt () 함수를 함수명으로만 호출
       
    - 모듈명으로만 호출 
    import math # 이 경우 math. 을 붙여야 함
    a = math.sqrt (2.0) # sqrt () 함수 앞에 해당 모듈명을 명시해야 함    
    - math 의 별칭에 해당
    
    import math as m # 이 경우 m. 을 붙여야 함
    a = m.sqrt (2.0) # m 은 math 의 별칭에 해당
    
- math 모듈에는 많은 함수들이 존재
    - trunc () 함수 : 인수로 받은 값의 버림 계산 ( math.trunc(1.5) == 1 )
    - pow( x,y ) 함수 : x y 을 반환 ( math.pow (81, 0.5) == 9.0)

### 연산자 우선 순위

- 위에서부터 아래로 우선순위 부여
연산자 | 	설명 
------------ | -------------
( ) | anything in brackets is done first Highest
** | exponentiation
-x, +x |arithmetic operators
*, /, %, // |arithmetic operators
+, - | arithmetic operators
< , >, <=, >=, !=, == |relational operators
=, +=, -=, *= etc | assignment operators
not |logical operator
and |logical operator
or |logical operator Lowest