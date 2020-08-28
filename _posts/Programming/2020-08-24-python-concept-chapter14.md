---
title: "[Python] Chapter14 파일 입출력 "
categories:   
  - Python
last_modified_at: 2020-08-24T11:00:00+09:00
toc: true
toc_sticky: true
toc_label: "목차"
tags:
  - 파일 입출력
  - 파일 열기 
sidebar:
  nav: posts
comment: true

---

## Chapter14 파일 입출력
### 파일 입출력
-입력 데이터의 양이 많으면 손으로 직접 입력하기 어렵다 (오타가 가능성이 많고 , 이 경우 다시 실행해야 한다)
- 실험 데이터를 처리해야 할 경우 , 이 데이터는 보통 파일로 전달되며 그 양이 매우 많다
- 출력 데이터를 파일로 보관할 필요가 있을 때가 있다
- 본 강의에서는 문자열로 구성된 파일 만을 다룬다
- 파일 입출력은 다음과 같은 세 단계를 통하여 이루어짐
    1. 파일 열기 (File Open)
    2. 파일에서 읽거나 또는 파일에 쓰기
    3. 파일 닫기 (File Close)
    
### 파일 열기 
- 형식

    > fp_r = open ("in. txt", ' r‘) # read mode
    > fp_w = open ("out. txt", ' w‘) # write mode

    - fp_r , fp_w : 파일 object 를 나타내는 변수
    - in.txt , out.txt : 파일의 이름
    - File Mode : 파일을 어떤 용도로 사용할지 결정
        - 'r' : 읽기 전용 .
        - 'w' : 쓰기 전용 . 파일이 없으면 빈 파일을 새로 만들고 , 기존 있던 파일이면 내용을 모두 지우고 파일을 open.
        - 'a' : Append 의 약자이며 , 기존 파일에 덧붙여서 이어서 쓰기 작업을 함
        - 그 외에 'r+', 'b' 등이 있으나 다루지 않는다

### 입출력 파일 위치
- script 파일이 저장되어 있는 폴더에 저장되어 있는 파일을 읽거나 쓰는 경우 : 파일 이름만 명시
    
> fp_r = open ("in. txt", ' r')# read mode
    
- script 파일과 다른 폴더에 저장되어 있는 파일을 읽거나 쓰는 경우 : 전체 경로를 파일 이름과 함께 명시  
    
> fp_r = open (" work in . txt", 'r')
    
- 위 예는 C: Work 라는 폴더에서 in.txt 라는 파일을 읽겠다는 의미이다

### 파일 읽기
- open() 함수에서 읽기 모드로 반환받은 파일객체를 가리키는 변수를
fp_r 라고 가정
- fp_r.read ( ) : 파일 전체를 하나의 문자열로 읽어 들임
- fp_r.readline ( ) : 한 줄을 문자열 형식으로 읽어 이를 반환
- fp _r.readlines ( ) : 파일을 줄 단위로 읽어 각 줄을 문자열 형식으로 저장 . 이들 전체 문자열을 원소로 하는 리스트를 반환
- 파일 전체를 한 줄씩 읽어 처리하는 방법 : for loop 를 사용하면 편리

```python
for aLine in fp_r :# 변수 aLine 은 fp_r 에서 한 줄씩 읽어 들인 문자열
       statements # 읽어들인 줄에 처리할 명령어들
```

### 파일 쓰기
- open() 함수에서 쓰기 모드로 반환받은 파일객체를 가리키는 변수를 fp_w 라고 가정
- fp_w.write (string)
    - string 문자열 하나를 파일에 씀
    - 줄바꿈 문자가 자동으로 삽입되지 않음
    - 줄바꿈이 필요한 경우 , string 의 마지막에 줄바꿈 기호를 추가
- print(*objects, file = fp_w)
    - 화면 대신 파일 fp_w 에 쓴다
    - print() 함수는 줄바꿈이 자동 .
    - 줄바꿈을 하지 않으려면 , end 인수값 변경
    > print(*objects, file = fp_w , end ="")

### 파일 닫기 
 파일을 열었다면 반드시 파일을 닫아야 함

```python
fp_r = open ("in. txt", ' r‘)# read mode
fp_w = open ("out. txt", ' w‘)# write mode

fp_r.close()
fp_w.close()
```

- 파일이 열려있는 상태에서는 파일을 지우거나 이름을 바꿀 수 없음
- Python shell 을 종료하거나 , restart 하거나 또는 close method 를 호출하여야 파일이 닫혀 파일 지우기 또는 이름 바꾸기 등을 수행할 수 있음
- 따라서 , 파일 작업을 마치면 반드시 파일을 닫도록 함

- 한 줄씩 읽어 화면에 출력하기

```python
fp = open("in_data. txt", 'r')
for s in fp :# 한 줄씩 읽어
    print (s, end = """")# 화면에 출력
fp.close()

```