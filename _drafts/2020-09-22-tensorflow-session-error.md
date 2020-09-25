

텐스플로우 1.0에서 텐서플로우 2.0으로 넘어오면서 session과 placeholder가 사라졌다. 

```
# 텐서플로 1.x
outputs = session.run(f(placeholder), feed_dict={placeholder: input})
# 텐서플로 2.0
outputs = f(input)
```

[tensorflow 공식 홈페이지](https://www.tensorflow.org/guide/effective_tf2?hl=ko)



만약 1.0version 기능 그대로 사용하고 싶다면 아래 라이브러리를 import해서 사용하면 된다.

```python
import tensorflow.compat.v1 as tf

tf.disable_v2_behavior()
```





2.0에서 그대로 사용하게 되면 현상과 대안에 대해서 알아보자. 

## session

### 1.0 사용시 에러 발생

tensor flow 실행시 아래와 같은 에러로 실행이 안됨

```python
import tensorflow as tf
```

```python
tf.__version__
```


    '2.3.0'



```python
hello = tf.constant("Hello, Tensor")
```


```python
sess = tf.Session() 
```

```
---------------------------------------------------------------------------
AttributeError                            Traceback (most recent call last)
<ipython-input-16-430b1c109abd> in <module>
----> 1 sess = tf.Session()

AttributeError: module 'tensorflow' has no attribute 'Session'
```





### 2.0 version에서 사용방법

tf.Session()은 1.0.0 version에서 사용하던 것이며, 2.0 version 이후엔 그냥 실행하면된다

```python
# sess = tf.Session() 
tf.print(hello)
```

    Hello, Tensor



.

## placeholder

### 1.0 사용시 에러 발생

````python
a = tf.placeholder(tf.float32)
b = tf.placeholder(tf.float32)
````

```python
---------------------------------------------------------------------------
RuntimeError                              Traceback (most recent call last)
<ipython-input-25-4ed639d73737> in <module>
----> 1 a = tf.placeholder(tf.float32)
      2 b = tf.placeholder(tf.float32)

D:\AnacondaDev\lib\site-packages\tensorflow\python\ops\array_ops.py in placeholder(dtype, shape, name)
   3095   """
   3096   if context.executing_eagerly():
-> 3097     raise RuntimeError("tf.placeholder() is not compatible with "
   3098                        "eager execution.")
   3099 

RuntimeError: tf.placeholder() is not compatible with eager execution.
```





### 2.0 version에서 사용방법

1. placeholder를 그대로 사용하고 싶다면, 아래와 같이 관련 라이브러리 import 와 세션 선택 후 실행

   ```python
   import tensorflow.compat.v1 as tf
   
   with tf.Session() as sess:
       x = tf.placeholder( tf.float32, [None, 784] )
   ```

   

2. 아래와 같은 사칙 연산에서 사용할때 굳이 필요없는 경우라면 numpy나 tensorflow 함수 그대로 사용

   [공식홈페이지 예제](https://www.tensorflow.org/guide/function?hl=ko#%EA%B8%B0%EC%B4%88)

   ```python
   import numpy as np
   
   # a = tf.placeholder(tf.float32)
   # b = tf.placeholder(tf.float32)
   
   @tf.function
   def addfunc(a,b):
       return a + b
   
   a = tf.constant(1)
   b = tf.constant(2)
   print(addfunc(a,b))
   
   c = tf.constant([1,2])
   d = tf.constant([3,4])
   print(addfunc(c,d))
   
   e = tf.constant([[1,2,3], [4,5,6]])
   f = tf.constant([[4,5,6], [7,8,9]])
   print(addfunc(e,f))
   
   ```

   ```python
   tf.Tensor(3, shape=(), dtype=int32)
   tf.Tensor([4 6], shape=(2,), dtype=int32)
   tf.Tensor(
   [[ 5  7  9]
    [11 13 15]], shape=(2, 3), dtype=int32)
   ```

   

## random_normal()

### 1.0 사용시 에러 발생

```python
# cost 함수의 변수 설정 
W = tf.Variable(tf.random_normal([1]), name="weight")
```

```python
---------------------------------------------------------------------------
AttributeError                            Traceback (most recent call last)
<ipython-input-13-4060169ece27> in <module>
      1 # cost 함수의 변수 설정
----> 2 W = tf.Variable(tf.random_normal([1]), name="weight")

AttributeError: module 'tensorflow' has no attribute 'random_normal'
```





### 2.0 version 사용 방법

```python
# cost 함수의 변수 설정 
W = tf.Variable(tf.random.normal([1]), name="weight")
b = tf.Variable(tf.random.normal([1]), name="bias")
```

