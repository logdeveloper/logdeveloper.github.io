---
title: "[Python] 'DataFrame' object has no attribute 'ix'"
categories:   
  - Python
last_modified_at: 2020-07-12T11:00:00+09:00
toc: true
tags:
  - Python
  - AttributeError
  - ix attribute
  - ilo attribute
sidebar:
  nav: posts
---



## 현상

 파이썬 실행 중 아래와 같은 에러가 발생하였다. 

```python
AttributeError: 'DataFrame' object has no attribute 'ix'
```



[pandas doc](<https://pandas.pydata.org/pandas-docs/version/0.23.4/generated/pandas.DataFrame.ix.html>) 를 참고하면  ix 함수는 사라지고 `.loc` 혹은 `.iloc`로 대체 되었다.



## 해결방법

해결 방법은 간단한다.  `ix`자리에  `.loc` 혹은 `.iloc`로 수정하여 사용하면 된다. 

- 사용 예

	```python
........
	
	# axs[i].plot(data.ix[:, 0])
	# axs[i].plot(data.ix[:, 0][(data.ix[:, i+1] == True)], 'ro')
	axs[i].plot(data.iloc[:,0])
	axs[i].plot(data.iloc[:, 0][(data.iloc[:, i + 1] == True)], 'ro')
	
	........
	```





