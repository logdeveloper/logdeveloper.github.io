---
title: "[Hadoop] Ubuntu 18.04 + Hadoop 3.1.3 Setting On Linux"
categories: 
  - Hadoop
last_modified_at: 2020-07-13T11:00:00+09:00
toc: true
toc_sticky: true
toc_label: "페이지 주요 목차"
tags:
  - Ubuntu 18.04
  - Linux
  - Hadoop  
  - Setting
sidebar:
  nav: posts
---

학부때 배운 리눅스 지식으로 리눅스 기반 하둡을 설치하려고 하니, 기본적인 리눅스 셋팅에서 많이 해맸던 것 같다.

한단계씩 꾸준히 따라오면 설치 할수 있다. 



[아파치 하둡 공식 문서](https://hadoop.apache.org/docs/r3.0.0/hadoop-project-dist/hadoop-common/SingleCluster.html)에서 가이드 해주는 내용과 구글링을 참고하여 진행하였다. 





# 1. 사전 작업

## 1) SSH

- apt-get update 실행

  ```bash
    $ sudo apt-get update
  ```

  

  ![image-20200712230128956](/assets/images/2020-07-06-ubuntu18-hadoop-3/image-20200712230128956.png)



- SSH, pdsh 다운로드

  ```bash
    $ sudo apt-get install ssh
    $ sudo apt-get install pdsh
  ```

  

  ![image-20200712230152679](/assets/images/2020-07-06-ubuntu18-hadoop-3/image-20200712230152679.png)

- ssh 설정

  ![image-20200712233014177](/assets/images/2020-07-06-ubuntu18-hadoop-3/image-20200712233014177.png)

  ![image-20200712233018697](/assets/images/2020-07-06-ubuntu18-hadoop-3/image-20200712233018697.png)

  ![image-20200712233021923](/assets/images/2020-07-06-ubuntu18-hadoop-3/image-20200712233021923.png)



- pdsh 환경설정

  bashrc 파일 열기

  ```
  log@ubuntu:~/hadoop/hadoop-3.1.3$ sudo nano ~/.bashrc 
  
  ```

  

  아래 환경변수 추가

  ```
  export PDSH_RCMD_TYPE=ssh
  ```

  ![image-20200713000854619](/assets/images/2020-07-06-ubuntu18-hadoop-3/image-20200713000854619.png)

- 파일 적용

  ```bash
  log@ubuntu:~/hadoop/hadoop-3.1.3$ source ~/.bashrc 
  ```

  





## 2) Java

### 자바 다운로드 
- apt-get update
	```bash
	$ sudo apt-get update	
	```

- apt-get install java

  ![image-20200712231604276](/assets/images/2020-07-06-ubuntu18-hadoop-3/image-20200712231604276.png)

- java verison 확인

  ![image-20200712232400321](/assets/images/2020-07-06-ubuntu18-hadoop-3/image-20200712232400321.png)

### 자바 환경설정

/etc/environment 에서 자바 환경 변수를 설정해준다.





설정 후 적용해준다.

```
source /etc/enviroment
```






# 2. 하둡 설치

## 1) 다운로드
- wget을 이용하여 hadoop mirror 홈페이지의 사이트 주소를 통해 하둡을 다운 받는다.

  ```
  wget http://apache.mirror.cdnetworks.com/hadoop/common/
  ```

  

  ![image-20200712230902965](/assets/images/2020-07-06-ubuntu18-hadoop-3/image-20200712230902965.png)



- 하둡 폴더 생성

  ![image-20200712231158156](/assets/images/2020-07-06-ubuntu18-hadoop-3/image-20200712231158156.png)



- 다운 받은 폴더를 하둡 폴더 경로에 압축 해제 한다.

  ![image-20200712231521764](/assets/images/2020-07-06-ubuntu18-hadoop-3/image-20200712231521764.png)



## 2) 설정

### 하둡 외부 환경설정
어느 경로에 있든 하둡을 실행하기 위해 하둡 환경설정을 한다.

```
$ sudo nano ~/.bashrc 
```



환경 설정 변수 추가

```

export JAVA_HOME=/usr/lib/jvm/java-8-openjdk-amd64

export HADOOP_HOME=/home/log/hadoop/hadoop-3.1.3
export PATH=$PATH:$HADOOP_HOME/bin
export PATH=$PATH:$HADOOP_HOME/sbin 
export HADOOP_MAPRED_HOME=${HADOOP_HOME}
export HADOOP_COMMON_HOME=${HADOOP_HOME}
export HADOOP_HDFS_HOME=${HADOOP_HOME}
export YARN_HOME=${HADOOP_HOME}

```



![image-20200713010933501](/assets/images/2020-07-06-ubuntu18-hadoop-3/image-20200713010933501.png)



- 변경 내용 적용 

	```
$ source ~/.bashrc
	```



### 하둡 내부 환경 설정

#### datanode, namenode 폴더 생성 및 권한 주기 

#### hadoop-env.sh 

- 자바 설치 경로 확인

  ![image-20200712235201964](/assets/images/2020-07-06-ubuntu18-hadoop-3/image-20200712235201964.png)

- nano 편집기로 파일 열기 

  ```bash
  log@ubuntu:~/hadoop/hadoop-3.1.3$ sudo nano etc/hadoop/hadoop-env.sh
  ```

  

- etc/hadoop/hadoop-env.sh 에 자바 경로 추가 

  ![image-20200712235549373](/assets/images/2020-07-06-ubuntu18-hadoop-3/image-20200712235549373.png)



#### core-site.yml

- nano 편집기로 파일 열기 

  ```
  log@ubuntu:~/hadoop/hadoop-3.1.3$ sudo nano etc/hadoop/core-site.xml 
  ```

  

- property 내용 추가 

	```xml
<configuration>
    <property>
        <name>fs.defaultFS</name>
        <value>hdfs://localhost:9000</value>
    </property>
</configuration>
	```
	
	![image-20200713000038535](/assets/images/2020-07-06-ubuntu18-hadoop-3/image-20200713000038535.png)

#### hdfs-site.yml

- nano 편집기로 파일 열기 

  ```bash
  log@ubuntu:~/hadoop/hadoop-3.1.3$ sudo nano etc/hadoop/hdfs-site.xml 
  ```

  

- 아래 내용 추가 

  ```xml
  <configuration>
      <property>
          <name>dfs.replication</name>
          <value>1</value>
      </property>
  </configuration>
  ```

  ![image-20200713000153855](/assets/images/2020-07-06-ubuntu18-hadoop-3/image-20200713000153855.png)

  

#### yarn-site.yml



# 3. 하둡 실행


## 1) 하둡 실행 명령어

### format namenode

```
log@ubuntu:~/hadoop/hadoop-3.1.3$ bin/hdfs namenode -format
```

![image-20200713000425567](/assets/images/2020-07-06-ubuntu18-hadoop-3/image-20200713000425567.png)

### run hadoop 

- dfs 실행

	```
	log@ubuntu:~/hadoop/hadoop-3.1.3$ sbin/start-dfs.sh 
	```

	![image-20200713004849294](/assets/images/2020-07-06-ubuntu18-hadoop-3/image-20200713004849294.png)

- yarn 실행

  ```
  log@ubuntu:~/hadoop/hadoop-3.1.3$ sbin/start-yarn.sh 
  ```

  ![image-20200713004955310](/assets/images/2020-07-06-ubuntu18-hadoop-3/image-20200713004955310.png)



## 2) 웹 사이트 확인 

웹사이트에서 하둡 동작 확인 

```
http://localhost:8088/cluster
```

![image-20200713005101711](/assets/images/2020-07-06-ubuntu18-hadoop-3/image-20200713005101711.png)

```
http://localhost:9870
```

![image-20200713005230395](/assets/images/2020-07-06-ubuntu18-hadoop-3/image-20200713005230395.png)

`참고` 하둡 3부터 50070 포트가 9870으로 변경됨.















