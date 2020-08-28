---
title: "[DataScience][Study] 데이터 과학을 위한 통계 4-2"
categories:
  - Study
last_modified_at: 2020-07-25T11:00:00+09:00
toc: true
toc_sticky: true
toc_label: "주요 목차"
tags:
  - 회귀
  - 예측
  - 신뢰구간
  - 예측구간
  - 요인변수
  - 가변수
  - 회귀방정식 해석
  - 다중공선성
  - 교란변수
  - 주효과

sidebar:
  nav: posts

---

------------




# Chapter4. 회귀와 예측



## 4.3 회귀를 이용한 예측

- 데이터 과학에서 회귀의 목적은 `예측`
  - 전통적인 의미의 통계학에서는 `모델링`에 더 적합



### 4.3.1 외삽의 위험

- 외삽 (extrapolation) : 모델링에 사용된 데이터 범위를 벗어난 부분까지 모델을 확장하는 것.

- 회귀모형을 데이터 범위를 초과하면서까지 외삽하는 데 사용해서는 안됨.

  - 회귀보형은 충분한 데이터 값이 있는 예측변수에 대해서만 유효
  - 결과값을 예측하지 못할 수 있음

  

### 4.3.2 신뢰구간과 예측구간

- 통계학은 변동성(불확실성)을 이해하고 측정하는 것을 포함

  - 일반적인 방법 : 회귀분석 결과 `t통계량` , `p값`
  - 종종 변수 선택을 위해 활용
  -  이것은 `부트스트랩`으로 쉽게 이해 가능
    - `부트스트랩`: 회귀 파라미터(계수)에 대해 신뢰구간을 생성하기 위한 부트스트랩 알고리즘
    - R의 boot 함수를 사용하면 실제 부트스트랩 신뢰구간을 구할 수 있음.

- 데이터 과학자들은 예측된 y에만 관심이 있다.

  - 예측된 y 값의 불확실성의 원인

    1. 무엇이 적합한 예측변수 인지, 계수가 얼마인지 불확실성

    2. 개별 데이터 값에 존재하는 추가적인 오류 

       - 회귀방정식이 나오더라도 실제 결과값과는 다를 수 있음
       - 이러한 개별 오차를 적합값으로부터의 잔차로 모델링 가능

       

## 4.4 회귀에서의 요인변수

- 범주형 변수 : 요인변수, factor variable, 개수가 제한된 이산값
  - 예 : 대출목적 에서 '부채정리', '결혼', '자동차'등
- 지표 변수 : 이진변수 , 예/아니오로 구성
- 회귀분석에서는 수치 입력이 필요하기 때문에 요인변수를 수치화 해야됨
  - 가장 일반적인 방법이 가변수(dummy variable)들의 집합으로 변환하는 것



### 4.4.1 가변수 표현

- 사례 : 킹 카운티 주택 가격 데이터

  - 요인변수 확인

      ```R
      > head(house[, 'PropertyType'])
      [1] "Multiplex"     "Single Family" "Single Family" "Single Family"
      [5] "Single Family" "Townhouse"    
      ```

  - 요인변수를 이진변수로 변환 , R의 model.matrix 함수 구현

      ```R
      
      ```
  > prop_type_dummies <- model.matrix(~PropertyType -1, data=house)
      > head(prop_type_dummies)
        PropertyTypeMultiplex PropertyTypeSingle Family PropertyTypeTownhouse
      1                     1                         0                     0
      2                     0                         1                     0
      3                     0                         1                     0
      4                     0                         1                     0
      5                     0                         1                     0
      6                     0                         0                     1
  
      ```
      
      > R의 model.matrix 함수 
      >
      > - 선형모형에 적합한 행렬 형태로 변환
      >
      > - 머신러닝에서는 원-핫 인코딩이라고 부름.
      > - `-1` 기호는 절편을 삭제하는 것을 의미(= `P-1` 개의 이진 변수값 정의를 의미)


- 회귀분석에서는 P개의 개별 수준을 갖는 요인변수는 보통 `P-1`개의 열을 갖는 행렬로 표시
  
- P번째 열을 추가하면 `다중공선성` 오류가 발생
  
- R 회귀분석 결과

  ```R
  > lm(AdjSalePrice ~ SqFtTotLiving+ SqFtLot+ Bathrooms+
  +                Bedrooms+ BldgGrade + PropertyType, data = house)
  
  Call:
  lm(formula = AdjSalePrice ~ SqFtTotLiving + SqFtLot + Bathrooms + 
      Bedrooms + BldgGrade + PropertyType, data = house)
  
  Coefficients:
                (Intercept)              SqFtTotLiving  
                 -4.409e+05                  2.072e+02  
                    SqFtLot                  Bathrooms  
                 -2.314e-02                 -1.500e+04  
                   Bedrooms                  BldgGrade  
                 -4.957e+04                  1.122e+05  
  PropertyTypeSingle Family      PropertyTypeTownhouse  
                 -9.819e+04                 -1.189e+05  
  ```

  

### 4.4.2 다수의 수준을 갖는 요인변수들

- 요인변수는 가능한 수준의 수가 많으면, 많은 양의 이진 더미를 생성할 수있다. 

  - 사례 : 미국의 43,000개의 우편번호
  
- 주택 가격 산정에 우편번호는 위치에 대한 효과를 볼 수 있는 변수

  - 우편번호를 그대로 사용할 수 없으므로 성격이 비슷한 변수끼리 그룹으로 묶거나

  - 회귀 결과의 잔차값의 중간값을 기준으로 5개의 그룹으로 통합함.

  - R 적용

    ```R
    library(dplyr)    # alternatively, this also loads %>%
    
    zip_groups <- house %>%
      mutate(resid = residuals(house_lm)) %>%
      group_by(ZipCode) %>%
      summarize(med_resid =median(resid),
                cnt = n()) %>%
      arrange(med_resid) %>%
      mutate(cum_cnt = cumsum(cnt),
             ZipGroup = ntile(cum_cnt, 5))
    
    house <- house %>%
      left_join(select(zip_groups, ZipCode, ZipGroup), by ='ZipCode')
    ```

    > - 각 우편번호에 대한잔차의 중간값을 계산
    >
    > - ntile함수를 사용해 중간값으로 정렬한 우편번호를 5개의 그룹으로 분할
    > - 회귀 적합화를 돕는 데 잔차를 사용한다는 개념은 모델링 프로세스의 기본 단계!



### 4.4.3 순서가 있는 요인변수

- 요인 변수중 순서를 갖는 경우가 있다.
  - 예 : 대출 등급이 A,B,C 로 나누어짐.
- 순서 요인은 일반적으로 숫자 값으로 변환하여 그대로 사용할 수 있음.
  - 이렇게 함으로 순서에 대한 정보를 유지함.



## 4.5 회귀방정식 해석

- 회귀의 가장 중요한 용도는 일부 종속변수(결과변수)를 예측하는 것
- 때론 예측변수와 결과 간 관계의 본질을 이해하기 위해 방정식 자체로부터 통찰을 얻기도함.



### 4.5.1 예측변수 간 상관

- 다중회귀분석에서 예측 변수는 종종 서로 상관성이 있음

- house 회귀 분석 사례를 알아보자.

  ```R
  > step_lm$coefficients
                (Intercept)             SqFtTotLiving                 Bathrooms 
               6.227632e+06              1.865012e+02              4.472172e+04 
                   Bedrooms                 BldgGrade PropertyTypeSingle Family 
              -4.980718e+04              1.391792e+05              2.332869e+04 
      PropertyTypeTownhouse           SqFtFinBasement                   YrBuilt 
               9.221625e+04              9.039911e+00             -3.592468e+03 	
  ```

  > - 침실 개수 변수(Bathrooms) : 음수 -> 침실 개수를 늘릴수록 그 가치가 감소한다는 것을 의미.
  >
  > - 그 이유는 예측 변수들이 서로 연관되어 있기 때문.
  >   - 집이 클수록 침실이 더 많은 경향
  >   - 침실 수 보다는 주택의 크기가 주택 가격에 더 큰 영향을 줌.
  >   - 침실 수, 평수, 욕실 수에 대한 변수들은 모두 상관관계가 있음.	

- 위의 방정식에서 SqFtTotLiving, SqFtFinBasement, Bathrooms 제거한 후 얻은 회귀모형

  ```R
  > update(step_lm, . ~ . -SqFtTotLiving - SqFtFinBasement - Bathrooms)
  
  Call:
  lm(formula = AdjSalePrice ~ Bedrooms + BldgGrade + PropertyType + 
      YrBuilt, data = house, na.action = na.omit)
  
  Coefficients:
                (Intercept)                   Bedrooms                  BldgGrade  
                    4834680                      27657                     245709  
  PropertyTypeSingle Family      PropertyTypeTownhouse                    YrBuilt  
                     -17604                     -47477                      -3161  
  
  
  ```

  > - R의 업데이트 함수 사용
  >   - 모델의 변수를 추가 하거나 제외할 수 있음
  > - Bedrooms변수가 양수, 실제 주택크기에 대한 대리 변수로 사용 





### 4.5.2 다중공선성

- 변수 상관의 극단적이 경우 다중 공선성이 나타남

  - 이는 예측변수 사이의 중복성을 판단하는 조건이 됨.

- 완전 다중공선성 : 한 예측변수가 다른 변수들의 선형결합으로 표현

- 다중공성선이 발생하는 경우

  - 오류로 인해 한 변수가 여러 번 포함된 경우
  - 요인변수로부터 P-1개가 아닌 P 개의 가변수가 만들어진 경우
  - 두 변수가 서로 거의 완벽하게 상관성이 있는 경우

- 회귀분석에서는 다중공선성이 사라질때까지 변수를 제거해야함.

  - 그렇지 않으면 제대로된 답을 얻기가 어려움.

    



### 4.5.3 교란변수

- 회귀방정식에 중요한 변수가 포함되지 못해서 생기는 누락의 문제.

- 주택 가격 예측에서 우편번호를 통해 위치정보를 알 수 있는데, 이전 회귀 분석에서는 이것을 포함되어 있지 않았다.

- 아래는 우편번호를 통해 위치정보를 포함하여 회귀분석을 결과이다.

  ```R
  > lm(AdjSalePrice ~ SqFtTotLiving+ SqFtLot+ Bathrooms+
  +                Bedrooms+ BldgGrade + PropertyType + ZipGroup, data = house, na.action = na.omit)
  
  Call:
  lm(formula = AdjSalePrice ~ SqFtTotLiving + SqFtLot + Bathrooms + 
      Bedrooms + BldgGrade + PropertyType + ZipGroup, data = house, 
      na.action = na.omit)
  
  Coefficients:
                (Intercept)              SqFtTotLiving                    SqFtLot  
                 -6.719e+05                  1.941e+02                  3.507e-01  
                  Bathrooms                   Bedrooms                  BldgGrade  
                  7.845e+03                 -3.939e+04                  1.043e+05  
  PropertyTypeSingle Family      PropertyTypeTownhouse                  ZipGroup2  
                  4.296e+03                 -2.032e+04                  5.948e+04  
                  ZipGroup3                  ZipGroup4                  ZipGroup5  
                  1.042e+05                  1.756e+05                  3.342e+05  
  ```

  > - zipgroup : 우편번호를 가장 싼 지역 (1), 가장 비싼 지역(5)까지 5개 그룹으로 분류
  > - 위치에 따라 가격이 올라가는 것을 확인할 수 있다.



### 4.5.4 상호작용과 주효과

- 주효과 : 회귀방정식에서 종종 예측변수라고 불림.

- 모델에서 주효과만 사용한다면, 여기에는 예측변수와 응답변수 간의 관계가 다른 예측변수들에 대해 독립적이라는 가정이 있지만 `사실이 아니다`

- R의 `*`연산자를 사용하면 모델에 변수의 상호작용을 포함시킬수 있음

  ```R
  > lm(AdjSalePrice ~ SqFtTotLiving*ZipGroup+ SqFtLot+ Bathrooms+
  +                Bedrooms+ BldgGrade + PropertyType, data = house, na.action = na.omit)
  
  Call:
  lm(formula = AdjSalePrice ~ SqFtTotLiving * ZipGroup + SqFtLot + 
      Bathrooms + Bedrooms + BldgGrade + PropertyType, data = house, 
      na.action = na.omit)
  
  Coefficients:
                (Intercept)              SqFtTotLiving                  ZipGroup2  
                 -4.984e+05                  1.034e+02                 -3.741e+04  
                  ZipGroup3                  ZipGroup4                  ZipGroup5  
                  5.502e+04                 -1.412e+03                 -1.719e+05  
                    SqFtLot                  Bathrooms                   Bedrooms  
                  5.507e-01                  3.207e+02                 -3.895e+04  
                  BldgGrade  PropertyTypeSingle Family      PropertyTypeTownhouse  
                  1.082e+05                  5.978e+03                 -2.206e+04  
    SqFtTotLiving:ZipGroup2    SqFtTotLiving:ZipGroup3    SqFtTotLiving:ZipGroup4  
                  4.985e+01                  1.575e+01                  8.321e+01  
    SqFtTotLiving:ZipGroup5  
                  2.355e+02  
  ```

  > - SqFtTotLiving:ZipGroup2, SqFtTotLiving:ZipGroup3등의 4가지 새로운 정보들을 볼 수 있음
  > - 주택의 위치와 크기는 강한 상호작용이 있는 것으로 보임.

- 상호작용 항들은 랜덤 포레스트나 그레이디언트 부스팅 트리같은 트리모델에서 가장 일반적으로 사용됨



****

> 참고 : 해당 포스트의 내용은 O'REILLY 시리즈 `데이터 과학을 위한 통계` ( 피터 브루스 & 앤드루 브루스 저, 한빛미디어 출판) 도서를 요약한 내용입니다.

















