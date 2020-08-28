```python
with open("config_kafka.json") as f :
    # config = json.load(f)
    raise FileNotFoundError("File does not exist.")
```

일부러 예외를 발생시킬 때, raise Exception 구문을 사용한다. ㅇ

