[![Review Assignment Due Date](https://classroom.github.com/assets/deadline-readme-button-24ddc0f5d75046c5622901739e7c5dd533143b0c8e959d652212380cedb1ea36.svg)](https://classroom.github.com/a/nDCOQnZo)


# Commerce Purchase Behavior Prediction 상품 구매 예측 및 추천 대회
## Team

| ![박성우 사진](https://github.com/UpstageAILab/upstage-ai-final-rs2/assets/138054658/ccc7c3c1-8af6-4bae-9581-d12c2821542e) | ![노균호](https://github.com/UpstageAILab/upstage-ai-final-rs2/assets/138054658/f3372ca8-ccb1-4e55-b082-eee25c67401e) | ![윤수인](https://github.com/UpstageAILab/upstage-ai-final-rs2/assets/138054658/f3272375-44d9-4d6e-904b-38bd1ad7b935) | ![조예람](https://github.com/UpstageAILab/upstage-ai-final-rs2/assets/138054658/324ea6a8-e391-4fbf-b422-d6545843dccb) |
| :--------------------------------------------------------------: | :--------------------------------------------------------------: | :--------------------------------------------------------------: | :--------------------------------------------------------------: |
|            [박성우](https://github.com/UpstageAILab)             |            [노균호](https://github.com/UpstageAILab)             |            [윤수인](https://github.com/UpstageAILab)             |            [조예람](https://github.com/UpstageAILab)             |
|                         팀장, EDA, Modeling, Ensemble                          |                         EDA, Modeling                   |                        EDA, Modeling                          |                            EDA, Modeling, Ensemble               |

## 0. Overview
### Environment
- Vscode, ssh server(RTX 3090/Ubuntu 20.04.6), pytorch


## 1. Competiton Info

### Overview
![대회 개요](https://github.com/UpstageAILab/upstage-ai-final-rs2/assets/138054658/43f105ad-3d3c-49bf-88a0-8de7e5135a98)

- 'Commerce Behavior Purchase Prediction' 대회는 사용자의 과거 쇼핑 패턴을 분석하여 미래(next one week)에 사용자가 구매할 상품을 추천하는 태스크의 RecSys 대회입니다. 추천 시스템은 수많은 제품 중에서 적합한 제품을 찾는 데 어려움을 겪는 사용자들에게, 추천 시스템은 개인의 쇼핑 습관, 관심사, 과거 구매 이력 등을 분석해 맞춤형 상품을 추천할 수 있습니다. 따라서, 이커머스 분야에서 추천 시스템은 사용자의 취향을 분석하여 알맞은 상품을 추천함으로써 사용자의 경험을 증진하고 기업의 매출 향상에 도움을 줄 수 있습니다. 이커머스 추천 시스템을 구축하기 위한 알맞은 데이터 전처리 작업에서부터 시작하여, 목적에 맞는 모델을 선택하고, PyTorch 및 기존 라이브러리를 활용하여 모델을 구축하고, Feature Engineering 및 예측을 수행하는 전반적인 과정을 수행하였으며, 평가 지표에 최적화된 파이프라인을 개발하였습니다.

### Evaluation Metrix
- 사용자에게 가장 관련성이 높은 아이템들을 추천 리스트 상위에 잘 제공하였는지에 대한 평가지표
- 추천된 아이템 리스트에서 각 아이템의 관련성에 로그 기반의 가중치를 적용하여 계산한 값(DCG)을 가장 이상적인 아이템 추천 상황에서 계산될 수 있는 DCG 값이 IDCG로 정규화
- 본 대회에서는 각 유저 당 아이템 10개를 추첨하기 때문에 NDCG@10 평가지표를 활용하여 모델의 성능을 측정
![평가지표](https://github.com/UpstageAILab/upstage-ai-final-rs2/assets/138054658/51a4b04d-bd18-4fa6-84f1-28a1fd7393fd)

### Timeline

- 2024년 3월 8일 ~ 5월 2일

## 2. Components

### Directory

```
├── code
│   ├── jupyter_notebooks
│   │   └── model_train.ipynb
│   └── train.py
├── docs
│   ├── pdf
│   │   └── (Template) [패스트캠퍼스] Upstage AI Lab 1기_그룹 스터디 .pptx
│   └── paper
└── input
    └── data
        ├── eval
        └── train
```

## 3. Data descrption

### Dataset overview

#### 1) 학습 데이터
- 2019년 11월 1일 ~ 20년 2월 29일, 4개월 여 간의 온라인 스토어 유저의 행동 데이터 8,350,311 rows
- 유저와 아이템 id, 사용자의 세션 id, event time 및 type, 아이템 카테코리 분류 코드, 브랜드, 가격 등의 columns로 구성되어 있음
- 유저가 특정 아이템을 조회/장바구니 담기/구매 하는 등의 데이터와 함께 아이템의 브랜드 및 가격 등이 기록되어 있음 

#### 2) 평가 데이터
- 2020년 3월 1일 ~ 20년 3월 7일, 일주일 간의 온라인 스토어 유저의 행동 데이터 6,382,570 rows
- 해당 기간 동안 아이템을 구입한 모든 유저에 대해서 10개의 아이템을 예측해야함

### EDA

- 사용자는(user_id)는 홈페이지에 들어가 세션(user_session)을 할당받고 특정 아이템(item_id)을 특정 시간(event_time)에 상품(product_id) 장바구니에 추가(event_type = 'cart')하거나 조회(event_type = 'view')하거나 구매(event_type = 'purchase')할 수 있음
- 각 상품 별로 event_time 단위로 카테고리 코드(category_code)와 브랜드(brand), 가격(price)가 주어짐
- event type 간의 비중을 살펴보면 view(99.7%), cart(0.2%), purchase(0.02%)로 view 관련 데이터가 대부분이었으며 뚜렷하게 방문자 수 증가가 소비로 이어지는 등의 패턴을 확인하기 어려웠음
  
  ![일별](https://github.com/UpstageAILab/upstage-ai-final-rs2/assets/138054658/95a25fcb-364d-4432-b4b6-782616e64ca0)

  ![이벤트타입비교](https://github.com/UpstageAILab/upstage-ai-final-rs2/assets/138054658/e982e879-c533-4c2e-9c1f-a80b661ac008)        ![이벤트타입비교2](https://github.com/UpstageAILab/upstage-ai-final-rs2/assets/138054658/6c762078-aadf-4aeb-9849-f71db11df233)

- 가격 분포는 굉장히 넓게 나타났으며 200 달러 내외에 가장 많은 빈도를 보였으며, 반바지가 평균 가격이 비싸고 스카프가 가장 싼 상품으로 확인하였음

 ![가격1](https://github.com/UpstageAILab/upstage-ai-final-rs2/assets/138054658/64c7d413-da38-4f5e-ba95-1dbcb198280c)  ![가격2](https://github.com/UpstageAILab/upstage-ai-final-rs2/assets/138054658/4ba85145-4f04-48a2-84af-7f3ed6890411)

- 고객들의 view, cart, purchase 빈도수가 높은 상품군으로는 신발로 고객들의 관심이 높음을 알 수 있음

![top20](https://github.com/UpstageAILab/upstage-ai-final-rs2/assets/138054658/ca662978-688c-42a1-8db7-1dd1b0767d30)

### Data Processing

- purchase 관련 데이터를 기반으로 User-Item relevance, User-Item Matrix를 만들기 위한 Preprocessing & Feature Engineering을 진행하였음
- XGBoost, LGBM, Implicit, Recbole 등의 라이브러리들을 활용하여 추천 시스템 구축하였음

## 4. Modeling

### Model descrition

- sequential, time data가 매우 풍부했음에도 불구하고 비교적 간단한 모델인 tree-based model들이 높은 성능을 보임임

### Modeling Process

- 베이지안 최적화 방법에 기반한 Hyperopt library를 활용하여 parameter tuning 진행하였음
- 베이지안 최적화는 목적 함수를 최대 혹은 최소로 하는 최적해(Pair-Surrogate 대체 모델을 평가하여 업데이트)를 찾아나가는 방법

![모델결과](https://github.com/UpstageAILab/upstage-ai-final-rs2/assets/138054658/d1d8c02d-0f9a-4bc2-9430-a78c1e79afae)



## 5. Result

### Leader Board

- Private Score 0.1089 -> Public Score 0.1091 (1st Prize!)

### Presentation

- [RecSys 2조.pdf](https://github.com/UpstageAILab/upstage-ai-final-rs2/files/15198368/RecSys.2.pdf)


## etc

### Meeting Log

- 매주 월/수/금요일 오후 2시 미팅 진행(총 14회)
- zoom, slack, Google meet 활용

### Reference

- XGBoost: https://xgboost.readthedocs.io/en/latest/ 
- GRU4Rec: Gru4rec: https://arxiv.org/abs/1606.08117
- BERT4Rec: https://arxiv.org/abs/1904.06690 
- SAS4Rec: https://arxiv.org/abs/1808.09781 

