---
title: "[Python] Chapter1 파이썬 개요"
categories:   
  - Python
last_modified_at: 2020-08-11T11:00:00+09:00
toc: true
toc_sticky: true
toc_label: "목차"
tags:
  - 파이썬
  - 프로그래밍
sidebar:
  nav: posts

---


## Chapter1 파이썬 개요
### 컴퓨터 프로그램과 언어
- 컴퓨터 프로그램이란
    - 컴퓨터에서 실행될 때 특정 작업 (specific 을 수행하는 일련의 명령어들의 모음
    - 컴퓨터 소프트웨어와 같은 뜻    
    
- 프로그래밍 언어란
    - 프로그래밍 언어는 컴퓨터 시스템을 구동시키는 소프트웨어를 만들기 위한 언어
- 기계어
    - 컴퓨터가 알아듣는 유일한 언어
    - machine code 라고 부른다
    - 기계어는 0 과 1 로 구성 (binary
    - 초기의 컴퓨터에서는 기계어를 사용하여 프로그래밍을 하였다
    
- High Level 프로그래밍 언어
    - 인간의 언어와 비슷한 프로그래밍 언어
    - 프로그램을 작성하면 통역을 담당하는 SW(Compiler/Interpreter) 가 기계어로 번역

- Interpreter
    - 작성한 프로그램의 명령어들을 한번에 하나씩 해석하여 실행하는 프로그램 .
    - Python 프로그램은 interpreter 방식으로 실행된다

- Compiler
    - 작성한 프로그램 전체를 스캔하여 일괄적으로 한번에 실행프로그램으로 바꾸는 프로그램
    - C, C++ 프로그램 등은 compiler 을 사용하여 실행파일로 변환한 후 이를 실행한다

### 파이썬 프로그래밍 언어
- 1990 년 , 귀도 반 로썸 Guido van Rossum) 이 개발한 대화형 프로그래밍 언어
- 다양한 OS 환경에서 사용 가능 윈도우 , 매킨토시 , 유닉스 , 리눅스
- 파이썬 언어 버전
- 버전 2 : 2020 년까지 지원 예정
- 버전 3 : 현재 버전
- 버전 2 와 버전 3 의 문법이 다름

- 파이썬의 장점
    - 쉬운 문법 , 직관적인 코드 , 간단한 프로그램
    - 풍부한 라이브러리
    - 짧은 개발기간
    - 초보자에게 적합한 프로그래밍 언어
    
- 파이썬 단점
    - 느린 속도 , 인터프리터 언어의 특징
    - 모바일 프로그램 , 하드웨어 제어 등에 취약

### 파이썬 IDLE
- Integrated Development and Learning Environment 의 약어
- Python 프로그램을 배우거나 개발하기 위한 통합된 환경을 제공하는 시스템 프
로그램
- 주요 기능
    - Python shell
    프로그램을 대화형 ( 으로 입력 , 해석 , 수행할 수 있는 colored 사용자 인터페이스
    - Python 프로그램 편집기
    Python 프로그램 파일 ( script 을 편집 , 이를 수행할 수 있는 기능 제공
    - Debugger
    Python 프로그램 오류를 수행 중 탐지할 수 있는 기능
    
- Python Shell 실행
    - 바탕화면에서 IDLE icon 을 더블 클릭하면 Python Shell 창이 활성화됨
    - Python Shell 에서는 Python statement 를 interactive 하게 입력하고 실행할 수 있음
    ( statement 는 Python 명령어를 의미)
    - Python 언어를 배우거나 테스트 할 때 유용
    
- Interactive Mode 의미
    - Python Shell 창이 활성화된 상태는 아래와 같음
    - Python Shell 의 프롬프트 (>>>) 의 커서 위치에 Python 명령어를 입력하고 enter 키를 누르면
    명령어가 실행되고 실행 결과가 바로 다음 줄에 출력됨 . 이를 interactive mode 라고 함
    
- Python Shell 에 입력
- 아래와 같이 입력


- Python 에서의 주요 산술 연산 (arithmetic operation)

연산자 | 	연산 
------------ | -------------
+	| 덧셈
-	| 뺄셈
*	| 곱셈
/	| 나눗셈 결과는 항상 실수
//	| 몫 구하기
%	| 나머지 구하기

- Python 에서의 주요 관계 연산 (relational

관계연산자	| 연산| 	비고
------------ | -------------| -------------
x == y| 	equality 	 x= y 이면 True
x < y	| less 	 | x< y 이면 True
x > y	| greater 	| x > y 이면 True
x <= y| 	less then or equal 	 | x<= y 이면 True
x >= y| 	greater then or equal 	 | x=> y 이면 True
x != y| 	not equal 	| x!=y 이면 True

- 문자는 한 줄짜리 주석 (comment) 에 사용
- Python interpreter 는 명령어 실행 시 , 주석은 무시 프로그램 설명문으로 간주
- 여러 줄 주석은 큰 따옴표 또는 작은 따옴표 세 개를 사용
- : ＂＂＂로 시작하면 ＂＂＂로 마쳐야 함
Python Shell 에서는 주석을 echo 라고 한다 . n 은 줄바꿈 문자

