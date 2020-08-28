---
title: "[Python] Chapter5 자료의 입력과 출력 "
categories:   
  - Python
last_modified_at: 2020-08-15T11:00:00+09:00
toc: true
toc_sticky: true
toc_label: "목차"
tags:
  - 파이썬 자료 입력
  - 파이썬 자료 출력
sidebar:
  nav: posts

---

## Chapter5 자료의 입력과 출력
### 입력(input())
- 키보드로부터 문자열을 입력 받는 함수
  
    > variable_name = input(“Prompt string”)
    
    ① input() 함수의 인수로 지정된 문자열이 출력 프롬프트
    ② 그 문자열 뒤에 커서가 깜박이며 사용자로부터의 입력 기다림
    ③ 사용자가 키보드로 값을 입력하고 Enter 키를 누르면
    ④ 입력 받은 값이 문자열로 input() 함수의 반환 값이 됨
    ⑤ 반환된 값은 variable_name 에 할당되어 사용

- input() 함수의 반환값의 데이터 형은 string!!!
- input() 함수를 통하여 string 이 아닌 다른 유형을 입력 받으려면 , 입력받은 string 을 다른 유형으로 변환하여야 함    

- 두 개의 값을 입력 받기
    - String method 인 split( ) 을 사용하여 분리
    - input() 으로 입력 받은 문자열을 문자열의 메소드인 split() 함수를 사용하여 2 개의 문자열로 분리 .

```        
    >>> n = input("Enter two names :")
    Enter two names : Thom Bob
    >>> n1, n2 = n.split()
    >>>print(n1, n2)# type of n1 and n2 is string
    Thom Bob
```

- input() 함수는 입력 받은 데이터를 문자열로 반환
- 다른 데이터 형을 입력 받기 위해서는 입력된 문자열을 원하는 데이터 형으로 변환해야 함 .        

```
    >>> a = int ( input (("Enter an integer : ")
    Enter an integer : 123
    >>> b = float ( input (("Enter a float : ")
    Enter a float : 3.14    
    >>> c = input (("Enter a string :))
    Enter a string : Hello
    >>> print (a, b, c)
    123 3.14 Hello
    >>> print (type(a), type(b), type(c))
    <class int '> <class 'float'> <class str
```

### 출력 (print())
- 모니터 화면에 결과물을 출력하는 함수
- 함수의 인수를 모두 문자열로 바꾸어 출력하며 함수의 인수들은 출력하고자 하는 object 들임
- 함수의 인수 , object 와 object 사이에는 빈칸이 추가되어 출력 됨
- print() 함수는 출력시 기본 값으로 출력 문자열 마지막에 n 줄 바꿈 문자 가 더해짐 . 즉 출력시 줄바꿈이 발생함
- 줄 바꿈이 필요 없는 경우 , 함수의 end 인자 설정을 바꿈 .

```   
    >>> print("First Person.", end = ' '); 
        print("Second Person.")
        First Person. Second Person.
    >>> print("First Person.", end = '#');
        print("Second Person.")
        First Person.# Second Person.
```

### 출력 (print()) : 문자열 포매팅
- 실수 서식을 지정해서 출력

```
    >>> a = 1/3
    >>> print("1/3 =", a, "(too many digits).")
    1/3 = 0.3333333333333333 (too many digits).
    >>> print( "a = %.3f" % a)
    a = 0.333
```

- {0}, {1} 과 같은 인덱스뿐만 아니라 , 문자열의 {n}, {} 가 format 함수의 인수 값인 n='Luigi', age=35 값으로도 바뀜

```
    >>> print( 'My name is {0}. I am {1} years old.'.format ('Mario', '40'))
    My name is Mario. I am 40 years old.
    >>> print( 'My name is {n}. I am {age} years old.'.format(n='Luigi', age=35))
    My name is Luigi. I am 35 years old.
```

- 문자열 good” 을 위해 10 자리 만큼 폭을 잡고 왼쪽 정렬로 출력 문자열은 디폴트로 왼쪽 정렬

```    
    >>> print('T he light was {:10}.'.format('good'))
    The light was good .
```

- 숫자 3 을 위해 10 자리 만큼 폭을 잡고 오른쪽 정렬로 출력 숫자는 디폴트로 오른쪽 정렬

```
    >>> number = 3
    >>> print("I eat {:10} apples.".format(number))
    I eat 3 apples.
    >>> print("I eat {:<10} apples.".format(number))
    I eat 3 apples.    
```

### 출력 (print()) : example

```
    >>> i = 123; f = 3.14; s = 'Hello'
    >>> i : %d, f: %f, s: %s' % i , f, s
    i: 123, f: 3.140000, s: Hello
    >>> i : %9d, f: %5.2f, s: %7s' % i , f, s
    i: 123, f: 3.14, s: Hello
    >>> i : %09d, f: %05.2f, s: %7s' % i , f, s
    i: 000000123, f: 03.14, s: Hello
    >>> i : {}, f: {}, s: {}'. i , f, s
    i: 123, f: 3.14, s: Hello
    >>> print('f: {1}, i: {0}, s: {2}'. i , f, s)
    f: 3.14, i: 123, s: Hello
    >>> print('f: {ff}, i: {ii}, s: ss }'.format( i , ff =f, ss =Hello))
    f: 3.14, i: 123, s: Hello
    >>> print('a is {a}, b is {b}'.format(a = 'apple', b = 'banana'))
    a is apple, b is banana
```
