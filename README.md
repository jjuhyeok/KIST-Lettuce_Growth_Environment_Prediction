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

