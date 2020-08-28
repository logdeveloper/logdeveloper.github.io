---
title: "[DataScience][Study] 데이터 과학을 위한 통계 3-2"
categories:
  - Study
last_modified_at: 2020-07-23T11:00:00+09:00
toc: true
toc_sticky: true
toc_label: "페이지 주요 목차"
tags:
  - t 검정
  - 다중검정
  - 자유도
  - 분산분석
  - F 통계량
  - 카이제곱검정
  - 멀티암드 밴딧
  - 검정력
  - 표본크기
sidebar:
  nav: posts


---

# Chapter 3. 통계적 실험과 유의성 검정 (2)

## 3.5 t 검정

- 표준화된 형태의 검정 통계량

- 유의성 검정 방법 중 가장 자주 사용되는 t 검정(t-test)

  - 유의성 검정 : 관심있는 효과를 측정하기 위한 검정통계량을 지정, 관찰된 효과가 정상적인 랜덤 변이의 범위 내에 있는지 여부를 판단하는데 도움을 줌

- 척도에 상관없이 t분포를 사용하려면, ,표준화된 형태의 검정통계량을 사용해야한다.

- R에서는 t-test 사용

  ```R
  > t.test(Time ~ Page, data = session_times, alternative = 'less')
  
  	Welch Two Sample t-test
  
  data:  Time by Page
  t = -1.0983, df = 27.693, p-value = 0.1408
  alternative hypothesis: true difference in means is less than 0
  95 percent confidence interval:
        -Inf 0.1959674
  sample estimates:
  mean in group Page A mean in group Page B 
              1.263333             1.620000 
  
  
  ```

  > - 가설 : 페이지 A에 대한 평균 세션 시간이 페이지 B에 대한 평균보다 작다
  > - 이는 순열 검정을 통해 얻은  p=0.124과 매우 가깝다.

- 재표본추출 과정은 복잡하지만 데이터 과학자는 자세하게 알 필요는 없다..:)





## 3.6 다중검정

- 통계학에서는 다양한 관점으로 데이터를 보고 충분한 질문을 던지다 보면 거의 항상 통계적을 유의한 결과가 나옴.

- 하지만 변수가 많아지거나 다양한 모델을 사용하다보면 `우연에 의한` 유의미한 결과가 나타날 확률이 높아짐.

- 지도 학습에서는 이런 위험을 낮추기 위해, 홀드아웃 세트를 사용함

  - 홀드아웃은 교차검증 방벙의 범주에 속한것
  - 교차검증방법은 여러가지 있음 ex ) Holdout method, k-fold cross validation, Leave-p-out cross validation 등

- 통계학의 수정 절차는 단일 가설검정을 할대보다 통계적 유의성에 대한 기준을 엄격하게 세움.

  - 일반적으로 `검정횟수`에 따라 `유의수준`을 나눔.

- `중복도`같은 일반적인 문제를 포함하여 여러 가지 이유로 더 많은 연구가 반드시 나은 연구를 의미하는 것은 아님.

  



## 3.7 자유도

- 자유도 : 표본 데이터에서 계산된 통계량에 적용되며 변화가 가능한 값들의 개수를 나타냄
- 자유도는 많은 통계 검정에서 입력으로 주어지는 값. 
  - ex) 분산, 표준편차에서 분포에 표시된 `n-1`
    - `n-1`을 사용하면 추정값에 편향이 발생하지 않는다.
- 자유도는 표준화된 데이터가 그에 적합한 기준 분포(t분포, F분포 등)에 맞도록 하기 위한 표준화 계산의 일부.
- 하지만 데이터 과학에서는 유의성 검정 측면에서 중요하지 않다.
  - cf) 완전히 불필요한 예측변수들이 있는 경우 회귀 알고리즘 사용하기 어렵다.
    - ex) 일주일에 7일이 있지만 요일을 지정할때 자유도는 6일이다. 



## 3.8 분산분석

- 분산 분석 (analysis of variance, ANOVA) : 여러 그룹간의 통계적 유의미한 차이를 검정하는 통계적 절차.

  - 여러그룹(ex : A-B-C-D)의 수치를 서로 비교 

  - 사레 : 4개의 페이지로 이루어진 웹페이지에 5명의 사용자가 방문한 페이지 

  - 한 쌍씩 비교하게 되면 우연히 일어난 일에 속을 가능성이 커짐

  - ''원래 4개 페이지에 할당된 세션시간이 무작위로 할당된 것인가?"라는 질문을 다루는 `총괄검정` 필요

  - ANOVA 기반의재추출 과정

    1. 모든 데이터를 한 상자에 담아 놓음.
    2. 5개의 값을 갖는 4개의 재표본을 섞어서 추출
    3. 각 그룹의 평균을 기록
    4. 네그룹 평균 사이의 분산을 기록
    5.  2~4단계 여러번 반복

  - R의 lmPerm 패키시 사용

    ```R
    > summary(aovp(Time ~ Page, data = four_sessions))
    [1] "Settings:  unique SS "
    Component 1 :
                Df R Sum Sq R Mean Sq Iter Pr(Prob)  
    Page1        3    831.4    277.13 4072  0.09651 .
    Residuals   16   1618.4    101.15                
    ---
    Signif. codes:  0 ‘***’ 0.001 ‘**’ 0.01 ‘*’ 0.05 ‘.’ 0.1 ‘ ’ 1
    ```

    > - Pr (Prob) = p-value : 0.09651
    > - Iter : 4027 (4027번 반복)



### 3.8.1 F 통계량

- F통계량을기반으로 한 ANOVA 통계 검정도 있음

- F 통계량 : 잔차 오차로 인한 분산과 그룹 평균(처리 효과)의 분산에 대한 비율을 기초로함.

  - 비율이 높을수록 통계적으로 `유의미`

- R의 aov 함수 이용하여 ANOVA 테이블 계산

  ```R
  > summary(aov(Time ~ Page, data = four_sessions))
              Df Sum Sq Mean Sq F value Pr(>F)  
  Page         3  831.4   277.1    2.74 0.0776 .
  Residuals   16 1618.4   101.2                 
  ---
  Signif. codes:  0 ‘***’ 0.001 ‘**’ 0.01 ‘*’ 0.05 ‘.’ 0.1 ‘ ’ 1
  ```

  >- Df : 자유도
  >  - 처리 방법에 대한 평균의 자유도는 3이다
  >  - 3개의 평균과 함께 총 평균이 정해지면 나머지 평균은 달라질 수 없다.
  >- Sum sq : 제곱합
  >- Mean sq : 평균 제곱(평균 제곱 편차를 줄여서..)
  >- F value : F 통계량
  >
  >



### 3.8.2 이원 분산분석

- 위의 사례 A-B-C-D 검정은 변하는 요소(그룹)가 하나인 `일원`ANOVA이다.
- 두가지 요소르르 고려하여 분석하기 위해선 `이원` ANOVA가 필요함
  - 주말 대 평일 / 그룹 A, B, C, D



## 3.9 카이제곱검정

- 카이제곱 검정(chi-square test) : 횟수 관련 데이터에 주로 사용, 예상되는 분포에 얼마나 잘 맞는지 검정.
  - 웹 테스트시, 여러 가지 처리를 한 번에 테스트 할때..
- 일반적으로 변수 간 독립성에 대한 귀무가설이 타당한지 평가하기 위해 r*c 분할표 함께 사용
  - r과 c는 각각 행과 열의 수 의미



### 3.9.1 카이제곱검정: 재표본추출 방법

- 피어슨 잔차, R : 실제 횟수와 기대한 횟수 사이의 차이를 나타냄.

- R에서 chisq.test 함수 사용

  ```R
  > click_rate <-  read.csv(file = 'source/click_rates.csv')
  > clicks <- matrix(click_rate$Rate, nrow=3, ncol=2, byrow=TRUE)
  > chisq.test(clicks, simulate.p.value = TRUE)
  
  	Pearson's Chi-squared test with simulated p-value (based on 2000
  	replicates)
  
  data:  clicks
  X-squared = 1.6659, df = NA, p-value = 0.5057
  ```

  > 검증 결과는 관찰된 결과가 귀무가설 (랜덤)로부터 얼마든지 얻을 수있는 결과임을 알 수 있다.



### 3.9.2 카이제곱검정: 통계적 이론

- 점근적 통계 이론은 카이제곱통계량의 분포가 카이제곱분포로 근사화될 수 있음을 보여줌.

- 적절한 표준 카이제곱분포는 `자유도`에 의해 결정

  - 자유도 = (r-1) * (c-1)

- 카이제곱분포는 일반적으로 한쪽으로 기울어져 있고, 오른쪽 긴 꼬리가 있다.

- R의 chisq.test 함수를 이용하여 카이제곱분포에 대한 p 값 계산

  ```R
  > chisq.test(clicks, simulate.p.value = FALSE)
  
  	Pearson's Chi-squared test
  
  data:  clicks
  X-squared = 1.6659, df = 2, p-value = 0.4348
  ```

  > - p 값을 보면, 재표본추출해서 얻은 p 값보다 약간 작다.
  > - 이는 카이제곱분포가 실제 통계 분포가 아니라 근사치이기 때문이다.



### 3.9.3 피셔의 정확검정

- 피셔의 정확검정 : 모든 조합(순열)을 실제로 열거하고, 빈도를 집계하고, 관찰된 결과가 얼마나 극단적으로 발생할 수 있는지 정확하게 결정하는 절차를 제공.

- R에서의 피셔의 정확검정

  ```R
  > fisher.test(clicks)
  
  	Fisher's Exact Test for Count Data
  
  data:  clicks
  p-value = 0.4824
  alternative hypothesis: two.sided
  ```

  > 이렇게 얻은 p 값은 재표본추출 방법을 사용하여 얻은 p 값 0.4853과 매우 가깝다.



### 3.9.4 데이터 과학과의 관련성

- 대부분의 실험 목표는 단순히 통계적 유의성을 조사하는 것이 아니라 최적의 처리 방법을 찾는 것
- 피셔의 정확검정 활용 사례 
  - 웹 실험에 적합한 표본크기를 판별하는 일
    - 실험은 종종 클릭률이 매우낮기때문에 확실한 결론 도출 어려움.
    - 이때 피셔의 정확검증을 사용하여 검정력이나 표본크기를 게산하는데 유용하게 사용
- 데이터과학 응용분야에서는 `카이제곱검정`이나 이와 유사한 재표분 추출 시뮬레이션 필터로서 많이 사용
- 머신러닝에서는 자동으로 특징을 선택하기 위해 사용



## 3.10 멀티암드 밴딧 알고리즘

- 멀티암드 밴딧(Multi-Armed Bandit, MAB) : 전통적인 통계적 접근 방식보다 명시적인 쵲거화와 좀 더 빠른 의사 결정이 목표
  - 특히 웹테스트에 사용
- 밴딧 알고리즘은 하이브리드 접근 방식을 취한다. 
  - A,B,C 케이스가 있다면,  A의 우위를 활용하기 위해 검증하고 나머지 B, C도 포기하지 않는다.
- 적용 알고리즘
  - 앱실론-그리디 알고리즘
    - 앱실론 : 알고리즘을 제어하는 단일 파라미터
      - 앱실론이 1이면 표준 A/B 검정
      - 앱실론이 0이면 탐욕 알고리즘
  - 톰슨의 샘플링
    - 베이지언 방식 사용
    - 베타분포(사전 정보)를 사용하여 수익의 일부 사전 부포를 가정함.



## 3.11 검정력과 표본 크기

- 실험 진행시 표본크기에 대한 고려가 중요하다.
- 표본 크기에 대한 고려는 실제로 A와 B의 차이를 밝혀낼 수 있을지에 대한 질문과 연결된다.
  - p값(가설검정의 결과)은 A와 B의 차이에 따라 달라진다.
- A,B 의 차이가 작을 수록 더 많은 데이터가 필요하다.
- 검정력 : 특정 표본 조건(크기와 변이)에서 특정한 효과크기를 알아낼 수 있을 확률을 의미



### 3.11.1 표본크기

- 검정력 계산의 주된 용도는 표본크기가 어느 정도가 필요한가를 추정하는 것

- 작은 차이에도 관심이 있다면 훨씬 큰 표본이 필요함.

  - `효과크기`가 표본크기를 좌우함.

- `검정력` 혹은 `표본크기`의 계산과 관련된 다음 4가지 중요한 요소

  - 표본크기
  - 탐지하고자 하는 효과크기
  - 가설검정을 위한 유의수준
  - 검정력

- 위의 3가지를 정하면 나머지 하나를 알 수 있다.

- R코드에서는 pwr 패키지 사용 

  ```R
  pwr.2p.test(h=..., n=..., sig.level=..., power=...)
  ```

  > - h : 효과크기(비율)
  > - n : 표본크기
  > - sig.level : 검정을 수행할 유의수준(알파)
  > - power : 검정력(효과크기를 알아낼 확률)






