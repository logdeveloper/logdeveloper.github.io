## import library

```python
from pyspc import *
import numpy as np
import pandas as pd
```
## sample data

```python
print(circuits)
```

    [[100  21]
     [100  24]
     [100  16]
     [100  12]
     [100  15]
     [100   5]
     [100  28]
     [100  20]
     [100  31]
     [100  25]
     [100  20]
     [100  24]
     [100  16]
     [100  19]
     [100  10]
     [100  17]
     [100  13]
     [100  22]
     [100  18]
     [100  39]
     [100  30]
     [100  24]
     [100  16]
     [100  19]
     [100  17]
     [100  15]]



## ewma chart

```python
# ewma : 지수 가중 이동평균 모형으로 가중치를 가진 모형 
sample_basic_chart = spc(pistonrings) + ewma()
print(sample_basic_chart)
```


![png](output_2_0.png)


    <pyspc: (-9223371859563349920)>

## p-chart


```python
sample_p_chart = spc(circuits) + p() + rules()
# sample_p_chart = spc(circuits) + p()
print(sample_p_chart)
```


![png](output_4_0.png)

## xbar-R-chart

```python
sample_xbar_R_chart = spc(circuits) + xbar_rbar() +rules()
print(sample_xbar_R_chart)
```


![png](output_5_0.png)


    <pyspc: (-9223371859562247904)>

## cusum-chart

```python
sample_all = spc(pistonrings) + cusum() + rules()

print(sample_all)
```


![png](output_6_0.png)



## xbar-chart

```python
sample_all = spc(pistonrings) + xbar_sbar() + rules()

print(sample_all)
```


![png](output_7_0.png)


    <pyspc: (-9223371859562057004)>

## standard-deviation-chart

```python
sample_all = spc(pistonrings) + sbar() + rules()

print(sample_all)
```


![png](output_8_0.png)


## all-chart

```python
a = spc(pistonrings) + ewma()

sample_all = a + cusum() + xbar_sbar() + sbar() + rules()

print(sample_all)
```


![png](output_9_0.png)


    <pyspc: (-9223371859561935164)>

