# Upsatage AILab 2 : 6조 

## Team organization

| ![박혜민](https://avatars.githubusercontent.com/u/156163982?v=4) | ![김민지](https://avatars.githubusercontent.com/u/156163982?v=4) | ![김도후](https://avatars.githubusercontent.com/u/156163982?v=4) | ![민경태](https://avatars.githubusercontent.com/u/156163982?v=4) |
| :--------------------------------------------------------------: | :--------------------------------------------------------------: | :--------------------------------------------------------------: | :--------------------------------------------------------------: |
|            [박혜민](https://github.com/BusyBee0828)             |            [김민지](https://github.com/minji919kim)             |            [김도후](https://github.com/kimdohoo1102)             |            [민경태](https://github.com/starcltae)             |
|                            팀장, 담당 역할                             |                            담당 역할                             |                            담당 역할                             |                            담당 역할                             |

## 1. Competiton Info

### Overview

- House Price Prediction
- 주어진 데이터를 활용하여 서울의 아파트 실거래가를 효과적으로 예측하는 모델을 개발하는 경진대회


### Timeline

- March 21, 2024 - Start Date
- April 1, 2024 - Final submission deadline

### Evaluation

- RMSE(Root Mean Squared Error) 

## 2. Components

### Directory

- _Insert your directory structure_

## 3. Data descrption

- 대회에서 제공된 데이터셋을 기반으로 모델을 학습하고, 서울시 각 지역의 아파트 매매 실거래가를 예측
- 제공된 데이터셋
    - 국토교통부에서 제공하는 아파트 실거래가 데이터 : 위치, 크기, 건축년도, 주변 시설 및 교통 편의성과 같은 다양한 특징들을 포함
    - 추가데이터 : 지하철역, 버스정류장 데이터 포함
    - train set: 2007.01 ~ 2023.06
    - test set: 2023.07 ~ 2023.09

### Dataset overview

- ![image](https://github.com/UpstageAILab2/upstage-ml-regression-6/assets/139244450/95a5d85e-f552-44b4-b583-4f85c04f5655)


### EDA
- 데이터가 출처가 다른 2개를 outer join으로 합쳐져서 제공된 것으로 추정
    - 출처별로 데이터프레임을 분리하여 각각 예측을 수행
- 예측하고자 하는 ‘target(가격)’은 시계열데이터
    - 트리모델 이외 LSTM, Moving Average 등의 방법 시도

### Feature engineering

- **‘Target’(가격) 관련  Feature**
    - 평가 방법인 RMSE 계산 수식상 test data에 있는 고가격대 주택을 잘 예측하는 것이 중요
    - 가격이 비싼 아파트를 구분하는 feature 생성
        - ‘top_5_pct’ :  ‘target’값 중 상위 5%에 해당하는 데이터
        - ‘luxury_apt’ : ‘동+아파트명’을 기준으로 2023년 평균 거래가격이 20억원 이상인 데이터
        - ‘전용면적’ : 가격과 높은 상관관계가 있어 역시 중요
- **위치 관련 Feature**
    - 크롤링으롤 X좌표, Y좌표 결측치를 채워서 ‘주소’피처를 새롭게 생성
- **건물 관련 Feature**
    - 건축년도 보다는 계약시점의 건물나이를 계산하는 feature 생성
        - ‘apt_age’ = ‘계약년도’ - ‘건축년도’
    - 아파트 면적 관련 중복칼럼 삭제
        - 개별세대가 아닌 단지 전체면적에 대한 정보는 1개의 피처만 선별하여 사용
- **기타**
    - 직전 거래 날짜 & 간격차이  Feature
        - 이전 거래의 가격이 현재의 가격을 얼마나 잘 설명하는지
    - 그외 불필요하다고 판단되는 feature 제거
        - Permutation Importance
        - RFECV(Recursive Feature Elimination with Cross-Validation)

## 4. Modeling

### Model descrition

- ![image](https://github.com/UpstageAILab2/upstage-ml-regression-6/assets/139244450/b3c2895b-f570-44e7-a4b2-8badccea7095)


### Modeling Process

- _Write model train and test process with capture_

## 5. Result

### Leader Board

- _![image](https://github.com/UpstageAILab2/upstage-ml-regression-6/assets/139244450/24dcbd76-83c1-42a9-8849-8785655bbd4d)
_
- 최종순위: 5위(RMSE:13331.0750)

### Presentation

- [ML_6조_발표자료(pdf) link](https://drive.google.com/drive/folders/1r0iW8JdaNZWcQWv_hv5Qm-K1yybsqAZ_)

## etc

### Meeting Log

- _Insert your meeting log link like Notion or Google Docs_

### Reference

- _Insert related reference_
