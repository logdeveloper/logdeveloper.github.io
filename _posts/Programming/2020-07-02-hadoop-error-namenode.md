---
title: "[Hadoop] hdfs namenode format error "
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
  - Hdfs Error
  - Hadoop Error
  - Namenode Format Error
  - hdfs 초기 설정
sidebar:
  nav: posts
---

##  현상

sidebar_main: true
search: true

hdfs 명령어로 namenode format 진행시, 발생한 문제이다. 

````bash
2020-07-03 10:47:32,709 INFO namenode.NameNode: createNameNode [-format]
2020-07-03 10:47:32,897 WARN util.NativeCodeLoader: Unable to load native-hadoop library for your platform... using builtin-java classes where applicable
2020-07-03 10:47:33,534 ERROR common.Util: Syntax error in URI \hadoop\namenode. Please check hdfs configuration.
java.net.URISyntaxException: Illegal character in path at index 0: \hadoop\namenode
        at java.net.URI$Parser.fail(URI.java:2848)
        at java.net.URI$Parser.checkChars(URI.java:3021)
        at java.net.URI$Parser.parseHierarchical(URI.java:3105)
        at java.net.URI$Parser.parse(URI.java:3063)
        at java.net.URI.<init>(URI.java:588)
        at org.apache.hadoop.hdfs.server.common.Util.stringAsURI(Util.java:91)
        at org.apache.hadoop.hdfs.server.common.Util.stringCollectionAsURIs(Util.java:139)
        at org.apache.hadoop.hdfs.server.namenode.FSNamesystem.getStorageDirs(FSNamesystem.java:1521)
        at org.apache.hadoop.hdfs.server.namenode.FSNamesystem.getNamespaceDirs(FSNamesystem.java:1476)
        at org.apache.hadoop.hdfs.server.namenode.NameNode.format(NameNode.java:1162)
        at org.apache.hadoop.hdfs.server.namenode.NameNode.createNameNode(NameNode.java:1645)
        at org.apache.hadoop.hdfs.server.namenode.NameNode.main(NameNode.java:1755)
2020-07-03 10:47:33,535 INFO common.Util: Assuming 'file' scheme for path \hadoop\namenode in configuration.
2020-07-03 10:47:33,542 ERROR common.Util: Syntax error in URI \hadoop\namenode. Please check hdfs configuration.
java.net.URISyntaxException: Illegal character in path at index 0: \hadoop\namenode
        at java.net.URI$Parser.fail(URI.java:2848)
        at java.net.URI$Parser.checkChars(URI.java:3021)
        at java.net.URI$Parser.parseHierarchical(URI.java:3105)
        at java.net.URI$Parser.parse(URI.java:3063)
        at java.net.URI.<init>(URI.java:588)
        at org.apache.hadoop.hdfs.server.common.Util.stringAsURI(Util.java:91)
        at org.apache.hadoop.hdfs.server.common.Util.stringCollectionAsURIs(Util.java:139)
        at org.apache.hadoop.hdfs.server.namenode.FSNamesystem.getStorageDirs(FSNamesystem.java:1521)
        at org.apache.hadoop.hdfs.server.namenode.FSNamesystem.getNamespaceEditsDirs(FSNamesystem.java:1566)
        at org.apache.hadoop.hdfs.server.namenode.FSNamesystem.getNamespaceEditsDirs(FSNamesystem.java:1535)
        at org.apache.hadoop.hdfs.server.namenode.NameNode.format(NameNode.java:1168)
        at org.apache.hadoop.hdfs.server.namenode.NameNode.createNameNode(NameNode.java:1645)
        at org.apache.hadoop.hdfs.server.namenode.NameNode.main(NameNode.java:1755)
2020-07-03 10:47:33,543 INFO common.Util: Assuming 'file' scheme for path \hadoop\namenode in configuration.
Formatting using clusterid: CID-48338ebc-ee81-4847-92ef-859e78319aa6
````



## 해결 방법

원인은 hdfs-site.xml 파일에서 파일경로 설정시, 상대경로, 절대경로 문제였다. 

dfs는 hadoop 소스가 상주하는 드라이브에 대한 경로를 상대적으로 가지고 있기 때문이다. 

해결하기 위해선 드라이브를 사용하고 있다면` /d:/ 앞에 접두사 슬래시를 사용`하면 된다. 

다른 방법으로는 datanode, namenode의 경로를 따로 설정하지 않으면 루트 폴더에 자동으로 생성되는 점을 활용하여 경로 옵션을 주지 않는 방법이 있다. 



### 참고 

[hadoop에서 네임 노드를 시작하지 못했습니까?]([https://www.it-swarm-ko.tech/ko/java/hadoop%ec%97%90%ec%84%9c-%eb%84%a4%ec%9e%84-%eb%85%b8%eb%93%9c%eb%a5%bc-%ec%8b%9c%ec%9e%91%ed%95%98%ec%a7%80-%eb%aa%bb%ed%96%88%ec%8a%b5%eb%8b%88%ea%b9%8c/822593574/](https://www.it-swarm-ko.tech/ko/java/hadoop에서-네임-노드를-시작하지-못했습니까/822593574/))

[Failed to start namenode in hadoop?](https://stackoverflow.com/questions/34871814/failed-to-start-namenode-in-hadoop)

