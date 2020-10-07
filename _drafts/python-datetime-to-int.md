## date to int

```
import time
milliseconds = int(round(time.time() * 1000))
print(milliseconds)
```



## datetime to int

```
from datetime import datetime
dt = datetime(2018, 1, 1)
milliseconds = int(round(dt.timestamp() * 1000))
print(milliseconds)
```



## int to datetime

```
sampletime = 1598604056058
date = datetime.datetime.fromtimestamp(sampletime / 1e3)
print(date)
```

