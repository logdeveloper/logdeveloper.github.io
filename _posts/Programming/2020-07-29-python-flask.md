---
title: "[Python] flask framework 적용"
categories:
  - Python
last_modified_at: 2020-07-29T11:00:00+09:00
toc: true
toc_sticky: truess
tags:
  - flask 
  - web service 
sidebar:
  nav: posts


---



## Flask 실습

### 1. Flask 설치

```powershell
PS C:\Windows\system32> pip install Flask
Collecting Flask
  Downloading Flask-1.1.2-py2.py3-none-any.whl (94 kB)
     |████████████████████████████████| 94 kB 632 kB/s
Requirement already satisfied: Jinja2>=2.10.1 in d:\anacondadev\lib\site-packages (from Flask) (2.11.2)
Collecting Werkzeug>=0.15
  Downloading Werkzeug-1.0.1-py2.py3-none-any.whl (298 kB)
     |████████████████████████████████| 298 kB 6.8 MB/s
Requirement already satisfied: click>=5.1 in d:\anacondadev\lib\site-packages (from Flask) (7.1.2)
Collecting itsdangerous>=0.24
  Using cached itsdangerous-1.1.0-py2.py3-none-any.whl (16 kB)
Requirement already satisfied: MarkupSafe>=0.23 in d:\anacondadev\lib\site-packages (from Jinja2>=2.10.1->Flask) (1.1.1)
Installing collected packages: Werkzeug, itsdangerous, Flask
Successfully installed Flask-1.1.2 Werkzeug-1.0.1 itsdangerous-1.1.0
```

>  `주의` : Flask는 Werkzeug와 Jinja2 라이브러리에 의존적이다.
>
> - Werkzeung : 웹어플리케이션과 다양한 서버 사이의 개발과 배포를 위한 표준 파이썬 인터페이스인 WSGI를 구현한 툴킷.
> - Jinja2 : HTML 템플릿을 렌더링 하는 템플릿 엔진 
>
> - anaconda가 설치되지 않았다면 virtualenv을 활용하여 설치 및 설정이 필요하지만, anaconda가 설치되어 있다면, flask 작동시 필요한 라이브러리를 설치해주기 때문에 신경쓰지 않아도 됨.



### 2. Pycharm 에서 간단한 코드 실행



#### 1) Intellij 에서 Flask Project 생성

![1595999236436](/assets/images/2020-07-29-python-flask/1595999236436.png)



#### 2) app.py 코드 작성

자동으로 생성된 app.py 파일 그대로 사용해도 되지만, 테스트를 위해 아래와 같이 코드를 조금 수정했다. 

```python
from flask import Flask

app = Flask(__name__)


@app.route('/')
def home():
    return 'Here is log\'s home!'

@app.route('/welcome')
def welcome_world():
    return 'Welcome log!'

@app.route('/hello')
def hello_world():
    return 'Hello log!'



if __name__ == '__main__':
    app.run()

```



#### 3) app.py 코드 실행 

Run을 실행하거나, `python app.py` 명령어를 실행한다. 

![1595999382982](/assets/images/2020-07-29-python-flask/1595999382982.png)

해당 테스트 URL을 실행해본다. 

> <http://127.0.0.1:5000/>
>
> ![1596001016917](/assets/images/2020-07-29-python-flask/1596001016917.png)

> <http://127.0.0.1:5000/hello>
>
> ![1596001026810](/assets/images/2020-07-29-python-flask/1596001026810.png)



> <http://127.0.0.1:5000/welcom>e
>
> ![1596001034446](/assets/images/2020-07-29-python-flask/1596001034446.png)





