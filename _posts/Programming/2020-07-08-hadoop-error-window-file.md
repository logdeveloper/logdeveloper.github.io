---
title: "[Hadoop] Window NameNode & DataNode 실행 오류 "
categories: 
  - Hadoop
last_modified_at: 2020-07-08T11:00:00+09:00
toc: true
toc_sticky: true
toc_label: "페이지 주요 목차"
tags:
  - Window Hadoop  
  - Hadoop Error
  - UnsatisfiedLinkError
  - FileNotFoundException
  - DiskChecker DiskErrorException
sidebar:
  nav: posts
---

### 현상

하둡은 초기 리눅스 기반으로 운영되었기 때문에, 하둡 버전 2부터는 윈도우에서 실행은 되지만, 실제 실행시 자잘한 에러가 발생 한다. 
(리눅스의 파일 경로, 파일 권한 등 관련 이슈..)

그 중에 하나가 Hadoop 3 을 Window에서 설치 후, start-dfs.cmd 명령어 실행시 발생한 에러다. 

아래와 같이 datanode, namenode 모두 UnsatisfiedLinkError Error 발생하여 실행 되지 않는다. 

- namenode error 
```bash
2020-07-08 15:14:19,965 ERROR namenode.NameNode: Failed to start namenode.
java.lang.UnsatisfiedLinkError: org.apache.hadoop.io.nativeio.NativeIO$Windows.access0(Ljava/lang/String;I)Z
        at org.apache.hadoop.io.nativeio.NativeIO$Windows.access0(Native Method)
        at org.apache.hadoop.io.nativeio.NativeIO$Windows.access(NativeIO.java:640)
        at org.apache.hadoop.fs.FileUtil.canWrite(FileUtil.java:1242)
        at org.apache.hadoop.hdfs.server.common.Storage$StorageDirectory.analyzeStorage(Storage.java:667)
        at org.apache.hadoop.hdfs.server.common.Storage$StorageDirectory.analyzeStorage(Storage.java:620)
        at org.apache.hadoop.hdfs.server.namenode.FSImage.recoverStorageDirs(FSImage.java:384)
        at org.apache.hadoop.hdfs.server.namenode.FSImage.recoverTransitionRead(FSImage.java:240)
        at org.apache.hadoop.hdfs.server.namenode.FSNamesystem.loadFSImage(FSNamesystem.java:1103)
        at org.apache.hadoop.hdfs.server.namenode.FSNamesystem.loadFromDisk(FSNamesystem.java:718)
        at org.apache.hadoop.hdfs.server.namenode.NameNode.loadNamesystem(NameNode.java:644)
        at org.apache.hadoop.hdfs.server.namenode.NameNode.initialize(NameNode.java:706)
        at org.apache.hadoop.hdfs.server.namenode.NameNode.<init>(NameNode.java:949)
        at org.apache.hadoop.hdfs.server.namenode.NameNode.<init>(NameNode.java:922)
        at org.apache.hadoop.hdfs.server.namenode.NameNode.createNameNode(NameNode.java:1688)
        at org.apache.hadoop.hdfs.server.namenode.NameNode.main(NameNode.java:1755)
2020-07-08 15:14:19,969 INFO util.ExitUtil: Exiting with status 1: java.lang.UnsatisfiedLinkError: org.apache.hadoop.io.nativeio.NativeIO$Windows.access0(Ljava/lang/String;I)Z
2020-07-08 15:14:19,972 INFO namenode.NameNode: SHUTDOWN_MSG:
```

- datanode error 
```bash
2020-07-08 15:14:12,757 WARN util.NativeCodeLoader: Unable to load native-hadoop library for your platform... using builtin-java classes where applicable
2020-07-08 15:14:17,922 INFO checker.ThrottledAsyncChecker: Scheduling a check for [DISK]file:/C:/hadoop-3.1.3/hdfs/datanode
2020-07-08 15:14:17,958 WARN checker.StorageLocationChecker: Exception checking StorageLocation [DISK]file:/C:/hadoop-3.1.3/hdfs/datanode
java.lang.RuntimeException: java.io.FileNotFoundException: Could not locate Hadoop executable: C:\hadoop-3.1.3\bin\winutils.exe -see https://wiki.apache.org/hadoop/WindowsProblems
        at org.apache.hadoop.util.Shell.getWinUtilsPath(Shell.java:737)
        at org.apache.hadoop.util.Shell.getGetPermissionCommand(Shell.java:260)
        at org.apache.hadoop.fs.RawLocalFileSystem$DeprecatedRawLocalFileStatus.loadPermissionInfoByNonNativeIO(RawLocalFileSystem.java:727)
        at org.apache.hadoop.fs.RawLocalFileSystem$DeprecatedRawLocalFileStatus.loadPermissionInfo(RawLocalFileSystem.java:717)
        at org.apache.hadoop.fs.RawLocalFileSystem$DeprecatedRawLocalFileStatus.getPermission(RawLocalFileSystem.java:678)
        at org.apache.hadoop.util.DiskChecker.mkdirsWithExistsAndPermissionCheck(DiskChecker.java:233)
        at org.apache.hadoop.util.DiskChecker.checkDirInternal(DiskChecker.java:141)
        at org.apache.hadoop.util.DiskChecker.checkDir(DiskChecker.java:116)
        at org.apache.hadoop.hdfs.server.datanode.StorageLocation.check(StorageLocation.java:239)
        at org.apache.hadoop.hdfs.server.datanode.StorageLocation.check(StorageLocation.java:52)
        at org.apache.hadoop.hdfs.server.datanode.checker.ThrottledAsyncChecker$1.call(ThrottledAsyncChecker.java:142)
        at com.google.common.util.concurrent.TrustedListenableFutureTask$TrustedFutureInterruptibleTask.runInterruptibly(TrustedListenableFutureTask.java:125)
        at com.google.common.util.concurrent.InterruptibleTask.run(InterruptibleTask.java:57)
        at com.google.common.util.concurrent.TrustedListenableFutureTask.run(TrustedListenableFutureTask.java:78)
        at java.util.concurrent.ThreadPoolExecutor.runWorker(ThreadPoolExecutor.java:1149)
        at java.util.concurrent.ThreadPoolExecutor$Worker.run(ThreadPoolExecutor.java:624)
        at java.lang.Thread.run(Thread.java:748)
Caused by: java.io.FileNotFoundException: Could not locate Hadoop executable: C:\hadoop-3.1.3\bin\winutils.exe -see https://wiki.apache.org/hadoop/WindowsProblems
        at org.apache.hadoop.util.Shell.getQualifiedBinInner(Shell.java:620)
        at org.apache.hadoop.util.Shell.getQualifiedBin(Shell.java:593)
        at org.apache.hadoop.util.Shell.<clinit>(Shell.java:690)
        at org.apache.hadoop.util.StringUtils.<clinit>(StringUtils.java:78)
        at org.apache.hadoop.hdfs.server.datanode.DataNode.secureMain(DataNode.java:2899)
        at org.apache.hadoop.hdfs.server.datanode.DataNode.main(DataNode.java:2924)
2020-07-08 15:14:17,962 ERROR datanode.DataNode: Exception in secureMain
org.apache.hadoop.util.DiskChecker$DiskErrorException: Too many failed volumes - current valid volumes: 0, volumes configured: 1, volumes failed: 1, volume failures tolerated: 0
        at org.apache.hadoop.hdfs.server.datanode.checker.StorageLocationChecker.check(StorageLocationChecker.java:231)
        at org.apache.hadoop.hdfs.server.datanode.DataNode.makeInstance(DataNode.java:2799)
        at org.apache.hadoop.hdfs.server.datanode.DataNode.instantiateDataNode(DataNode.java:2714)
        at org.apache.hadoop.hdfs.server.datanode.DataNode.createDataNode(DataNode.java:2756)
        at org.apache.hadoop.hdfs.server.datanode.DataNode.secureMain(DataNode.java:2900)
        at org.apache.hadoop.hdfs.server.datanode.DataNode.main(DataNode.java:2924)
2020-07-08 15:14:17,968 INFO util.ExitUtil: Exiting with status 1: org.apache.hadoop.util.DiskChecker$DiskErrorException: Too many failed volumes - current valid volumes: 0, volumes configured: 1, volumes failed: 1, volume failures tolerated: 0
2020-07-08 15:14:17,972 INFO datanode.DataNode: SHUTDOWN_MSG:
```

### 해결 방법

아래의 방법을 시도해봤지만, 해결되지 않았다.
- dfs.datanode.failed.volumes.tolerated 옵션 추가
- dfs.name.dir, dfs.data.dir 옵션 삭제 (root로 지정되는 기본값 사용)

그래서 마지막으로 실행했던 방법이 hadoop.dll 파일과 winuils.exe 파일을 /bin 폴더에 넣는 방법 으로 했더니 해결되었다. 
![a5be4f70](/assets/images/2020-07-08-hadoop-error-window-file/a5be4f70.png)

다시 start-dfs.cmd 실행시 정상적으로 실행되었다.
- datanode
![37d3c9e5](/assets/images/2020-07-08-hadoop-error-window-file/37d3c9e5.png)

- namenode
![a8592d2d](/assets/images/2020-07-08-hadoop-error-window-file/a8592d2d.png)


 ps. 하둡은 리눅스에서 운영하는게 편한 것 같다..





















