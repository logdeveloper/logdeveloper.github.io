python을 설치한 후 pip 설치를 한다. 



우선 pip 설치를 위해 get-pip.py 파일을 다운로드 한다. 

(만약 get-pip.py 파일이 있다면 생략해도 된다.)

```powershell
PS C:\WINDOWS\system32> curl https://bootstrap.pypa.io/get-pip.py -o get-pip.py
```



get-pip.py 파일을 통해 pip를 설치한다.

```powershell
PS C:\WINDOWS\system32> python get-pip.py
Collecting pip
  Downloading pip-20.2.3-py2.py3-none-any.whl (1.5 MB)
     |████████████████████████████████| 1.5 MB 1.1 MB/s
Collecting wheel
  Downloading wheel-0.35.1-py2.py3-none-any.whl (33 kB)
Installing collected packages: pip, wheel
  Attempting uninstall: pip
    Found existing installation: pip 10.0.1
    Uninstalling pip-10.0.1:
      Successfully uninstalled pip-10.0.1
Successfully installed pip-20.2.3 wheel-0.35.1
```



pip가 정상 설치 되었으면, 기본적으로 설치되어 있는 라이브러리를 확인해보자. 

```powershell
PS C:\WINDOWS\system32> pip list
Package    Version
---------- -------
pip        20.2.3
setuptools 39.0.1
wheel      0.35.1
```

