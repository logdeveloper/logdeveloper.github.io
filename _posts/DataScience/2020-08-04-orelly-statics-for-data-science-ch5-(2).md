---
title: "[DataScience][Study] 데이터 과학을 위한 통계 5-2"
categories:
  - Study
last_modified_at: 2020-08-04T11:00:00+09:00
toc: true
toc_sticky: true
toc_label: "페이지 주요 목차"
tags:
  - 분류
  - 로지스틱 회귀
  - GLM
  - 일반화선형모형
  - 계수
  - 오즈비
  - 선형회귀
  - 모델 평가

sidebar:
  nav: posts

---

------------

# Chapter 5. 분류

## 5.3 로지스틱 회귀

- 로지스틱 휘귀 : 결과가 이진형 변수라는 점만 빼면 다중선형회귀와 유사함.
- 선형문제에 적합한 문제로 변환하기 위해 사용되는 다양한 변환방법
  - 판별 분석과 비슷
  - K 최근접 이웃, 나이브 베이즈와는 다름
  - 구조화된 모델 접근 방식 
- 빠른 점수 산정 덕분에 다양한 분야에서 널리 사용



### 5.3.1 로지스틱 반응 함수와 로짓

- 구성요소
  - 로지스틱 반응 함수 (logistic response function)
  - 로짓
- 확률(0~1사이의 단위)을 선형 모델에 적합한 더 확장된 단위로 매핑
- 선형 모델이다 보니 p가 0가 1사이로 딱 떨어지지 않을수 있다. 
  - 이럴 경우, 항상 p가 0에서 1 사이에 오도록 예측변수에 `로지스틱 반응` 혹은 `역 로짓` 함수를 적용해 p를 모델링함.
- 구하는 과정에서 분모의 지수 부분을 구하려면 확률 대신 오즈비를 이용
  - 오즈비 : 성공(1), 실패(0)의 비율, 사건이 발생할 확률을 사건이 발생하지 않을 확률로 나눈 비율.
  - 로그 오즈 함수 (로짓 함수) : 0과 1사이의 확률 p를 -∞ 에서 +∞ 까지의 값으로 매핑해줌.



### 5.3.2 로지스틱 회귀와 GLM

- 로지스틱회귀는 선형회귀를 확장한 일반화선형모형(GLM)의 특별한 사례

- R에서 로지스틱 회귀는 family인수를 binomial로 지정하고 glm 함수를 사용

  > 사례 : 개인 대출 정보를 이용해서 로지스틱 회귀를 구하는 코드

  ```R
  > logistic_model <- glm (formula = outcome ~ payment_inc_ratio + purpose_ + home_ +
  + emp_len_ + borrower_score, family = "binomial", data = loan_data)
  > 
  > logistic_model
  
  Call:  glm(formula = outcome ~ payment_inc_ratio + purpose_ + home_ + 
      emp_len_ + borrower_score, family = "binomial", data = loan_data)
  
  Coefficients:
                 (Intercept)           payment_inc_ratio  purpose_debt_consolidation  
                     1.63809                     0.07974                     0.24937  
    purpose_home_improvement      purpose_major_purchase             purpose_medical  
                     0.40774                     0.22963                     0.51048  
               purpose_other      purpose_small_business                    home_OWN  
                     0.62066                     1.21526                     0.04833  
                   home_RENT           emp_len_ > 1 Year              borrower_score  
                     0.15732                    -0.35673                    -4.61264  
  
  Degrees of Freedom: 45341 Total (i.e. Null);  45330 Residual
  Null Deviance:	    62860 
  Residual Deviance: 57510 	AIC: 57540
  > 
  ```

  > - outcome : 응답 변수 , 모두 갚으면 0, 연체 상태 1
  > - purpose_ , home_ : 대출 목적, 주택 소유 상태를 나타내는 요인 변수 
  > - creadit_card, MORTGAGE : 요인변수들에 대한 기준 수준
  > - borrower_score : 차용인의 신용도(불량에서 우수까지)를 나타내는 0에서 1까지의 점수



### 5.3.3 일반화선형모형

- 일반화선형모형(generalizal linear model : GLM)은 회귀와 함게 두번째로 가장 중요한 모델 
- 특징
  - 확률분포 또는 분포군(로지스틱 회귀의 경우 이항분포)
  - 응답을 예측변수로 매핑하는 연결 함수(로지스틱 회귀의 경우 로짓)
- 로지스틱 회귀는 GLM의 가장 널리 알려진 일반적인 형태 



### 5.3.4 로지스틱 회귀의 예측값

- 로지스틱 회귀에서 예측하는 값은 로그 오즈에 관한 값

- 예측된 확률은 로지스틱 반응 함수에 의해 주어짐.

  > logistic_model로부터 얻은 예측값

  ```R
  > pred <- predict(logistic_model)
  > summary(pred)
       Min.   1st Qu.    Median      Mean   3rd Qu.      Max. 
  -2.704774 -0.518825 -0.008539  0.002564  0.505061  3.509606 
  ```
  
  > 간단한 변환을 통해 확률값으로 바꿀 수 있음.
  
  ```R
  > prob <- 1/(1+exp(-pred))
  > summary(prob)
     Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
  0.06269 0.37313 0.49787 0.50000 0.62365 0.97096 
  ```
  
  > - 하지만 이 값들은  0에서 1사이에 있을 뿐이지, 아직 이 예측 결과가 연체인지 아니면 빚을 갚는 것인지는 분명히 말해주지 않음
  >
  > - 기본으로 0.5보다 큰 값을 사용하면 판별 가능.



### 5.3.5 계수와 오즈비 해석하기

- 로지스틱 회귀의 장점 
  - 재계산 없이 새 데이터에 대해 빨기 결과를 계산할 수 있음.
  - 모델을 해석하기가 다른 분류 방법들에 비해 상대적으로 쉽다.

- 확률 대신 오즈비를 사용하는 이유

  - 로지스틱 회귀분석에서 계수는  β~j~ 는 X~J~ 에 대한 오즈비의 로그값이기때문.

  

### 5.3.6 선형회귀와 로지스틱 회귀: 유사점과 차이점

- 공통점
  - 두 가지 모두 예측변수와 응답변수를 선형 관계로 가정.
  - 가장 좋은 모델을 탐색하고 찾는 과정도 아주 유사
  - 예측변수에 스플라인 변환을 사용하는 방법 모두 적용가능
- 차이점
  - 모델 피팅 방식
    - 선형 회귀 : 모델 피팅을 위해 `최소제곱` 사용, RMSE와 R 제곱 통계량을 사용하여 피팅의 성능을 평가.
    - 로지스틱 회귀 : 닫힌 형태의 해가 없으므로 `최대우도추정`(MLE:maximum likelihood estimation)을 사용하여 모델을 피팅
      - 최대우도추정 
        - 우리가 보고 있는 데이터를 생성했을 가능성이 가장 큰 모델을 찾는 프로세스
        - 로지스틱 회귀식에서 응답변수는 0이나 1이 아니라, 응답인 1인 로그 오즈비의 추정치
        - 예상 로그 오즈비가 관찰된 결과를 가장 잘 설명하는 모델을 찾음.
        - 피팅과정에서 편차라는 지표를 사용하여 모델을 평가하고, 편차가 작을 수록 모델 적합도가 높은 것을 의미.
  - 모델에서 잔차의 특징과 분석



### 5.3.7 모델 평가하기

- 모델이 새로운 데이터를 얼마나 정확하게 분류하는가를 기준으로 로지스틱 회귀를 평가.

- 선형회귀와 같이 표준 통계 도구들을 사용해 모델을 평가하고 향상시킬수 있음.

- 예측된 계수들과 함께 R은 계수들의 표준오차(SE), z 점수, p 값을 출력

  ```R
  > summary(logistic_model)
  
  Call:
  glm(formula = outcome ~ payment_inc_ratio + purpose_ + home_ + 
      emp_len_ + borrower_score, family = "binomial", data = loan_data)
  
  Deviance Residuals: 
       Min        1Q    Median        3Q       Max  
  -2.51951  -1.06908  -0.05853   1.07421   2.15528  
  
  Coefficients:
                              Estimate Std. Error z value Pr(>|z|)    
  (Intercept)                 1.638092   0.073708  22.224  < 2e-16 ***
  payment_inc_ratio           0.079737   0.002487  32.058  < 2e-16 ***
  purpose_debt_consolidation  0.249373   0.027615   9.030  < 2e-16 ***
  purpose_home_improvement    0.407743   0.046615   8.747  < 2e-16 ***
  purpose_major_purchase      0.229628   0.053683   4.277 1.89e-05 ***
  purpose_medical             0.510479   0.086780   5.882 4.04e-09 ***
  purpose_other               0.620663   0.039436  15.738  < 2e-16 ***
  purpose_small_business      1.215261   0.063320  19.192  < 2e-16 ***
  home_OWN                    0.048330   0.038036   1.271    0.204    
  home_RENT                   0.157320   0.021203   7.420 1.17e-13 ***
  emp_len_ > 1 Year          -0.356731   0.052622  -6.779 1.21e-11 ***
  borrower_score             -4.612638   0.083558 -55.203  < 2e-16 ***
  ---
  Signif. codes:  0 ‘***’ 0.001 ‘**’ 0.01 ‘*’ 0.05 ‘.’ 0.1 ‘ ’ 1
  
  (Dispersion parameter for binomial family taken to be 1)
  
      Null deviance: 62857  on 45341  degrees of freedom
  Residual deviance: 57515  on 45330  degrees of freedom
  AIC: 57539
  
  Number of Fisher Scoring iterations: 4
  ```

  > - p 값 해석시, 회귀에서 언급했던 주의사항도 동일함.
  > - 통계적인 유의성을 측정하는 지표로 보기보다는 변수의 중요성을 나타내는 상대적인 지표로 봐야함.
  > - 분류 문제에서 가장 일반적으로 사용되는 측정 지표들을 사용할 수 있음.


​    

- 로지스티 회귀에서 편잔차는 회귀에서보다 덜 중요함
- 하지만 비 선형성을 검증하고 영향력이 큰 레코드를 확인하는 데는 유용함.



****

> 참고 : 해당 포스트의 내용은 O'REILLY 시리즈 `데이터 과학을 위한 통계` ( 피터 브루스 & 앤드루 브루스 저, 한빛미디어 출판) 도서를 요약한 내용입니다.