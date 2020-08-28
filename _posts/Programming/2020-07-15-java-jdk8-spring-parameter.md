---
title: "[Java][Springboot] Spring boot Java 1.8 Time 적용"
categories:   
  - Springboot
last_modified_at: 2020-07-15T11:00:00+09:00
toc: true
tags:
  - junit5 
  - Java 1.8
  - Datetime
  - Spring Annotation
  - DateTimeFormat
  - JsonFormat
  - LocalDateTime
  - ZonedDateTime
  - Instant
sidebar:
  nav: posts
---



springboot에서 java8 time을 사용하여 get 요청을 해오는 방법에 대해서 알아보자

### 테스트 코드

먼저 컨트롤러 및 DTO 클래스를 생성한다. 

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
      public TestDTO getTestDTO(TestDTO testDTO){
          System.out.println(testDTO.toString());
          return testDTO;
      }
  
  }
  
  ```



- TestDTO.class

  ```java
  package com.example.demo;
  
  import com.fasterxml.jackson.annotation.JsonFormat;
  import org.springframework.format.annotation.DateTimeFormat;
  
  import java.time.LocalDateTime;
  import java.time.ZonedDateTime;
  import java.time.Instant;
  
  /**
   * The Class .
   */
  public class TestDTO {
  
      private Long customerId;
  
      private String customerName;
  
      @DateTimeFormat(pattern = "yyyy-MM-dd'T'HH:mm:ss")
      private LocalDateTime registDateTime1;
  
      @DateTimeFormat(pattern = "yyyy-MM-dd'T'HH:mm:ssZ")
      private ZonedDateTime registDateTime2;
  
      @JsonFormat(shape = JsonFormat.Shape.STRING, pattern = "yyyy-MM-dd'T'HH:mm:ssZ", timezone = "Asia/Seoul")
      private Instant registDateTime3;
      
      // Getter, Setter, ToString..
  
  }
  
  ```



단위 테스트를 위해 아래 클래스를 생성한다.

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
  import org.springframework.test.web.servlet.request.MockHttpServletRequestBuilder;
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
  
          String url = "/test?customerId=10&customerName=내이름은로그&registDateTime1=2020-07-15T06:34:20&registDateTime2=2020-07-15T06:34:20+0000&registDateTime3=2020-07-15T06:34:20Z";
  
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

  

### 테스트 실행 결과

![1594862731349](/assets/images/2020-07-15-java-jdk8-spring-parameter/1594862731349.png)



### 테스트 내용 정리

아래는 테스트를 진행하며 주의해야할 점을 정리하였다.

- ZoneDateTime은 무조건 타임존 정보를 넣어줘야 한다.

  - 타임존 정보가 없으면 String으로 처리되어 에러가 발생한다.

- DateTimeFormat ISO 타입은 NONE, TIME, DATE, DATETIME 4가지로 정의된다.

  ![1594862737453](/assets/images/2020-07-15-java-jdk8-spring-parameter/1594862737453.png)

  

-  @DateTimeFormat으로 Instant 데이터가 처리 안될때가 있었다... (원인은 정확하게 못찾았지만,)

  - 정의되지 않은 시간 형식은 @JsonFormat으로 처리하였다. 
  
- @JsonFormat 형식은 Spring 2.x 버전 이후부터 포함되어 지원한다. 

  - 1.x 버전은 jackson-datatype-jsr310 라이브러리를 추가 해주어야한다.

