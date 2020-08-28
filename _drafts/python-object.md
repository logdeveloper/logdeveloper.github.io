## 생성자, 초기화, 소멸자 처리

### 객체 생명주기

- 생성자와 초기화로 객체 생성
- 객체를 다 사용하면 소멸자로 객체 삭제

- `__new__` : 클래스 객체를 만들때 사용
- `__init_` :  초기화 함수, 생성자를 통해 겍츨ㄹ 만든 후에 속성을 추가 할 때 사용

### 객체 생성 순서

- 클래스 정의할 때 생성자인 `__new__`함수 내에 상위 클래스의 `__new__`를 기준으로 아무런 속성이 없는 객체를 하나 생성
- `super().__new__` 로 실행하면, 최상위 클래스 object의 `__new_`가 실행되어 속성이 없는 빈객체를 만듦
- 그다음에 초기화를 작성하여 객체의 속성을 추가
  - 생성자 함수의 매개변수를 `*args`, `**kwargs`로 지정하는 초기화 함수의 매개변수를 항상 같은 인자를 전달받았기 때문.



### 예제

```python
class Agreement:
    # 객체를 만들때 사용하는 __new__ (생성자 함수)
    def __new__(cls, *args, **kwargs):
        return super().__new__(cls)

    # 생성자를 통해 객체를 만든 후, 속성을 추가할때 __init__ (초기화함수)를 사용 
    def __init__(self, name, age):
        self.name = name
        self.age = age
```


```python
a = Agreement("log", 10)
```


```python
# 객체의 이름 공간 확인
a.__dict__
```




    {'name': 'log', 'age': 10}




```python
# 객체의 클래스 확인
type(a)
```




    __main__.Agreement



```python
class Meta(type):
    def __call__(self, *args, **kwargs):
        print("메타 클래스 call 호출")
        instance = self.__new__(self, *args, **kwargs )
        instance.__init__(*args, **kwargs)
        return instance
```


```python
class Cond(metaclass=Meta):
    def __new__(cls, *args, **kwargs):
        return super().__new__(cls)
    def __init__(self, title, condition):
        self.title = title
        self.condition = condition
   def __del(self):
        del self
```


```python
aa = Cond("가입연령", "0세 이상")
```

    메타 클래스 call 호출



```python
aa
```




    <__main__.Cond at 0x182b285ee08>




```python
aa.__dict__
```





## 약한 참조







## 싱글턴(singleton) 패턴

