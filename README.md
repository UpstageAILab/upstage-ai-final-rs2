[![Review Assignment Due Date](https://classroom.github.com/assets/deadline-readme-button-24ddc0f5d75046c5622901739e7c5dd533143b0c8e959d652212380cedb1ea36.svg)](https://classroom.github.com/a/nDCOQnZo)


# Title (Please modify the title)
## Team

| ![박성우 사진](https://github.com/UpstageAILab/upstage-ai-final-rs2/assets/138054658/01a46263-0c8d-4847-b850-6d598e4bb624) | ![노균호](https://avatars.githubusercontent.com/u/156163982?v=4) | ![윤수인](https://avatars.githubusercontent.com/u/156163982?v=4) | ![조예람](https://avatars.githubusercontent.com/u/156163982?v=4) |
| :--------------------------------------------------------------: | :--------------------------------------------------------------: | :--------------------------------------------------------------: | :--------------------------------------------------------------: |
|            [박성우](https://github.com/UpstageAILab)             |            [노균호](https://github.com/UpstageAILab)             |            [윤수인](https://github.com/UpstageAILab)             |            [조예람](https://github.com/UpstageAILab)             |
|                         팀장, EDA, Modeling, Ensemble                          |                         EDA, Modeling                   |                        EDA, Modeling                          |                            EDA, Modeling, Ensemble               |

## 0. Overview
### Environment
- _Write Development environment_

### Requirements
- _Write Requirements_

## 1. Competiton Info

### Overview

- 'Commerce Behavior Purchase Prediction' 대회는 사용자의 과거 쇼핑 패턴을 분석하여 미래(next one week)에 사용자가 구매할 상품을 추천하는 태스크의 RecSys 대회입니다. 하는 것을 목적으로 합니다. 추천 시스템은 수많은 제품 중에서 적합한 제품을 찾는 데 어려움을 겪는 사용자들에게, 추천 시스템은 개인의 쇼핑 습관, 관심사, 과거 구매 이력 등을 분석해 맞춤형 상품을 추천할 수 있습니다. 따라서, 이커머스 분야에서 추천 시스템은 사용자의 취향을 분석하여 알맞은 상품을 추천함으로써 사용자의 경험을 증진하고 기업의 매출 향상에 도움을 줄 수 있습니다. 이커머스 추천 시스템을 구축하기 위한 알맞은 데이터 전처리 작업에서부터 시작하여, 목적에 맞는 모델을 선택하고, PyTorch 및 기존 라이브러리를 활용하여 모델을 구축하고, Feature Engineering 및 예측을 수행하는 전반적인 과정을 수행하였으며, 평가 지표에 최적화된 파이프라인을 개발하였습니다.

### Timeline

- 2024년 3월 8일 ~ 5월 2일

## 2. Components

### Directory

- _Insert your directory structure_

e.g.
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
- 유저와 아이템 id, 사용자의 세션 id, event time 및 type, 아이테 카테코리 분류 코드, 브랜드, 가격 등의 columns로 구성되어 있음
- 유저가 특정 아이템을 조회/장바구니 담기/구매 하는 등의 데이터와 함께 아이템의 브랜드 및 가격 등이 기록되어 있음 

#### 2) 평가 데이터
- 2020년 3월 1일 ~ 20년 3월 7일, 일주일 간의 온라인 스토어 유저의 행동 데이터 6,382,570 rows
- 해당 기간 동안 아이템을 구입한 모든 유저에 대해서 10개의 아이템을 예측해야함

### EDA

- _Describe your EDA process and step-by-step conclusion_

### Data Processing

- _Describe data processing process (e.g. Data Labeling, Data Cleaning..)_

## 4. Modeling

### Model descrition

- _Write model information and why your select this model_

### Modeling Process

- _Write model train and test process with capture_

## 5. Result

### Leader Board

- _Insert Leader Board Capture_
- _Write rank and score_

### Presentation

- _Insert your presentaion file(pdf) link_

## etc

### Meeting Log

- 매주 월/수/금요일 오후 2시 미팅 진행(총 14회)
- zoom, slack, Google meet 활용

### Reference

- _Insert related reference_

