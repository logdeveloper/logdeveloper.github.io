---
title: "[Java] Java 1.8 DateTime"
categories:   
  - Java
last_modified_at: 2020-07-16T11:00:00+09:00
toc: true
tags:
  - junit5 
  - Java 1.8
  - Datetime
  - LocalDateTime
  - ZonedDateTime
  - TypeMismatch
  - ConversionFailedException
  - Failed to convert value of type String to required type ZonedDateTime
sidebar:
  nav: posts
---



## LocalDateTime

### LocalDateTime 단위 테스트

- TimeController.class

  ```java
  package com.example.demo;
  
  import org.springframework.web.bind.annotation.GetMapping;
  import org.springframework.web.bind.annotation.RestController;
  
  
  /**
   * The Class TimeController.
   */
  @RestController
  public class TimeController {
  
      @GetMapping("/test")
      public TestDTO helloDTO4(TestDTO testDTO){
          System.out.println(testDTO.toString());
          return testDTO;
      }
  
  }
  
  ```

  

- TestDTO.class

  ```java
  package com.example.demo;
  
  import org.springframework.format.annotation.DateTimeFormat;
  
  import java.time.LocalDateTime;
  
  /**
   * The Class .
   */
  public class TestDTO {
  
      private Long customerId;
  
      private String customerName;
  
      @DateTimeFormat(pattern = "yyyy-MM-dd'T'HH:mm:ss")
      private LocalDateTime registDateTime;
  
      public TestDTO(Long customerId, String customerName, LocalDateTime registDateTime) {
          this.customerId = customerId;
          this.customerName = customerName;
          this.registDateTime = registDateTime;
      }
  
      public Long getCustomerId() {
          return customerId;
      }
  
      public void setCustomerId(Long customerId) {
          this.customerId = customerId;
      }
  
      public String getCustomerName() {
          return customerName;
      }
  
      public void setCustomerName(String customerName) {
          this.customerName = customerName;
      }
  
      public LocalDateTime getRegistDateTime() {
          return registDateTime;
      }
  
      public void setRegistDateTime(LocalDateTime registDateTime) {
          this.registDateTime = registDateTime;
      }
  
      @Override
      public String toString() {
          return "TestDTO{" +
                  "customerId=" + customerId +
                  ", customerName='" + customerName + '\'' +
                  ", registDateTime=" + registDateTime +
                  '}';
      }
  
  }
  
  ```

  

- TimeControllerTest.class

  ```java
  package com.example.demo;
  
  import org.junit.jupiter.api.BeforeEach;
  import org.junit.jupiter.api.Test;
  import org.springframework.beans.factory.annotation.Autowired;
  import org.springframework.boot.test.autoconfigure.web.servlet.WebMvcTest;
  import org.springframework.test.web.servlet.MockMvc;
  import org.springframework.test.web.servlet.MvcResult;
  import org.springframework.test.web.servlet.ResultActions;
  import org.springframework.test.web.servlet.request.MockMvcRequestBuilders;
  import org.springframework.test.web.servlet.setup.MockMvcBuilders;
  import org.springframework.web.context.WebApplicationContext;
  import org.springframework.web.filter.CharacterEncodingFilter;
  
  import static org.springframework.test.web.servlet.result.MockMvcResultMatchers.status;
  
  @WebMvcTest
  class TimeControllerTest {
  
      @Autowired
      WebApplicationContext context;
  
      private MockMvc mockMvc;
  
      @BeforeEach
      void setUp() {
          mockMvc = MockMvcBuilders.webAppContextSetup(context)
                  .addFilter(new CharacterEncodingFilter("UTF-8", true))
                  .build();
  
      }
  
      @Test
      public void testDTO() throws Exception {
          //given
          String url = "/test?customerId=10&customerName=내이름은로그&registDateTime=2020-07-15T06:34:20";
  
          //when
          ResultActions resultActions = this.mockMvc.perform(MockMvcRequestBuilders.get(url));
  
          //then
          MvcResult mvcResult = resultActions
                  .andExpect(status().isOk())
                  .andReturn();
  
  
          System.out.println(mvcResult.getResponse().getContentAsString());
      }
  
  
  }
  ```

  

### 실행 결과

![1594802113823](/assets/images/2020-07-15-java-jdk8-time/1594802113823.png)



## ZoneDateTime

### LocalDateTime의 한계

java 8 time의 타임존 사용시 datetime에서는 사용할 수 없다. 사용하려고 하면 아래와 같은 에러가 발생한다. 

확인을 위해 TestDTO 클래스의 registDateTime의 데이터 형식만 ZoneDateTime으로 바꾸고 Test를 진행했다. 

- ZoneDateTime을 반영한 TestDTO 클래스

  ```java
  package com.example.demo;
  
  import org.springframework.format.annotation.DateTimeFormat;
  
  import java.time.LocalDateTime;
  import java.time.ZonedDateTime;
  
  /**
   * The Class .
   */
  public class TestDTO {
  
      private Long customerId;
  
      private String customerName;
  
      @DateTimeFormat(pattern = "yyyy-MM-dd'T'HH:mm:ss")
      private ZonedDateTime registDateTime;
  
      public TestDTO(Long customerId, String customerName, ZonedDateTime registDateTime) {
          this.customerId = customerId;
          this.customerName = customerName;
          this.registDateTime = registDateTime;
      }
  
      public Long getCustomerId() {
          return customerId;
      }
  
      public void setCustomerId(Long customerId) {
          this.customerId = customerId;
      }
  
      public String getCustomerName() {
          return customerName;
      }
  
      public void setCustomerName(String customerName) {
          this.customerName = customerName;
      }
  
      public ZonedDateTime getRegistDateTime() {
          return registDateTime;
      }
  
      public void setRegistDateTime(ZonedDateTime registDateTime) {
          this.registDateTime = registDateTime;
      }
  
      @Override
      public String toString() {
          return "TestDTO{" +
                  "customerId=" + customerId +
                  ", customerName='" + customerName + '\'' +
                  ", registDateTime=" + registDateTime +
                  '}';
      }
  
  }
  
  ```

  

테스트를 진행하면 아래와 같은 에러가 발생한다. 

![1594802388310](/assets/images/2020-07-15-java-jdk8-time/1594802388310.png)

Error 내용을 자세히 보면 TypeMismatch라는 내용이 있다. 

```bash
Field error in object 'testDTO' on field 'registDateTime': rejected value [2020-07-15T06:34:20]; codes [typeMismatch.testDTO.registDateTime,typeMismatch.registDateTime,typeMismatch.java.time.ZonedDateTime,typeMismatch]; arguments [org.springframework.context.support.DefaultMessageSourceResolvable: codes [testDTO.registDateTime,registDateTime]; arguments []; default message [registDateTime]]; default message [Failed to convert value of type 'java.lang.String[]' to required type 'java.time.ZonedDateTime'; nested exception is org.springframework.core.convert.ConversionFailedException: Failed to convert from type [java.lang.String] to type [@org.springframework.format.annotation.DateTimeFormat java.time.ZonedDateTime] for value '2020-07-15T06:34:20'; nested exception is java.lang.IllegalArgumentException: Parse attempt failed for value [2020-07-15T06:34:20]]]
```



String에서 Instant로 바꾸지 못했다는 뜻인데, 타임존에 대한 값을 넣어 주지 않으면, String으로 인식 되는 것 같다. 



타임존을 적용해서 사용하려면 입력값에도 타임존에 대한 값을 넣어줘야한다. 



### ZoneDateTime 단위 테스트

TestDTO, TimeControllerTest 클래스를 수정하여 다시 테스트 진행해보자. 

- TestDTO.class

  `Z` 포맷 형식 추가

  ```java
    @DateTimeFormat(pattern = "yyyy-MM-dd'T'HH:mm:ssZ")
      private ZonedDateTime registDateTime;
  ```

  

- TimeControllerTest.class

  `+0000` 타임존 값 추가

  ```java
     @Test
      public void testDTO() throws Exception {
          //given
          String url = "/test?customerId=10&customerName=내이름은로그&registDateTime=2020-07-15T06:34:20+0000";
          ...
          }
  
  ```





### 실행결과 

![1594802777773](/assets/images/2020-07-15-java-jdk8-time/1594802777773.png)



타임 존 사용을 위해 zonetimedate를 사용하자. 시간 형식을 표현하기 위한 참고 문서 이다.



## 참고

### 시간 형식 참고

구체적인 시간 형식이 궁금하다면 아래 사이트를 참고하면된다. 

<https://docs.oracle.com/javase/8/docs/api/java/text/SimpleDateFormat.html?is-external=true>

