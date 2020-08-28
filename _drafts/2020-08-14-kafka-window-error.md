

현상 

window에서 kafka 운영시, 

`/`, `\`  구분을 명확하게 해줘야한다.

```powershell
log4j:ERROR Failed to rename [C:\kafka_2.12-2.5.0/logs/log-cleaner.log] to [C:\kafka_2.12-2.5.0/logs/log-cleaner.log.2020-08-13-17].
```

위와 같은 에러 발생
[stackoverflow](https://stackoverflow.com/questions/46318534/set-kafka-log-directory-property-in-windows) 를 참고하면 config 파일의 kafka log 경로를 아래와 같이 변경하라고 가이드 해준다. 

- server.properties 파일 수정
    ```properties
    ############################# Log Basics #############################

    # A comma separated list of directories under which to store log files
    # log.dirs=/kafkalog/kafka-logs-1
    log.dirs=\kafkalog\kafka-logs-1
    ```





수정하고 띄우면 아직까지는 error 가 발생하진 않는다. 

리눅스 기반이라 그런지 까다로운 것 같다. 