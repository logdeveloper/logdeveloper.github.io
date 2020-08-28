---
title: "[Linux] Ubuntu 18.04 고정(static) ip 설정"
categories:
  - Linux
last_modified_at: 2020-07-02T11:00:00+09:00
toc: true
toc_sticky: true
toc_label: "페이지 주요 목차"
tags:
  - Ubuntu 18.04
  - Ubunbtu Setting  
  - Setting
sidebar:
  nav: posts
---


우분투 18.04 버전에서 ip를 고정으로 할당하려면 이전 버전과는 다른 방법으로 설정해줘야 한다. 



우분투 18 LTS 이전 버전에서는 /etc/network 디렉토리에 있는 interfaces 파일에서 설정을 변경하거나 추가해주면 되지만, 

우분투 18 LTS 이후 버전에서는 netplan은 yaml을 사용한다. 



## 고정 아이피설정 방법

### 1. 본인의 이더넷 이름 확인



```bash
log@ubuntu:/usr/local/java$ ifconfig -a
```

![ubuntu-1](/assets/images/2020-07-02-ubuntu-static-ip-config/ubuntu-1.png)



필자의 이더넷 이름은 `ens33` 으로 확인하였다.



### 2. /etc/netplan 01-network-manager-all.yaml 파일 수정

/etc/netplan에 있는 yaml 파일을 수정해준다. 

```bash
log@ubuntu:/etc/netplan$ sudo nano 01-network-manager-all.yaml
```



![ubuntu-2](/assets/images/2020-07-02-ubuntu-static-ip-config/ubuntu-2.png)



sudo 계정으로 nano편집기로 파일을 연다.

```
# Let NetworkManager manage all devices on this system
network:
  version: 2
  renderer: NetworkManager
  ethernets:
    ens33:
      dhcp6: no
      addresses: [192.168.59.100/24]
      gateway4: 192.168.59.1
      nameservers:
        addresses: [8.8.8.8, 8.8.4.4]

```



해당 파일을 아래와 같이 수정한다. 

여기서  주의할 점은 띄어쓰기나, 문장 간격이 엄~~~~청 까다롭다는 것이다.  

꼼꼼하게 검토후 파일을 저장한다.



### 3. netplan 적용

아래의 명령어로 netplan 적용한다.

```bash
log@ubuntu:/etc/netplan$ sudo netplan apply
```



`주의` 조금이라도 규격에 맞지 않으면 netplan 적용시 아래와 같은 에러로 고생한다.

![ubuntu-3](/assets/images/2020-07-02-ubuntu-static-ip-config/ubuntu-3.png)

> 위의 에러는 `-` 특수문자로 ip 를 적었던 것을 []로 바꾸어서 적용했더니 성공하긴 했다..





### 4. 고정 ip 확인

```bash
log@ubuntu:/etc/netplan$ ifconfig
```





고정 ip 100 으로 잘 적용되었다.

![ubuntu-4](/assets/images/2020-07-02-ubuntu-static-ip-config/ubuntu-4.png)








#### 참고 사이트 

https://www.lesstif.com/lpt/ubuntu-18-lts-ip-static-ip-config-61899302.html