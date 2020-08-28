---
title: "[MariaDB] Window 설치 및 환경설정"
categories:
  - Database
last_modified_at: 2020-08-12T11:00:00+09:00
toc: true
toc_sticky: true
toc_label: "목차"
comments : true
tags:
  - MariaDB
  - Window 
  - Database
sidebar:
  nav: posts
---





Maria db는 mysql의 경량 버전이라고 생각하면 된다. 

window version에서 설치하고 환경설정하는 방법에 대해서 알아보자.

## 1. 설치

### 1) 공식 사이트에 접속 및 Download 

> <https://mariadb.org/> 
>
> <https://mariadb.org/download/>

MariaDB Server Version, OS, Architecture, Packaga Type 확인후 다운로드 

![1597200779244](/assets/images/2020-08-12-window-mariadb-install/1597200779244.png)

필자는 바로 설치를 위해 msi 버전을 다운로드 하였다. 



### 2) msi 파일 실행

- 다운 받은 msi 파일을 실행하고, 내용 확인하며 `Next` 클릭

	![1597201137799](/assets/images/2020-08-12-window-mariadb-install/1597201137799.png)

- maria db를 설치할 경로 확인

	![1597201169882](/assets/images/2020-08-12-window-mariadb-install/1597201169882.png)


- root 계정의 비밀번호 설정

	![1597201842673](/assets/images/2020-08-12-window-mariadb-install/1597201842673.png)

-  window service 이름과 네트워크는 기본으로 설정

  ![1597201952926](/assets/images/2020-08-12-window-mariadb-install/1597201952926.png)

- 마지막으로 `Install` 클릭

  ![1597201991390](/assets/images/2020-08-12-window-mariadb-install/1597201991390.png)

- 설치 완료 되면 `Finish` 클릭

  ![1597202037488](/assets/images/2020-08-12-window-mariadb-install/1597202037488.png)



### 3) maria db 설치 확인

- 시작  프로그램에서 maria db client  검색하여 실행

  ![1597202173702](/assets/images/2020-08-12-window-mariadb-install/1597202173702.png)



- client cmd 실행 후 설치할 때 입력한 root 계정 비밀번호로 login 되면 정상적으로 설치 된것을 확인할 수 있다.

  ![1597202712008](/assets/images/2020-08-12-window-mariadb-install/1597202712008.png)