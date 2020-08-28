---
title: "[Python][MariaDB] python mariadb 연동"
categories:
  - Python
last_modified_at: 2020-08-11T11:00:00+09:00
toc: true
toc_sticky: true
toc_label: "목차"
tags:
  - python 
  - mariadb 
sidebar:
  nav: posts
---

이전에는 MySQL Python package를 사용하여 MariaDB를 연결하였지만, 2020년 6월에 MairaDB에서  Connector/Python 첫번째 버전을 만들었다. ([예전 자료 바로가기](<https://mariadb.com/resources/blog/how-to-connect-python-programs-to-mariadb-2014/>))

MariaDB Server, MariaDB MaxScale and MariaDB SkySQL를 포함한 MairaDB Platform안에 저장된 데이터를 다룰 수 있다. 아래 예제에서 검색, 업데이트, 삽입을 위해 MairaDB 플랫폼에 연결하는 방법에 대해서 알아보자.

## 1. MariaDB Server 연결


```python
# Module Imports
import mariadb
import sys
```


```python
# Connect to MariaDB Platform
try:
    conn = mariadb.connect(
        user="log",
        password="log1234",
        host="localhost",
        port=3306,
        database="log_db"
    )
except mariadb.Error as e:
    print(f"Error connecting to MariaDB Platform: {e}")
    sys.exit(1)

# Get Cursor
cur = conn.cursor()
```



## 2. 데이터 가져오기

사전에 MariaDB에 아래와 같이 데이터를 저장해 두었다

![1597215447110](/assets/images/2020-08-11-python-mariadb-example/1597215447110.png)

### 1) 모든 데이터 가져오기


```python
# selectall = "SELECT * from employee" 
select_all_query = "SELECT firstname, lastname from employee" 
cur.execute( select_all_query )

# query 결과를 list 형으로 가져옴.
resultset = cur.fetchall()

for firstname, lastname in resultset: 
    print(f"First name: {firstname}, Last name: {lastname}")
```

    First name: kim, Last name: log
    First name: park, Last name: happy

### 2) 특정 조건의 데이터 가져오기


```python
some_name = "kim" 
select_where_query = "SELECT firstname, lastname from employee WHERE firstname=?" 

cur.execute( select_where_query,(some_name,))
resultset = cur.fetchall()

for firstname, lastname in resultset: 
    print(f"First name: {firstname}, Last name: {lastname}")
```

    First name: kim, Last name: log



## 3. 데이터 추가하기


```python
firstname = "joy"
lastname = "lee"

insert_query = "INSERT INTO employee (firstname,lastname) VALUES (?, ?)"

try: 
    cur.execute( insert_query, (firstname, lastname))
except mariadb.Error as e: 
    print(f"Error: {e}")
```

실행 결과는 아래와 같다.

![1597215547482](/assets/images/2020-08-11-python-mariadb-example/1597215547482.png)





기본적 MariaDB connector/Python은 자동 커밋으로 설정되어 있다. 

만약 수동으로 `commit`과 `rollback`을 관리하고 싶다면, `conn.autocommit = False` 옵션을 적용하여 비활성화 한다.

auto-commit 비활성화 옵션이 적용되면, 수동으로 `commit`과 `rollback`을 관리할 수 있다. 
> conn.commit()


행을 insert하는 동안 자동 증가 값과 마찬가지로 생성될 때, 마지막으로 삽입된 행의 기본 키를 찾을수 있다. 
> cur.lastrowid

## 4. 예외처리
try-except 문을 통해 mariadb.Error 예외를 반환한다.


```python
try: 
    cur.execute( "Some MariaDB query")
except mariadb.Error as e: 
    print(f"Error: {e}")
```

DB 작업을 마친 후에는 사용하지 않는 연결을 열어 리소스를 낭비하지 않기 위해 연결을 닫아야 한다. 


```python
# 연결 닫기 
conn.close ()
```

## 5. 스크립트 모아보기


```python
# Module 추가
import mariadb
import sys

# MariaDB 연결
try:
    conn = mariadb.connect(
        user="log",
        password="log1234",
        host="localhost",
        port=3306,
        database="log_db"
    )
except mariadb.Error as e:
    print(f"Error connecting to MariaDB Platform: {e}")
    sys.exit(1)

# Cursor 가져오기 
cur = conn.cursor()

## 모든 데이터 조회
# selectall = "SELECT * from employee" 
select_all_query = "SELECT firstname, lastname from employee" 
cur.execute( select_all_query )

# query 결과를 list 형으로 가져옴.
resultset = cur.fetchall()

print('-------- select all data ----------')
for firstname, lastname in resultset: 
    print(f"First name: {firstname}, Last name: {lastname}")

## 특정 조건 데이터 조회

some_name = "kim" 
select_where_query = "SELECT firstname, lastname from employee WHERE firstname=?" 

cur.execute( select_where_query,(some_name,))
resultset = cur.fetchall()

print('-------- select kim data ----------')
for firstname, lastname in resultset: 
    print(f"First name: {firstname}, Last name: {lastname}")

    
# 데이터 추가 
    
lastname = "joy"
firstname= "lee"
insert_query = "INSERT INTO employee (firstname,lastname) VALUES (?, ?)"

try: 
    cur.execute( insert_query, (firstname, lastname))
except mariadb.Error as e: 
    print(f"Error: {e}")
    
# 연결 닫기 
conn.close ()
```

    -------- select all data ----------
    First name: kim, Last name: log
    First name: park, Last name: happy
    -------- select kim data ----------
    First name: kim, Last name: log


> 참고 사이트 
    [MariaDB Blog](https://mariadb.com/ko/resources/blog/how-to-connect-python-programs-to-mariadb/)


