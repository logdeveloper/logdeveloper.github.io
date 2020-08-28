---
title: "[Hadoop] hdfs -ls 오류 "
categories: 
  - Hadoop
last_modified_at: 2020-07-05T11:00:00+09:00
toc: true
toc_sticky: true
toc_label: "페이지 주요 목차"
tags:
  - Window
  - Linux
  - Error
  - Hdfs error
  - Hadoop Error
  - No such file or directory
  - hdfs 초기 설정
sidebar:
  nav: posts
---



## 현상

하둡을 실행 한 후, 초기 hdfs 파일을 확인 하려고 할때 발생 하는 에러다.

```bash
log@ubuntu:~$ hdfs fs -ls
ls: `.': No such file or directory
```
![image-20200713005434580](/assets/images/2020-07-05-hadoop-error-window-fs/image-20200713005434580.png)

## 해결 방법

원인은 기본 경로에 대한 파일이 존재 하지 않기 때문이다. 
이를 해결하기 위해선 /user/{user_name}/ 폴더를 생성해주면 된다.

```bash
hdfs dfs -mkdir /user 
hdfs dfs -mkdir /user/{loggedin user} 
hdfs dfs -ls
```


> 참고 사이트 : https://stackoverflow.com/questions/28241251/hadoop-fs-ls-results-in-no-such-file-or-directory


















