---
title: "[Cassandra] Cassandra Unit Test - Junit5"
categories:   
  - NoSQL
last_modified_at: 2020-07-17T11:00:00+09:00
toc: false
tags:
  - junit5 
  - Java 
  - Cassandra
  - Unit Test
  - Cassandra Unit Spring
sidebar:
  nav: posts

---



## 카산드라 단위테스트



junit5를 활용하여 카산드라 단위테스트를 진행하려고 했지만, cassandra db는 따로 연결해 주어야하는 듯 싶다.

~~혹시나 다른 방법이 있다면 피드백 부탁드려요!~~



카산드라를 단위 테스트에 사용하기 위해 cassandra unit 라이브러리를 추가해주었다.

```yml
<dependency>
	<groupId>org.cassandraunit</groupId>
	<artifactId>cassandra-unit-spring</artifactId>
	<version>2.2.2.1</version>
</dependency>
```



그리고 test 파일에 @BeforeClass 주입된 클래스에 아래의 간단한 내용을 추가해준다. 

```java
....

@BeforeClass
public static void startServer() throws InterruptedException, TTransportException, ConfigurationException, IOException {
    EmbeddedCassandraServerHelper.startEmbeddedCassandra();
    Cluster cluster = new Cluster.Builder().addContactPoints("127.0.0.1").withPort(9142).build();
    Session session = cluster.connect();
    CQLDataLoader dataLoader = new CQLDataLoader(session);
    dataLoader.load(new ClassPathCQLDataSet("config/cql/create-tables.cql", true, "cassandra_unit_keyspace"));
}

....
```





>  참고 사이트 : <https://www.javatips.net/api/org.cassandraunit.utils.embeddedcassandraserverhelper>