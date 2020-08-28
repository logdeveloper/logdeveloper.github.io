---
title: "[Intellij] JavaDoc 주석 + 파일 생성"
categories: 
  - Etc
last_modified_at: 2020-07-07T13:00:00+09:00
toc: true
toc_sticky: true
toc_label: "페이지 주요 목차"
tags:
  - JavaDoc
  - Intellij
  - 코드 관리
sidebar:
  nav: posts
---

IntelliJ에서 JavaDoc 설정하는 방법에 대해서 알아보자.

## 1. JavaDoc comment 추가

- 방법 1. 단축키 (window 기준) : ctrl+shift+alt+G
- 방법 2. 더블 shift -> create JavaDocs for all elements 실행

  ![1594111978665](/assets/images/2020-07-07-intellij-java-doc-setting/1594111978665.png)
    
- JavaDoc 코드 적용 전

  - Main Class

    ```java
    public class Main {
    
        public static void main(String[] args) {
            AddNumber addNumber = new AddNumber();
    
            System.out.println(addNumber.add(2, 6));
            System.out.println(addNumber.add(2, 3,4));
        }
    
    }
    ```

  - AddNumber Class

    ```java
    public class AddNumber {
    
        public int add(int a , int b){
            return a+b;
        }
    
        public int add(int a, int b , int c){
            return a+b+c;
        }
    }
    ```

    

- Java doc 코드 적용 후

  - Main Class
    
    ```java
    /**
     * The class Main.
     */
    public class Main {
    
        /**
         * The entry point of application.
         *
         * @param args the input arguments
         */
        public static void main(String[] args) {
            AddNumber addNumber = new AddNumber();
    
            System.out.println(addNumber.add(2, 6));
            System.out.println(addNumber.add(2, 3,4));
        }
    
    }
    ```

    
  
  - AddNumber Class
  
    ```java
    /**
     * The class Add number.
     */
    public class AddNumber {
    
        /**
         * Add int.
         *
         * @param a the a
         * @param b the b
         * @return the int
         */
        public int add(int a , int b){
            return a+b;
        }
    
        /**
         * Add int.
         *
         * @param a the a
         * @param b the b
         * @param c the c
         * @return the int
         */
        public int add(int a, int b , int c){
            return a+b+c;
        }
    }
    
    ```



## 2.  Java doc 생성

- 더블 shift + Generate JavaDoc

  ![001](/assets/images/2020-07-07-intellij-java-doc-setting/001.png)  



- JavaDoc 생성한 결과물을 저장할 폴더 경로 설정

  ![1594112035714](/assets/images/2020-07-07-intellij-java-doc-setting/1594112035714.png)


-  정상적으로 생성된 로그 확인
  ![1594112061642](/assets/images/2020-07-07-intellij-java-doc-setting/1594112061642.png)


- 설정 후 생성된 JavaDoc html 확인

  ![1594112078528](/assets/images/2020-07-07-intellij-java-doc-setting/1594112078528.png)

  ![1594112090544](/assets/images/2020-07-07-intellij-java-doc-setting/1594112090544.png)



## 참고 

### 한글 지원 옵션 

한글 지원을 위해선 아래 옵션을 기재해준다.

> ```
> -encoding UTF-8 -charset UTF-8 -docencoding UTF-8
> ```
  ![1594112687945](/assets/images/2020-07-07-intellij-java-doc-setting/1594112687945.png)





### JavaDoc Comment 형식 수정

- Setting > Tools > JavaDoc > Templates

  JavaDoc 주석 형식을 수정하여 사용 가능하다.

  ![1594112203829](/assets/images/2020-07-07-intellij-java-doc-setting/1594112203829.png)



### 주석 한줄로 보기

- Settings > Editor > Code Style > Java > JavaDoc 

  Do not wrap one line comments `체크`

  ![1594111863017](/assets/images/2020-07-07-intellij-java-doc-setting/1594111863017.png)

