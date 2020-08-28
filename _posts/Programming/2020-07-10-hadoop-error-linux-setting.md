---
title: "[Hadoop] rcmd socket permission denied"
categories:
  - Hadoop

last_modified_at: 2020-07-10T11:00:00+09:00
toc: true
toc_sticky: true
toc_label: "페이지 주요 목차"
tags:
  - Ubuntu 18.04
  - Linux
  - Hadoop  
  - Setting
  - rcmd socket Permission Denied
sidebar:
  nav: posts
---

## 현상 

dfs 실행시 아래와 같이 rcmd socket permission denied 에러가 발생하였고, 정상적으로 실행되지 않았다.

![image-20200713005452519](/assets/images/2020-07-13-hadoop-error-linux-setting/image-20200713005452519.png)




## 해결방법

원인은 pdsh 기본 rcmd가 ssh가 아닌 rsh, ssh 원격 로그인 인증이 동일 하지 않을 때 발생한다. 

이를 해결 하기 위해서 ~/.bashrc 파일에 아래의 환경변수 내용을 추가 한뒤, 적용해준다.

```
export PDSH_RCMD_TYPE=ssh
```


환경 변수 적용 후 정상적으로 실행된 화면이다. 
![image-20200713005457829](/assets/images/2020-07-13-hadoop-error-linux-setting/image-20200713005457829.png)

