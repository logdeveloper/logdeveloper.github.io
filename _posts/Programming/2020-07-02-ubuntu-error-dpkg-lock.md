---
title: "[Linux] Ubuntu 18.04 dpkg error"
categories: 
  - Linux
last_modified_at: 2020-07-02T11:00:00+09:00
toc: true
toc_sticky: true
toc_label: "페이지 주요 목차"
tags:
  - Ubuntu 18.04
  - Error  
  - Ubunbtu Error
  - dpkg
sidebar:
  nav: posts
---

우분투에 자바를 설치하는 과정에서 아래와 같은 에러가 발생하였다. 

![ubuntu-1](/assets/images/2020-07-02-ubuntu-error-dpkg-lock/ubuntu-1.png)



그래서 apt가 문제 인가 싶어서 update도 하고, process도 죽여보고 다 해봤지만 해결이 안됬다. 

- sudo update

  ![ubuntu-2](/assets/images/2020-07-02-ubuntu-error-dpkg-lock/ubuntu-2.png)

- sudo killall apt-get

  ![ubuntu-3](/assets/images/2020-07-02-ubuntu-error-dpkg-lock/ubuntu-3.png)



결국 해결한 방법은 관련된 파일을 삭제하는 것이다. 



- 삭제 할 목록

  /var/lib/apt/lists/lock 

  /var/cache/apt/archives/lock 

  /var/lib/dpkg/lock*



rm 명령어로 삭제한다.

```bash
log@ubuntu:/usr/local/java$ sudo rm /var/lib/apt/lists/lock 
log@ubuntu:/usr/local/java$ sudo rm /var/cache/apt/archives/lock 
log@ubuntu:/usr/local/java$ sudo rm /var/lib/dpkg/lock*
```





관련 파일 삭제 후 자바를 다시 설치하면 정상적으로 설치된다.

![ubuntu-4](/assets/images/2020-07-02-ubuntu-error-dpkg-lock/ubuntu-4.png)