---
title: "[DataScience][Study] 데이터 과학을 위한 통계 4-1"
categories:
  - Study
last_modified_at: 2020-07-25T11:00:00+09:00
toc: true
toc_sticky: true
toc_label: "주요 목차"
tags:
  - 회귀식
  - 적합값
  - 잔차
  - residual
  - 최소제곱
  - 예측
  - 다중선형회귀
  - 모형 평가
  - 교차 타당성 검사
  - cross validation
  - 가중회귀

sidebar:
  nav: posts

---

------------




# Chapter4. 회귀와 예측

- 통계학에서 일반적인 목표 : 변수 X (X~1~ ... X~p~) 가 변수 Y와 `관련`이 있는지? 이를 이용해 Y를 `예측`할 수 있는지?
- 통계와 데이터 과학이 강하게 연결되어 있다. 
  - `예측`변수 값을 기반으로 결과(목표) 변수를 예측분야
  - `이상 검출` 영역
- 회귀 진단은 비정상적인 데이터를 검출하는데 사용



## 4.1 단순 선형 회귀

- 단순선형회귀 모델 : 한 변수와 또 다른 변수의 크기 사이에 관계를 보여줌
  
- 변수간의 크기 : X↑  →   Y↑ , X↑  →   Y↓
  
  
  

### 4.1.1 회귀식

- 상관관계가 두변수 사이의 전체적인 관련 `강도를 측정`하는 것이라면, 회귀는 관계 자체를  `정량화`하는 방법이라는 점에서 차이가 있음.



### 4.1.1 회귀식 

- 단순선형회귀를 통해 X의 변화량에 따른 Y의 변화량을 추정 가능.

  - 상관계수의 경우 X, Y가 서로 바뀌어도 상관 없음
  - 회귀에서는 선형관계(즉, 직선)을 이용해 변수 X로부터 변수 Y를 예측하고자 함.

- X : 독립 변수, 예측 변수 (머신러닝에서 피처벡터)

- Y : 종속 변수, 응답 변수 (머신러닝에서 목표벡터)

- 사례 : 면진에 대한 노출 연수와 폐활량의 관계

  - R 함수 lm으로 선형회귀 함수 피팅

    ```R
    > model <- lm(PEFR ~ Exposure, data=lung)
    > model
    
    Call:
    lm(formula = PEFR ~ Exposure, data = lung)
    
    Coefficients:
    (Intercept)     Exposure  
        424.583       -4.185
    ```

    >- lm 함수는 선형 모형을 뜻함. linear model의 줄임말
    >- ~ 기호는 Exposure를 통해 PEFR을 예측한다
    >- 절편 b~0~ : 424.583
    >  - 노동자가 노출된 연수가 0일때 예측되는 PEFR이라고 해석 가능
    >- 회귀 계수 b~1~ : -4.185
    >  - 노동자가 면접에 노출되는 연수가 1씩 증가할 때마다 PEFR은 -4.185비율로 줄어듬.



### 4.1.2 적합값과 잔차

- 적합값 : 예측값 지칭. 보통  Y 햇으로 나타냄.

- 잔차 : 원래 값에서 예측한 값을 

- R에서 제공하는 predict와 residuals 함수

  ```R
  > fitted <- predict(model)
  > resid <- residuals(model)
  > 
  > fitted
         1        2        3        4        5        6        7        8 
  424.5828 424.5828 424.5828 424.5828 420.3982 416.2137 416.2137 416.2137 
         9       10       11       12       13       14       15       16 
  412.0291 412.0291 412.0291 412.0291 412.0291 412.0291 407.8445 407.8445 
  ...........................(생략).................................      
  > 
  > resid
             1            2            3            4            5 
   -34.5828066  -14.5828066    5.4171934   35.4171934   -0.3982301 
             6            7            8            9           10 
  -136.2136536    3.7863464  103.7863464  197.9709229  177.9709229 
            11           12           13           14           15 
    17.9709229   -2.0290771  -52.0290771  -92.0290771 -297.8445006 
  ...........................(생략).................................
  ```

  

### 4.1.3 최소제곱

- 실무에서 회귀선은 잔차들을 제곱한 값들의 합인 `잔차제곱합`(RSS : residual sum of squal)을 최소화하는 선
- 최소 제곱회귀 혹은 보통최소제곱회귀 : 잔차제곱합을 최소화하는 방법



### 4.1.4 예측 대 설명(프로파일링)

- 예전
  - 예측변수와 결과변수 사이에 있을것으로 추정되는 선형 관계를 밝히는 것이 회귀분석의 용도
  - 데이터 간의 관계를 이해하고 그것을 설명하는 것을 목표
  - 즉, 기울기 b를 추정하는 것에 초점
  - 사례 : 소비자 지출과 GDP 성장 간의 관계 추측
- 지금
  - 회귀분석은 새로운 데이터에 대한 개별 결과를 예측하는 모델(예측모델)을 구성하는데 사용
  - 주요 관심대상은 적합값(Y hat) 
  - 사례 : 마케팅에서 광고 캠페인의 크기에 따른 수익 변화 예측
- 데이터를 피팅한 회귀모형은 X의 변화가 Y의 변화를 유도하도록 설정.
  - 하지만 회귀방정식 자체가 인과관계가 되는 것은 아님.



## 4.2 다중선형회귀

- 예측 변수가 여러개일때
- 최소제곱법을 이용한 피팅, 적합값과 잔차의 정의 같은 단순선형회귀에서 다룬 기타 모든 개념은 다중선형회귀에도 그대로 확장되어 적용



### 4.2.1 킹 카운티 주택 정보 예제

- 주택 가치 추정은 회귀분석 대표적 사례 

- house라는 변수명을 가진 data.frame 객체에 저장된, 킹 카운티(워싱턴 시애틀 위치)의 주택 가격 데이터 일부

  ```R
  > head(house[, c("AdjSalePrice", "SqFtTotLiving", "SqFtLot", "Bathrooms",
  +                "Bedrooms", "BldgGrade")])
    AdjSalePrice SqFtTotLiving SqFtLot Bathrooms Bedrooms BldgGrade
  1       300805          2400    9373      3.00        6         7
  2      1076162          3764   20156      3.75        4        10
  3       761805          2060   26036      1.75        4         8
  4       442065          3200    8618      3.75        5         7
  5       297065          1720    8620      1.75        4         7
  6       411781           930    1012      1.50        2         8
  ```

- 목표 : 위의 변수들로부터 판매 금액을 예측하는 것.

- lm 함수의 우변에 더 많은 항을 추가함으로 다중회귀 사례 처리

  ```R
  > house_lm <- lm(AdjSalePrice ~ SqFtTotLiving+ SqFtLot+ Bathrooms+
  +                Bedrooms+ BldgGrade, data = house, na.action = na.omit)
  > house_lm
  
  Call:
  lm(formula = AdjSalePrice ~ SqFtTotLiving + SqFtLot + Bathrooms + 
      Bedrooms + BldgGrade, data = house, na.action = na.omit)
  
  Coefficients:
    (Intercept)  SqFtTotLiving        SqFtLot      Bathrooms       Bedrooms  
     -5.287e+05      2.127e+02     -1.430e-02     -1.823e+04     -4.657e+04  
      BldgGrade  
      1.088e+05
  ```

  > na.action = na.omit : 모델을 만들 때 결측값이 있는 레코드를 삭제하는 옵션 



### 4.2.2 모형 평가

- 제곱근 평균제곱오차(`RMSE`) 

  - 데이터 과학에서 가장 중요한 성능 지표
  - 예측된 Y hat 값들의 평균제곱오차의 제곱근
  - 전반적인 모델의 정확도를 측정하고 다른모데로가 비교하기 위한 기준이 됨.

- 잔차 표준오차 (`RSE`)

  - `RMSE`와 차이점은 분모가 데이터 수가 아닌 자유도

- 실무에서 `RMSE`와 `RSE`의 차이는 아주 작다.

- R의 summary 함수 : 회귀모형에 대한 `RSE`뿐 아니라 다른 지표들도 계산

  ```R
  > summary(house_lm)
  
  Call:
  lm(formula = AdjSalePrice ~ SqFtTotLiving + SqFtLot + Bathrooms + 
      Bedrooms + BldgGrade, data = house, na.action = na.omit)
  
  Residuals:
       Min       1Q   Median       3Q      Max 
  -1950841  -114032   -21451    83578  9549956 
  
  Coefficients:
                  Estimate Std. Error t value Pr(>|t|)    
  (Intercept)   -5.287e+05  1.443e+04 -36.629  < 2e-16 ***
  SqFtTotLiving  2.127e+02  3.401e+00  62.552  < 2e-16 ***
  SqFtLot       -1.430e-02  5.760e-02  -0.248    0.804    
  Bathrooms     -1.823e+04  3.225e+03  -5.654 1.58e-08 ***
  Bedrooms      -4.657e+04  2.329e+03 -19.999  < 2e-16 ***
  BldgGrade      1.088e+05  2.164e+03  50.266  < 2e-16 ***
  ---
  Signif. codes:  0 ‘***’ 0.001 ‘**’ 0.01 ‘*’ 0.05 ‘.’ 0.1 ‘ ’ 1
  
  Residual standard error: 259400 on 27057 degrees of freedom
  Multiple R-squared:  0.5348,	Adjusted R-squared:  0.5348 
  F-statistic:  6222 on 5 and 27057 DF,  p-value: < 2.2e-16
  ```

- 결정계수(R 제곱 통계량, R^2^) 

  - 범위는 0~ 1, 모델 데이터의 변동률 측정 
  - 모델이 데이터에 얼마나 적합한지 평가할 때 회귀분석을 설명하기 위한 용도로 활용됨.
  - 분모는 Y의 분산에 비례함.
  - R은 추정한 계수들과 함께, 계수의 표준오차(SE)와 t통계량을 함께 출력하여 보여줌. 

- t 통계량, p 값 : 계수가 통계적으로 유의미한 정도를 나타냄.
  - 즉, 예측변수와 목표변수를 랜덤하게 재배치했을 때 우연히 얻을 수 있는 범위를 어느정도 벗어났는지 측정.
  - t 통계량이 높을수록(p 값이 낮을 수록) 예측 변수는 더욱 유의미



### 4.2.3 교차타당성검사

- 전형적인 통계적 회귀 측정 지표들은 모두 표본내 지표들(데이터를 똑같이 그대로 사용)

- 데이터의 다수는 적합한 모델을 찾는데 사용하고, 소수는 모델을 테스트하는데 사용한다. 
  - 보통 비율이 70/30으로 잡는다.
- 교차 타당성검사(cross-validation)
  - 홀드아웃 샘플 아이디어를 여러 개의 연속된 홀드아웃 샘플로 확장한 것
  - 대표적으로 k 다중 교차타당성검사(k-fold cross-validation) 알고리즘이 있다.



### 4.2.4 모형 선택 및 단계적 회귀

- 많은 변수를 추사한다고 해서 꼭 더 좋은 모델을 얻는것은 아님 

- 모든 것이 동일한 조건에서는, 복잡한 모델보다는 단순한 모델을 우선 사용해야 함.

- 변수를 추가하면 항상 `RMSE`는 감소하고 R^2^ 은 증가.

- AIC : 모델에 항을 추가할수록 불이익을 주는 측정 기준

- AIC를 최소화하는 방법

  - 부분집합회귀

    - 모든 가능한 모델을 검색하는 방법 
    - 계산비용이 많이 들고, 대용량 데이터와 변수가 많은 문제에 적합하지 않다.

  - 단계적 회귀

    - 예측변수를 연속적으로 추가/삭제하여 AIC를 낮추는 모델

    - R에서는 MASS 패키지 사용

      ```R
      > step <-stepAIC(house_full, direction = "both")
      Start:  AIC=671316
      AdjSalePrice ~ SqFtTotLiving + SqFtLot + Bathrooms + Bedrooms + 
          BldgGrade + PropertyType + NbrLivingUnits + SqFtFinBasement + 
          YrBuilt + YrRenovated + NewConstruction
      
                        Df  Sum of Sq        RSS    AIC
      - NbrLivingUnits   1 3.6803e+09 1.6030e+15 671314
      - YrRenovated      1 1.2789e+10 1.6030e+15 671314
      - SqFtLot          1 2.5471e+10 1.6030e+15 671314
      - NewConstruction  1 7.1632e+10 1.6030e+15 671315
      <none>                          1.6030e+15 671316
      - SqFtFinBasement  1 2.8579e+11 1.6033e+15 671319
      - PropertyType     2 7.8637e+12 1.6108e+15 671444
      - Bathrooms        1 1.0095e+13 1.6131e+15 671484
      - Bedrooms         1 2.9035e+13 1.6320e+15 671800
      - SqFtTotLiving    1 1.4207e+14 1.7450e+15 673612
      - YrBuilt          1 1.4711e+14 1.7501e+15 673690
      - BldgGrade        1 2.3338e+14 1.8364e+15 674993
      
      Step:  AIC=671314.1
      AdjSalePrice ~ SqFtTotLiving + SqFtLot + Bathrooms + Bedrooms + 
          BldgGrade + PropertyType + SqFtFinBasement + YrBuilt + YrRenovated + 
          NewConstruction
      
                        Df  Sum of Sq        RSS    AIC
      - YrRenovated      1 1.2524e+10 1.6030e+15 671312
      - SqFtLot          1 2.5211e+10 1.6030e+15 671313
      - NewConstruction  1 7.2192e+10 1.6031e+15 671313
      <none>                          1.6030e+15 671314
      + NbrLivingUnits   1 3.6803e+09 1.6030e+15 671316
      - SqFtFinBasement  1 2.8911e+11 1.6033e+15 671317
      - PropertyType     2 7.8769e+12 1.6109e+15 671443
      - Bathrooms        1 1.0152e+13 1.6131e+15 671483
      - Bedrooms         1 2.9229e+13 1.6322e+15 671801
      - SqFtTotLiving    1 1.4222e+14 1.7452e+15 673613
      - YrBuilt          1 1.4802e+14 1.7510e+15 673702
      - BldgGrade        1 2.3544e+14 1.8384e+15 675021
      
      Step:  AIC=671312.3
      AdjSalePrice ~ SqFtTotLiving + SqFtLot + Bathrooms + Bedrooms + 
          BldgGrade + PropertyType + SqFtFinBasement + YrBuilt + NewConstruction
      
                        Df  Sum of Sq        RSS    AIC
      - SqFtLot          1 2.5083e+10 1.6030e+15 671311
      - NewConstruction  1 7.1293e+10 1.6031e+15 671311
      <none>                          1.6030e+15 671312
      + YrRenovated      1 1.2524e+10 1.6030e+15 671314
      + NbrLivingUnits   1 3.4152e+09 1.6030e+15 671314
      - SqFtFinBasement  1 2.9330e+11 1.6033e+15 671315
      - PropertyType     2 7.8650e+12 1.6109e+15 671441
      - Bathrooms        1 1.0238e+13 1.6132e+15 671483
      - Bedrooms         1 2.9219e+13 1.6322e+15 671799
      - SqFtTotLiving    1 1.4221e+14 1.7452e+15 673611
      - YrBuilt          1 1.6196e+14 1.7650e+15 673915
      - BldgGrade        1 2.3548e+14 1.8385e+15 675020
      
      Step:  AIC=671310.7
      AdjSalePrice ~ SqFtTotLiving + Bathrooms + Bedrooms + BldgGrade + 
          PropertyType + SqFtFinBasement + YrBuilt + NewConstruction
      
                        Df  Sum of Sq        RSS    AIC
      - NewConstruction  1 6.3500e+10 1.6031e+15 671310
      <none>                          1.6030e+15 671311
      + SqFtLot          1 2.5083e+10 1.6030e+15 671312
      + YrRenovated      1 1.2396e+10 1.6030e+15 671313
      + NbrLivingUnits   1 3.1669e+09 1.6030e+15 671313
      - SqFtFinBasement  1 2.8652e+11 1.6033e+15 671314
      - PropertyType     2 7.8468e+12 1.6109e+15 671439
      - Bathrooms        1 1.0215e+13 1.6132e+15 671481
      - Bedrooms         1 2.9451e+13 1.6325e+15 671801
      - SqFtTotLiving    1 1.4593e+14 1.7490e+15 673667
      - YrBuilt          1 1.6199e+14 1.7650e+15 673914
      - BldgGrade        1 2.3547e+14 1.8385e+15 675018
      
      Step:  AIC=671309.8
      AdjSalePrice ~ SqFtTotLiving + Bathrooms + Bedrooms + BldgGrade + 
          PropertyType + SqFtFinBasement + YrBuilt
      
                        Df  Sum of Sq        RSS    AIC
      <none>                          1.6031e+15 671310
      + NewConstruction  1 6.3500e+10 1.6030e+15 671311
      + SqFtLot          1 1.7290e+10 1.6031e+15 671311
      + YrRenovated      1 1.1567e+10 1.6031e+15 671312
      + NbrLivingUnits   1 3.7093e+09 1.6031e+15 671312
      - SqFtFinBasement  1 2.6805e+11 1.6033e+15 671312
      - PropertyType     2 8.5458e+12 1.6116e+15 671450
      - Bathrooms        1 1.0235e+13 1.6133e+15 671480
      - Bedrooms         1 2.9483e+13 1.6326e+15 671801
      - SqFtTotLiving    1 1.4722e+14 1.7503e+15 673686
      - YrBuilt          1 1.7535e+14 1.7784e+15 674117
      - BldgGrade        1 2.3572e+14 1.8388e+15 675020
      
      ```

      > 함수 실행 결과 house_full에서 sqFtLot, NbrLivingUnits, YrRenovated, NewConstruction 라는 변수들이 삭제된 모델을 선택함.

  - 전진선택, 후진선택

    - 전진선택 : 예측 변수 없이 각 단계에서 R^2^에 가장 큰 기여도를 갖는 예측 변수를 하나씩 추가하고 기여도가 통계적으로 더 이상 유의미하지 않을 때 중지
    - 후진 선택 : 전체 모델로 시작해서, 모든 예측 변수가 통계적으로 유의미한 모델이 될 때까지, 통계적으로 유의하지 않은 예측변수들을 제거해 나감.

- 별점회귀

  - 개념적으로는 AIC와 같다. 
  - 모델 적합 방정식에는 많은 변수(파라미터)에 대해 모델에 불이익을 주는 제약 조건을 추가
  - 계수 크기를 감소시키거나 경우에 따라서 거의 0으로 만들어 벌점을 적용
  - 방법 : 능형회귀, 라소

- 단계적 회귀분석과 모든 부분집합회귀 

  - 모델을 평가하고 조정하는 표본내 방법

  - 선택된 모델이 과적합(오버피팅)될 수 있음.

  - 이를 방지하기 위해 `교차타당성검사`를 통해 모델의 유효성을 알아보는 것

    



### 4.2.5 가중회귀

- 통계학자들은 다양한 목적으로 가중회귀 사용

- 복잡한 설문 분석에 중요

- 사례 

  - 주택 가격 데이터의 경우, 오래된 매매 정보일 수록 최근 정보보다는 신뢰하기 어렵다.

  - DocumentDate값을 이용하여 2005년(데이터 수집을 시작한) 이래 지난 연수를 가중치로 사용

    ```R
    > library(lubridate)
    > 
    > house$Year = year(house$DocumentDate)
    > house$Weight = house$Year - 2005
    > 
    > house_wt <- lm(AdjSalePrice ~ SqFtTotLiving+ SqFtLot+ Bathrooms+
    +                Bedrooms+ BldgGrade, data = house, weights = Weight)
    > round(cbind(house_lm=house_lm$coefficients,
    +             house_wt=house_wt$coefficients, digits=3))
                  house_lm house_wt digits
    (Intercept)    -528724  -580378      3
    SqFtTotLiving      213      230      3
    SqFtLot              0        0      3
    Bathrooms       -18233   -23335      3
    Bedrooms        -46574   -54234      3
    BldgGrade       108780   116037      3
    ```

    

****

> 참고 : 해당 포스트의 내용은 O'REILLY 시리즈 `데이터 과학을 위한 통계` ( 피터 브루스 & 앤드루 브루스 저, 한빛미디어 출판) 도서를 요약한 내용입니다.











