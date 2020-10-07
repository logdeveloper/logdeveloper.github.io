파일 설명

## File descriptions

- train.7z 
  - 정보파일과 오디오 파일 폴더
    - 오디오 폴더 : 1초의 음성 명령 클립이 있는 하위 폴더 포함, 폴더 이름은 오디오 클립 레이블이다. 예측해야할 레이블이 더 많다.
      - 레이블 :` yes`, `no`, `up`, `down`, `left`, `right`, `on`, `off`, `stop`, `go`
        - 다른 레이블은 알려져있지 않거나 침묵으로 간주(`unknown` or `silence`)
    - `__background__`폴더는 `silence`구간이 긴 클립을 포함하고 있다. 그래서 training input으로 사용할 수도 사용하지 못할 수도 있다.
  - 파일은 전반적으로 label이 training audio이 고유하지 않게 포함되어 있다. 만약 label 폴더에 포함한다면 그 파일은 고유한 것이다.
  
    - 예를 들어서 00f0204f_nohash_0.wav는 14개의 폴더에서 발견되지만, 그 파일은 각 폴더에서 다른 음성 명령이다.
  - 파일 이름을 붙여서 첫 번째 요소는 음성 명령을 내린 사람의 주체 ID로, 마지막 요소는 반복 명령을 가리킨다.
    - 반복된 명령은 피사체가 동일한 단어를 여러 번 반복하는 것을 말한다. 
    - Subject ID는 test dataset에 제공되지 않으며, test dataset의 대부분의 명령은 train 에서 볼 수 없는 과목에서 나온 것이라고 가정할 수 있다.
  
  - training data가 몇가지 불일치 하는 것을 예상할 수 있다.(ex : 오디오의 길이)
- test.7z
  - clip_000044442.wav 형식으로 150,000개 이상의 파일이 있는 오디오 폴더 포함.
  - 과제는 정확한 라벨을 예측하는 것이다. 
  - 모든 파일이 리더보드 점수에 대해 평가되는 것은 아니다.
- sample_submission.csv
  - 올바른 제출 파일 형식
- link_to_gcp_credits_form.txt
  -  처음 500명의 요청자에게 제공되는 GCP 크레딧에서 $500을 요청하기 위한 URL 제공. 신용 인증에 대한 설명을 참조





## Speech Commands Data Set v0.01

- 이것은 1초짜리 wav 오디오 파일 세트인데, 각각 하나의 구어 영어 단어를 포함하고 있다. 
- 이 단어들은 작은 명령어 집합에서 나온 것이며, 다양한 다른 스피커들에 의해 사용된다. 
- 오디오 파일은 포함된 단어를 기반으로 폴더로 구성되며, 이 데이터 세트는 간단한 머신러닝 모델을 교육할 수 있도록 설계되었다.



Creative Commons BY 4.0 라이선스에 따라 라이선스가 부여된다. 자세한 내용은 이 폴더의 LICE 파일을 참조하십시오. 원래 위치는 http:///다운로드였습니다.tensorflow.org/data/speech_commands_v0.01.tar.gz.



### History

2017년 8월 3일 발매된 6만4727개의 오디오 파일이 수록된 데이터 세트의 버전 0.01이다.



### Collection

- 오디오 파일은 크라우드소싱을 사용하여 수집되었다. 
- aiyprojects.withgoogle.com/open_speech_recording에서 우리가 사용한 오픈 소스 오디오 수집 코드 중 일부를 참조하면 된다.
- 대화형 문장이 아닌 단어의 명령어를 구사하는 사례를 수집하는 것이 목표였기 때문에 5분 동안 개별 단어를 입력하도록 유도되었다.
- 20개의 핵심 명령어가 기록되었는데, 대부분의 연사들이 각각 5번씩 말했다. 
  -  `Yes`, `No`, `Up`, `Down`, `Left`, `Right`, `On`, `Off`, `Stop`, `Go`, `Zero`, `One`, `Two`, `Three`, `Four`, `Five`, `Six`, `Seven`, `Eight`, and `Nine`
  - 인식되지 않는 단어를 구별할 수 있도록 하는 보조 단어 10개 :  `Bed`, `Bird`, `Cat`, `Dog`, `Happy`, `House`, `Marvin`, `Sheila`, `Tree`, and `Wow`
    - 대부분 단 한번씩만 말한다.



### Organization

- 파일들은 폴더로 구성되어 있고, 각각의 디렉토리 이름은 포함된 모든 오디오 파일에서 말하는 단어를 표시한다. 
- 참가자의 연령, 성별, 위치 등에 대한 세부사항은 기록되지 않았으며, 각 개인에게 무작위 ID가 할당되었다. 
  - 그러나 이러한 ID는 안정적이며, 밑줄 앞에 첫 번째 부분으로 각 파일 이름으로 인코딩된다.
- 참가자가 동일한 단어의 여러 발언을 한 경우, 파일 이름 끝에 있는 숫자로 구분한다. 
  - 예를 들어, 파일 경로 happy/3cfc6b3a_nohash_2.wav는 말하는 단어가 "행복하다"고, 말하는 사람의 ID는 "3cfc6b3a"이며, 이것은 데이터 집합에서 이 화자가 말한 단어 중 세 번째 발언이다. 
- `nohash` 섹션은 한 명의 발표자에 의한 모든 발언들이 동일한 훈련 칸막이로 분류되도록 하는 것으로, 매우 유사한 반복이 비현실적으로 긍정적인 평가 점수를 주는 것을 방지하는 것이다.





### Partitioning

- 오디오 클립이 교육, 테스트 및 검증 세트로 명확하게 분리되지 않았지만 관례에 따라 해싱 기능이 각 파일을 세트에 안정적으로 할당하는 데 사용된다. 

- 아래는 전체 파일 경로와 원하는 유효성 검사 및 테스트 세트 크기(대개 모두 10%)를 사용하여 세트를 할당하는 방법을 보여주는 몇 가지 Python 코드이다. 

  ```python
  python MAX_NUM_WAVS_PER_CLASS = 2**27 - 1 # ~134M
  def which_set(filename, validation_percentage, testing_percentage): 
  ```

  

- 우리는 시간이 지남에 따라 새로운 파일이 추가되더라도 동일한 교육, 검증 또는 테스트 세트에 파일을 보관하고 싶다. 따라서 예를 들어 장기 실행이 다시 시작될 때 테스트 샘플이 교육에 실수로 재사용될 가능성이 낮아진다. 이러한 안정성을 유지하기 위해 파일 이름의 해시를 가져와서 파일 이름이 어떤 집합에 속해야 하는지 결정하는 데 사용한다. 이 결정은 이름과 설정된 비율에만 의존하므로 다른 파일이 추가되더라도 변경되지 않는다.



- Args(파라미터)
  - 파일 이름: 데이터 샘플의 파일 경로. 
  - validation_validation: 유효성 검사에 사용할 데이터 세트의 양.
  -  testing_properties: 테스트에 사용할 데이터 세트의 양.





### Processing

- 원본 오디오 파일은 전세계 사람들에 의해 통제되지 않는 장소에서 수집되었다. 
- 사생활 보호를 이유로 밀폐된 방에서 녹음을 해달라고 요청했지만, 품질 요구 사항은 명시하지 않았다. 이것은 우리가 소비자와 로봇공학 애플리케이션에서 접하게 될 음성 데이터의 예를 원했기 때문에 디자인에 의한 것이었습니다. 녹음 장비나 환경에 대한 통제력이 별로 없는 곳이었다.
- 데이터는 웹앱용 Oggg Vorbis 인코딩 등 다양한 형식으로 캡처한 뒤 16000 샘플링 속도로 16비트 리틀엔디안 PCM 인코딩 WAVE 파일로 변환됐다. 그런 다음, 오디오를 1초 길이로 잘라 대부분의 발음을 정렬하고, ract_loudest_section 도구를 사용했다. 그리고 나서 오디오 파일들은 `slience`이나 부정확한 단어들로 가려졌고, 라벨에 의해 폴더로 정렬되었다.



### Background Noise

- 시끄러운 환경에 대처하기 위한 네트워크를 훈련시키기 위해, 현실적인 배경 오디오에 혼합하는 것이 도움이 될 수 있다. 
- _background_noise_ 폴더에는 녹음 또는 수학적 소음 시뮬레이션인 긴 오디오 클립이 포함되어 있다. 자세한 내용은 _properties_/README.md을 참조하면 된다.



### Citation

- 작업에서 음성 명령 데이터 집합을 사용하는 경우 아래의 케이스로 인용한다.
  - APA-style citation: "Warden P. Speech Commands: A public dataset for single-word speech recognition, 2017. Available from http://download.tensorflow.org/data/speech_commands_v0.01.tar.gz".
  - BibTeX @article{speechcommands, title={Speech Commands: A public dataset for single-word speech recognition.}, author={Warden, Pete}, journal={Dataset available from http://download.tensorflow.org/data/speech_commands_v0.01.tar.gz}, year={2017} }

