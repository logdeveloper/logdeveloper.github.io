---
title: "[Hadoop] Failed to start namenode"
categories:   
  - Hadoop
last_modified_at: 2020-07-12T11:00:00+09:00
toc: true
tags:
  - Linux
  - Hadoop Name Node Error
  - 폴더 권한
  - ERROR namenode.NameNode
  - Failed to start namenode
  - java.io.IOException
  - Cannot create directory
sidebar:
  nav: posts
sitemap :
  changefreq : daily
  priority : 1.0 
  
---

### 현상
하둡에서 namenode 실행시, 아래와 같은 오류가 발생하였다. 

```java
2020-07-04 09:08:39,574 INFO namenode.FSImage: Allocated new BlockPoolId: BP-812238600-127.0.1.1-1593878919566
2020-07-04 09:08:39,575 WARN namenode.NameNode: Encountered exception during format: 
java.io.IOException: Cannot create directory /home/hadoop/hadoop-3.1.3/data/namenode/current
	at org.apache.hadoop.hdfs.server.common.Storage$StorageDirectory.clearDirectory(Storage.java:436)
	at org.apache.hadoop.hdfs.server.namenode.NNStorage.format(NNStorage.java:579)
	at org.apache.hadoop.hdfs.server.namenode.NNStorage.format(NNStorage.java:601)
	at org.apache.hadoop.hdfs.server.namenode.FSImage.format(FSImage.java:186)
	at org.apache.hadoop.hdfs.server.namenode.NameNode.format(NameNode.java:1202)
	at org.apache.hadoop.hdfs.server.namenode.NameNode.createNameNode(NameNode.java:1645)
	at org.apache.hadoop.hdfs.server.namenode.NameNode.main(NameNode.java:1755)
2020-07-04 09:08:39,579 ERROR namenode.NameNode: Failed to start namenode.
java.io.IOException: Cannot create directory /home/hadoop/hadoop-3.1.3/data/namenode/current
	at org.apache.hadoop.hdfs.server.common.Storage$StorageDirectory.clearDirectory(Storage.java:436)
	at org.apache.hadoop.hdfs.server.namenode.NNStorage.format(NNStorage.java:579)
	at org.apache.hadoop.hdfs.server.namenode.NNStorage.format(NNStorage.java:601)
	at org.apache.hadoop.hdfs.server.namenode.FSImage.format(FSImage.java:186)
	at org.apache.hadoop.hdfs.server.namenode.NameNode.format(NameNode.java:1202)
	at org.apache.hadoop.hdfs.server.namenode.NameNode.createNameNode(NameNode.java:1645)
	at org.apache.hadoop.hdfs.server.namenode.NameNode.main(NameNode.java:1755)
2020-07-04 09:08:39,581 INFO util.ExitUtil: Exiting with status 1: java.io.IOException: Cannot create directory /home/hadoop/hadoop-3.1.3/data/namenode/current
2020-07-04 09:08:39,591 INFO namenode.NameNode: SHUTDOWN_MSG: 

```

### 해결

원인은 해당 폴더로 접근할 수 있는 권한이 없었기 때문이다. 
해결하기 위해선, 아래와 같이 폴더에 권한을 주면 된다. 

아래 예는 최상위 권한을 주었지만, 필요에 따라 변경하여 권한을 줄 수 있다.  

```
sudo chmod 777 /home/log/hadoop/hdfs/namenode/
```


