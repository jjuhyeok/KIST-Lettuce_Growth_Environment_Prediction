# KIST_Lettuce-Growth-Environment-Prediction  [(Link)](https://dacon.io/competitions/official/236033/overview/description)

## 🏆 Result
- **Public score 1st** 3.16772 | **Private score 4th** 7.65751 | **최종 2등(🏆)**

주최 : KIST

주관 : DACON

규모 : 약 800여명 참가


<img width="100%" src="https://github.com/jjuhyeok/KIST_Lettuce-Growth-Environment-Prediction/assets/49608953/13126173-812b-40a9-a6fa-6cedfabe1aed"/>

# 상추의 생육 환경 생성 AI 경진대회

===========================================================================

✏️
### **대회 느낀점**
 - 여러 대회들을 참여해보며 데이터가 재밌었고 항상 흥미로웠다.  
   하지만 이번 상추 대회 데이터를 보았을 때는, 이게 현실인가? 싶은 생각이 들었다.  
   이전까지 참여했던 대회들은 Train 데이터셋 CSV 1개, Test 데이터셋 CSV 1개
   이렇게 딱 2개로 주어져서 엄청 편했었다.  
   하지만 이번 대회는 Train 데이터셋 CSV가 56개가 존재 했었고, 데이터셋의 구조도 예측해야하는 Target 변수와 맞지 않았다.  
   상추 별로 24시간의 데이터가 28일치가 존재하였고(X), 해당 일에 해당하는 Weight(y)가 있었다.  
   데이터 셋의 구조가 X의 개수와 y의 row수와 일치하지 않았기 때문이다.(X==24, y==1)  

   그래서 이거 어떻게 해야하는거지? 라는 생각에 시작부터 의욕이 사라졌었다.  
   하지만 이미 칼을 뽑은 순간 무라도 배야 하지 않겠냐 라는 생각으로  
   꾸역 꾸역 흩어진 데이터셋들을 합치기 시작했고  
   데이터를 합치면서 놀라운 경험을 하게 되었다.  
   
   데이터는 주어져 있는게 아니라, 우리가 만들어 나가는 거구나?  
   이 작업을 하며 느꼈던 감정이다.  
   왜냐하면 타겟값인 train_y는 각 일(day)차의 00시에만 주어졌는데  
   train_x는 각 일(day)마다 1시간 간격으로 총 24개의 인덱스로 주어졌기 때문이다.  
   그래서 사실상 01시~23시의 train_x에 대한 train_y는 결측치로 되어있다.  

   이 글을 보고 있는 여러분이라면 어떻게 결측치를 처리할 것인가?  
   00시 데이터만 학습용으로 사용한다? 그냥 선형 보간을 한다? 아니면 regression imputation?  
   답은 정해져 있지 않다.  
   00시 데이터만 사용하여도 그 데이터를 어떻게 표현하느냐에 따라 예측 모델의 성능은 천차만별일 것이다.  
   좋을 확률은 적겠지만..  

   물론 target 값인 상추의 몸무게는 보통의 상황에서는 선형적으로 증가할 것이다.    
   하지만 나는 train_y에 대한 선형 보간을 하지 않고 00시의 train_y의 값만 사용하였다.  
   선형적으로만 보간하는 것은 "상"의 결과를 가져올 것이라 생각한다.    

   하지만 선형 보간한 값은 실제로 찍힌 값이 아니기 때문에 나는 단순히 선형으로 보간한 뒤 train_y 즉, target 값으로 학습하는 것은 싫었다.  

   나는 "최상"의 결과를 원했기 때문이다.    
   
   그렇게 나는 train_y는 00시의 실제 값만 사용하였고, 각각의 다른 인덱스인 01시~23시의 train_x 데이터들은 단순히 00시에 대한 피처로 transpose를 하여 사용하였다.  
   하지만 예측 모델의 정확도는 많이 좋지 않았다.  
   리더보드에서의 순위는 중상위권에 머물러 있었고  
   "최상"을 위해서는 새로운 접근법이 필요했다.  

   어느날 고기 800g을 세트로 파는 고기집에서  
   밥을 먹었던 적이 있다.  
   둘이서 밥을 먹으면서 "우리 둘이 800g 나눠서 살 찌는 중이야" 이랬었는데  
   문득 아이디어가 떠올랐다.  
   "어 상추도 밥을 먹을텐데 상추도 먹는 만큼 살(weight, target값)이 찌지 않을까?"  
   그렇다면 데이터에 상추별로 지금까지 밥을 얼마나 먹었는지 표현할 수 있는 변수를 추가를 해 볼까?  
   결과는 **대박**이었다.  
   데이터에 이러한 표현을 해주자 마자 예측 모델이 바로 반응을 해주었다.  
   리더보드 최상위에 진입을 할 수 있었고  
   이 날은 아직도 생생히 기억이 난다..  

   이번 대회를 통해 데이터를 보고 활용하는 시야가 정말 넓어진 것 같고  
   성장하는 모습이 바로바로 보이는 것 같아 정말 뿌듯하고  
   정성 평가에서도 나의 아이디어를 높게 평가해주신 것 같아 수상도 하게 되어 기뻤다.  

   
   
   

 

===========================================================================

<div align=center>
  
  ![단락 텍스트](./img/Lettuce%20Growth%20Environment%20Prediction.png)
</div>


<div align="center">
    
  ![Python Version](https://img.shields.io/badge/Python-3.8.16-blue)
</div>


## Host
- 주최 : KIST 강릉분원
- 주관 : Dacon
- 기간 : 11월 21일 (월) 10:00 ~ 12월 19일 (월) 10:00
- https://dacon.io/competitions/official/236033/overview/description
---
## 🧐 About
생육 환경 생성 AI 모델 결과를 바탕으로 상추의 일별 최대 잎 중량을 도출할 수 있는 최적의 생육 환경 조성


1. 상추의 일별 잎중량을 예측하는 **AI 예측 모델** 개발 
2. 1번의 예측 모델을 활용하여 생육 환경 **생성 AI 모델** 개발 
  - 생성 AI 모델 결과로부터 상추의 일별 최대 잎 중량을 도출할 수 있는 최적의 생육 환경 조성 및 제안 

---
## 🖥️ Development Environment
```
Google Colab
OS: Ubuntu 18.04.6 LTS
CPU: Intel(R) Xeon(R) CPU @ 2.20GHz
RAM: 13GB
```
---
## 🔖 Project structure

```
Project_folder/
|- data/  # required data (csv)
|- feature/  # feature engineering (py)
|- garbage/  # garbage 
|- generative_model/  # CTGAN Model (pkl)
|- predict_model/  # Autogluon Model (pkl)
|- config  # Setting (py)
|- *model  # notebook (ipynb)
|_ [Dacon]상추의-생육-환경-생성-AI-경진대회_상추세요  # ppt (pdf) 
```
## 📖 Dataset

```
Dataset Info.

- Input
Train, Test
CASE_01 ~ 28.csv (672, 16), TEST_01 ~ 05.csv (672, 16)
  DAT : 생육 일 (0~27일차)
  obs_time : 측정 시간
  상추 케이스 별 환경 데이터 (1시간 간격)

- Target
Train, Test
CASE_01 ~ 28.csv (28, 2), TEST_01 ~ 05.csv (28, 2)
  DAT : 생육 일 (1~28일차)
  predicted_weight_g : 일별 잎 중량
```


## 🔧 Feature Engineering
```
Feature selection.

누적값
- 구간별 시간에 대한 feature의 누적값
ex x 분무량
- 전체 평균에 대한 ec관측치와 분무량의 곱
수분량
- 자체 수분량 공식 사용
하루 평균
- 온도, 습도, co2, ec, 분무량, 적생광에 대한 하루 평균
Low-pass filter
- 누적값, ec x 분무량, 일평균에 적용
Kalman filter
- 누적값, ec x 분무량, 일평균에 적용
이동 평균
- 누적값, ec x 분무량, 수분량, 일평균에 적용
이동 중앙값
- 누적값, ec x 분무량, 수분량, 일평균에 적용
```

## 🎈 Modeling

**Predict Model**
```
AutoML: Autogluon, pycarat
Catboost
```
**Generative Model**
```
CTGAN
GAN
```



## 📖 Reference
CTGAN  
https://arxiv.org/abs/1907.00503  
https://github.com/sdv-dev/CTGAN  

생육환경  
https://scienceon.kisti.re.kr/srch/selectPORSrchArticle.do?cn=NPAP08069532&dbt=NPAP

