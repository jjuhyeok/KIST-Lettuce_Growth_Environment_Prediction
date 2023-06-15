# KIST_Lettuce-Growth-Environment-Prediction  [(Link)](https://dacon.io/competitions/official/236033/overview/description)

## 😃 Result
- **Public score** 1st 3.16772 | **Private score** 4th 7.65751 | **최종 2등**

주최 : KIST

주관 : DACON

규모 : 약 800여명 참가

# 상추의 생육 환경 생성 AI 경진대회


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
