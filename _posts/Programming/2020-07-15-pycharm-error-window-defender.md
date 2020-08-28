---
title: "[Pycharm] Window Defender Warning"
categories:   
  - Etc
last_modified_at: 2020-07-12T11:00:00+09:00
toc: true
tags:
  - Pycharm
  - Window Defender
sidebar:
  nav: posts

---

## 현상

pycharm을 사용 중에 아래와 같은 Window Defender 관련 로그를 발견하였다. 

그냥 써도 문제는 없지만,, 성능에 영향을 줄 수 있다고 하니 해결하기위해 아래 관련된 폴더를 설정 해주었다. 


```
Windows Defender might be impacting your build and IDE performance. 
PyCharm checked the following directories: 
	C:\Users\*\PycharmProjects\algo2
   	C:\Users\*\AppData\Local\JetBrains\PyCharmCE2020.1 
   	C:\Users\*\.gradle
```





## 해결 방법

윈도우 검색창에서 windows 보안 설정 클릭하여 관련 폴더를 추가해준다. 



- windows 보안 

  ![image-20200715220346477](/assets/images/2020-07-15-pycharm-error-window-defender/image-20200715220346477.png)



- 바이러스 및 위협 방지 

  ![image-20200715220416591](/assets/images/2020-07-15-pycharm-error-window-defender/image-20200715220416591.png)



- 설정 관리 > 제외 > 제외 추가 또는 제거 

  ![image-20200715220442282](/assets/images/2020-07-15-pycharm-error-window-defender/image-20200715220442282.png)



- 제외 사항 추가 > 해당 폴더를 추가

  ![image-20200715220527538](/assets/images/2020-07-15-pycharm-error-window-defender/image-20200715220527538.png)