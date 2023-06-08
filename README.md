# 웹소설 성공 예측 AI 프로그램
###  📃 소개
#### 최근 모바일 기술 발달 및 쉽고 가벼운 콘텐츠를 선호하는 경향이 강해지면서 웹소설에 관한 관심은 지속적으로 높아지고 있다. 
#### 시장조사전문기업 엠브레인 트렌드모니터가  2022년 7월 28일 ~ 8월 1일  동안 전국 만 19~59세 성인 남녀 1,000명을 대상으로 웹소설 관련 U&A 조사를 실시한 결과, 모바일 기술 발달 및 쉽고 가벼운 콘텐츠를 선호하는 경향이 강해지며  웹소설 시장의 전망이 비교적 높게 평가되고 있는 것으로 조사되었다.  
###### 출처 : 매드타임스(MADTimes)(http://www.madtimes.org)
#### 웹툰에 관한 관심이 많아지면서 웹소설에 도전하는 작가는 증가하고 매번 작품이 새로 등장한다. 그렇다면 그 많은 웹소설 중 어느 것이 정식 데뷔가 확정되고 어느 작품은 여전히 아마추어 작품으로 머물러 있을까? 그리고 웹소설의 성공 요인은 무엇인가?
#### 이를 판단할 수 있다면 웹소설 시장에 도전하는 작가에게도 그리고 작가를 뽑는 웹소설 플랫폼에도 유의미한 결과를 줄 것 같으나, 이에 관해 분석 요인에 관하여 분석한 결과나 AI 관련 연구 사례는 존재하지 않는다. 따라서 본 연구에서는 웹소설 성공 예측할 수 있는 AI 연구를 진행해보고자 한다.
  ---  
### 🛠 기능 요약
1. 성공 예측 모델은 **RandomForest, SVM, Gradient Boosting, LGBM, XGBoost** 5개의 모델을 사용하였다. 
과적합을 방지하기 위해 5-fold 교차 검증을 진행하였고, 각 모델이 갖고 있는 하이퍼 파라미터의 일부를 Grid Search를 통해 최적화하여 가장 성능이 높았던 파라미터를 최종 모델의 파라미터로 선정하였다. 
전체 데이터셋는 8:2의 비율로 훈련 데이터과 테스트 데이터로 분할하여 모델을 학습시켰고, 이때 종속 변수인 성공 여부의 비율을 고려하여 균등 분할하였다. 
학습된 모델은 검증 데이터셋을 사용하여 정확도를 평가하였고, 최종 모델의 성능은 테스트 데이터셋을 사용하여 평가하였다.
2. [KoAlpaca-Polyglot-5.8B](https://huggingface.co/beomi/KoAlpaca-Polyglot-5.8B) 모델을 활용하여 소설 창작에 대한 모델을 구축해보았다. 
GPU 문제를 극복하기 위해 [KoAlpaca-Polyglot-5.8B](https://huggingface.co/beomi/KoAlpaca-Polyglot-5.8B)모델을 활용하여 파인튜닝 작업을 실시해 [KoAlpaca-Polyglot-12.8B](https://huggingface.co/beomi/KoAlpaca-Polyglot-12.8B) 모델과 기능적으로 유사하게 동작하도록 하였다.
구축한 소설 데이터 중 소설의 본문과 장르 정보를 선택헤 데이터를 구성하였으며, 토큰화, 정제 및 문장 분리 등의 과정을 거쳐 데이터의 품질을 향상시켰다. 
학습에는 다양한 장르의 소설 데이터를 사용하였으며, 효과적인 파인튜닝을 위해 적절한 학습 전략을 적용하였다. 
이때, GPU 부족 문제를 해결하기 위해 본문 글자 수를 10000자로 제한하였다. 
파인튜닝을 위해 DataSet을 'instruction': df['novel'], 'output': df['genre'], DatasetDict을 'train': dataset 형태로 가공하였다. 
이후 입력 시퀀스를 모델의 입력 크기인에 맞게 조정 후 학습을 진행하였다.
###### 참고 : KoAlpaca: Korean Alpaca Model based on Stanford Alpaca (feat. LLAMA and Polyglot-ko) https://github.com/Beomi/KoAlpaca
---
### ⏰ 개발 기간
2023년 3월 22일 ~ 2023년 06월 05일  
---
### 👩‍💻 멤버 구성
- 김민수 
- 김은비
- 여언주
- 황서진  
---
### 📌 Files
- Data
  - `BN_final.xlsx` raw data best novel
  - `CN_final.xlsx` raw data challenge novel
  - `novel_final.csv` preprocessed data
  - `novel_genre.csv` novel&genre data for KoAlpaca
  - `네이버_소설_크롤링.ipynb` Crawling code
  - `데이터 전처리.ipynb` Data Preprocessing code

- EDA
    - `분석(별점,조회수,관심수,댓글수,리뷰수).docx` Analysis File
    - `분석(장르,글자수,업로드간격).ipynb` Analysis File
    
- ML   
    - `ML modeling.ipynb` modeling - RandomForest, SVM, Gradient Boosting, LGBM, XGBoost

- NLP
    - `ChatGPT.ipynb` modeling - ChatGPT
    - `Koalpaca.ipynb` modeling - KoAlpaca
