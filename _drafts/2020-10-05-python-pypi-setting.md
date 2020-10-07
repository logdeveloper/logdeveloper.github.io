## pypi 홈페이지 가입 및 로그인



## 프로젝트 구성
폴더와 패키지 명을 동일하게 입력 설정한다. 

### 설정

루트 경로에 LICENCE, README.md, setup.py 파일을 생성한다.
이 파일을들 패키지에 대한 정보를 의미한다. 

이외에도 requirements.txt, MANIFEST,in 등의 파일을 포함할 수 있다.

### 실행 코드



## 업로드 실행

업로드하면 (패키지명).egg-info,  build, dist 폴더가 생성된다. 





```
(base) D:\pypi-sample>python -m pip install --user --upgrade setuptools wheel
Collecting setuptools
  Using cached setuptools-50.3.0-py3-none-any.whl (785 kB)
Requirement already up-to-date: wheel in d:\anacondadev\lib\site-packages (0.35.1)
Installing collected packages: setuptools
  WARNING: The scripts easy_install-3.7.exe and easy_install.exe are installed in 'C:\Users\hanbit\AppData\Roaming\Python\Python37\Scripts' which is not on PATH.
  Consider adding this directory to PATH or, if you prefer to suppress this warning, use --no-warn-script-location.
Successfully installed setuptools-50.3.0
```



```
(base) D:\pypi-sample>python setup.py sdist bdist_wheel
D:\AnacondaDev\lib\distutils\dist.py:274: UserWarning: Unknown distribution option: 'package'
  warnings.warn(msg)
running sdist
running egg_info
creating pypi_sample.egg-info
writing pypi_sample.egg-info\PKG-INFO
writing dependency_links to pypi_sample.egg-info\dependency_links.txt
writing top-level names to pypi_sample.egg-info\top_level.txt
writing manifest file 'pypi_sample.egg-info\SOURCES.txt'
reading manifest file 'pypi_sample.egg-info\SOURCES.txt'
writing manifest file 'pypi_sample.egg-info\SOURCES.txt'
running check
creating pypi-sample-0.1
creating pypi-sample-0.1\pypi_sample.egg-info
copying files to pypi-sample-0.1...
copying README.md -> pypi-sample-0.1
copying setup.cfg -> pypi-sample-0.1
copying setup.py -> pypi-sample-0.1
copying pypi_sample.egg-info\PKG-INFO -> pypi-sample-0.1\pypi_sample.egg-info
copying pypi_sample.egg-info\SOURCES.txt -> pypi-sample-0.1\pypi_sample.egg-info
copying pypi_sample.egg-info\dependency_links.txt -> pypi-sample-0.1\pypi_sample.egg-info
copying pypi_sample.egg-info\not-zip-safe -> pypi-sample-0.1\pypi_sample.egg-info
copying pypi_sample.egg-info\top_level.txt -> pypi-sample-0.1\pypi_sample.egg-info
Writing pypi-sample-0.1\setup.cfg
creating dist
Creating tar archive
removing 'pypi-sample-0.1' (and everything under it)
running bdist_wheel
running build
installing to build\bdist.win-amd64\wheel
running install
running install_egg_info
Copying pypi_sample.egg-info to build\bdist.win-amd64\wheel\.\pypi_sample-0.1-py3.7.egg-info
running install_scripts
creating build\bdist.win-amd64\wheel\pypi_sample-0.1.dist-info\WHEEL
creating 'dist\pypi_sample-0.1-py3-none-any.whl' and adding 'build\bdist.win-amd64\wheel' to it
adding 'pypi_sample-0.1.dist-info/METADATA'
adding 'pypi_sample-0.1.dist-info/WHEEL'
adding 'pypi_sample-0.1.dist-info/top_level.txt'
adding 'pypi_sample-0.1.dist-info/RECORD'
removing build\bdist.win-amd64\wheel
```

```
(base) D:\pypi-sample>pip install twine
Collecting twine
  Downloading twine-3.2.0-py3-none-any.whl (34 kB)
Requirement already satisfied: pkginfo>=1.4.2 in d:\anacondadev\lib\site-packages (from twine) (1.5.0.1)
Collecting requests-toolbelt!=0.9.0,>=0.8.0
  Downloading requests_toolbelt-0.9.1-py2.py3-none-any.whl (54 kB)
     |████████████████████████████████| 54 kB 536 kB/s
Collecting keyring>=15.1
  Downloading keyring-21.4.0-py3-none-any.whl (31 kB)
Requirement already satisfied: colorama>=0.4.3 in d:\anacondadev\lib\site-packages (from twine) (0.4.3)
Requirement already satisfied: requests>=2.20 in d:\anacondadev\lib\site-packages (from twine) (2.24.0)
Requirement already satisfied: tqdm>=4.14 in d:\anacondadev\lib\site-packages (from twine) (4.49.0)
Requirement already satisfied: setuptools>=0.7.0 in c:\users\hanbit\appdata\roaming\python\python37\site-packages (from twine) (50.3.0)
Collecting rfc3986>=1.4.0
  Downloading rfc3986-1.4.0-py2.py3-none-any.whl (31 kB)
Requirement already satisfied: importlib-metadata; python_version < "3.8" in d:\anacondadev\lib\site-packages (from twine) (1.7.0)
Collecting readme-renderer>=21.0
  Downloading readme_renderer-26.0-py2.py3-none-any.whl (15 kB)
Collecting pywin32-ctypes!=0.1.0,!=0.1.1; sys_platform == "win32"
  Downloading pywin32_ctypes-0.2.0-py2.py3-none-any.whl (28 kB)
Requirement already satisfied: idna<3,>=2.5 in d:\anacondadev\lib\site-packages (from requests>=2.20->twine) (2.10)
Requirement already satisfied: urllib3!=1.25.0,!=1.25.1,<1.26,>=1.21.1 in d:\anacondadev\lib\site-packages (from requests>=2.20->twine) (1.25.10)
Requirement already satisfied: certifi>=2017.4.17 in d:\anacondadev\lib\site-packages (from requests>=2.20->twine) (2020.6.20)
Requirement already satisfied: chardet<4,>=3.0.2 in d:\anacondadev\lib\site-packages (from requests>=2.20->twine) (3.0.4)
Requirement already satisfied: zipp>=0.5 in d:\anacondadev\lib\site-packages (from importlib-metadata; python_version < "3.8"->twine) (3.1.0)
Requirement already satisfied: bleach>=2.1.0 in d:\anacondadev\lib\site-packages (from readme-renderer>=21.0->twine) (3.2.1)
Requirement already satisfied: Pygments>=2.5.1 in d:\anacondadev\lib\site-packages (from readme-renderer>=21.0->twine) (2.7.1)
Requirement already satisfied: six in d:\anacondadev\lib\site-packages (from readme-renderer>=21.0->twine) (1.15.0)
Collecting docutils>=0.13.1
  Downloading docutils-0.16-py2.py3-none-any.whl (548 kB)
     |████████████████████████████████| 548 kB 1.6 MB/s
Requirement already satisfied: webencodings in d:\anacondadev\lib\site-packages (from bleach>=2.1.0->readme-renderer>=21.0->twine) (0.5.1)
Requirement already satisfied: packaging in d:\anacondadev\lib\site-packages (from bleach>=2.1.0->readme-renderer>=21.0->twine) (20.4)
Requirement already satisfied: pyparsing>=2.0.2 in d:\anacondadev\lib\site-packages (from packaging->bleach>=2.1.0->readme-renderer>=21.0->twine) (2.4.7)
Installing collected packages: requests-toolbelt, pywin32-ctypes, keyring, rfc3986, docutils, readme-renderer, twine
Successfully installed docutils-0.16 keyring-21.4.0 pywin32-ctypes-0.2.0 readme-renderer-26.0 requests-toolbelt-0.9.1 rfc3986-1.4.0 twine-3.2.0

```

```
(base) D:\pypi-sample>python -m twine upload dist/*
Uploading distributions to https://upload.pypi.org/legacy/
Enter your username: hanbit
Enter your password:
Uploading pypi_sample-0.1-py3-none-any.whl
100%|██████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████| 3.91k/3.91k [00:02<00:00, 1.39kB/s]
Uploading pypi-sample-0.1.tar.gz
100%|██████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████| 3.91k/3.91k [00:02<00:00, 1.39kB/s]
Uploading pypi-sample-0.1.tar.gz
100%|██████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████| 3.77k/3.77k [00:01<00:00, 3.25kB/s]

View at:
https://pypi.org/project/pypi-sample/0.1/
```

