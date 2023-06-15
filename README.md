# KIST_Lettuce-Growth-Environment-Prediction  [(Link)](https://dacon.io/competitions/official/236033/overview/description)

## 🏆 Result
- **Public score 1st** 3.16772 | **Private score 4th** 7.65751 | **최종 2등(🏆)**

주최 : KIST

주관 : DACON

규모 : 약 800여명 참가



# 상추의 생육 환경 생성 AI 경진대회

===========================================================================

✏️
**대회 느낀점**
 - 실제 도로에서 나타나는 현상(ex, 러시아워)을 적용하는 과정에서 외부 데이터를 많이 사용하며 성능을 끌어올려 제공된 데이터 뿐만 아닌 외부의 많은 데이터를 융합하는 시야를 넓혔고, 실제 도로에서 과속이나 차량 사고 시 도로 막힘 현상에 대해
   고려를 해야 하는것이 맞나, 맞지 않나를 생각하며 다양한 이상치 처리 방법(3sigma, IQR)들을 적용시켜 보았고 이런 경험을 통해 데이터에 나타나는 여러가지 이상 현상에 대해 생각하는 자세를 가지게 되었습니다.
   
   또한 대회 중 수 많은 피처 중에 "Lane count" 즉 차선 수 피처가 존재했었는데, 차선 별로 나누어서 모델링을 했던 적이 있었고 예측 모델의 성능이 잘 나왔습니다.
   하지만 이전 대회에서 Data-Leakage 이슈가 있었기 때문에 이러한 모델링 방법이 맞는지에 대해 생각을 하게 되었고,
   train 데이터셋에는 차선이 1,2,3 차선 종류만 존재했었습니다. 하지만 train 데이터셋에 존재하지않는 차선 수, 예를 들어 5차선, 10차선이 test 데이터셋에 존재하면 어떻게 되는거지? 라는 생각이 들어.
   이 방법은 Data-Leakage 라 판단을 하고 이러한 방법론을 과감하게 버린 후 새로운 방법으로 모델링을 진행하였습니다.
   대회가 종료된 후 저희가 버렸던 방법론인 차선 별로 모델링을 진행한 팀이 존재하였고, 결국 그 팀은 2차 평가에서 Data-Leakage로 실격처리 되었습니다.

   또한 외부데이터를 사용하며 카카오맵 API를 연동하여 방문자수, 리뷰수가 많은 구간들은 사람들이 많이 몰리는 **Hot Place** 구간으로 그 주변 도로들의 평균 속도가 전체적으로 낮아질 것이라는 가설을 세우고 모델에 적용을 시켰습니다.
   이 방법을 사용하였을 때 예측 성능이 가장 많이 향상 되었지만 카카오맵API는 실시간으로 업데이트가 되기 때문에 test셋인 2022년 8월 데이터를 포함하게 됩니다.
   그래서 최종적으로 카카오맵 API를 사용하는 방법도 버리게 되었지만, 실제 end-to-end 모델을 개발하여 실시간으로 예측할 때는 많은 도움이 될 것이라 생각하여 주최사측에 의견 전달을 하였습니다.
   
   이러한 경험을 통해 현재 제공된 데이터셋(train)에서 어떻게 test 데이터를 보지 않고 일반화 성능을 올리는지에 대해 많은 생각을 할 수 있었고 앞으로도 이러한 이슈에는 유연하게 잘 대응을 할 수 있을 것입니다.

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
**Data Source**  [Train Test Dateset](https://dacon.io/competitions/official/236033/data)
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


## 😃 Result
- **Public score** 1st 3.16772 | **Private score** 4th 7.65751
- https://dacon.io/competitions/official/236033/overview/description

## 📖 Reference
CTGAN  
https://arxiv.org/abs/1907.00503  
https://github.com/sdv-dev/CTGAN  

생육환경  
https://scienceon.kisti.re.kr/srch/selectPORSrchArticle.do?cn=NPAP08069532&dbt=NPAP

===========================================================================

상추의 생육 환경 데이터(0일~27일치)를 바탕으로 전처리와 피처 엔지니어링을 통해 예측 모델을 학습시켜 먼저 예측 모델의 성능을 publice score 1등으로 끌어올렸습니다. 

예측 모델의 정확도를 올린 후 생성 모델(CTGAN)을 통해 가짜 환경 데이터를 만든 후 학습 시켰던 예측 모델로 예측을 진행하였습니다.

예측 모델의 정확도가 public score 상 1등이었기 때문에 가짜 환경 데이터에 대한 예측값은 신뢰할 수 있는 데이터라 판단하였고 그 후 주최사인 KIST에 최적의 생육환경을 제시하기 위한 Flow를 생각해야 했습니다. 

먼저, KIST 연구원분들은 각종 생육 환경 관련 논문을 바탕으로 실험을 해보았을 것이라는 전제를 바탕으로 저희만의 unique한 생육 환경을 제시해보자 판단하였고, Feature Engineering을 진행하며 중요한 데이터들을 알아냈었고 최저 잎 중량이었던 환경 데이터들을 직접 조작하여 생성 모델에 학습시킨 후 가짜 환경 데이터를 예측 모델이 예측하여 최저 잎 중량에서 최대 잎 중량을 도출하였습니다.

그렇게 최종 2등으로 수상하였습니다.
