# 팀명 : 뉴럴링크 

● 팀장 : 정재연
● 팀원 : 박주연, 양태성, 이도훈, 임나연 

![프로필](https://github.com/TaeseongYang/Loan_product_BI/assets/156265617/6c0b6d4c-affa-4b7d-af9c-1414700c0963)


---

# 프로젝트 주제 : 고객별 대출 등급 예측과 재정 안정성을 위한 대출 상품 제안 

**<기획 의도>**

주 목적은 금융 고객의 대출등급을 정확히 예측하는 것입니다. 이를 통해 금융 기관은 개인화된 대출 상품을 제공하고, 대출 위험 관리를 보다 효율적으로 수행할 수 있도록 지원합니다. 또한, 대출 상품의 조건을 더 정확하게 설정하여 고객 만족도를 향상시킬 수 있습니다. 

**<주요 분석 내용 및 구체적 방법 설정>**

1. 데이터 전처리 단계
  - 결측치 처리와 범주형 데이터 인코딩을 수행

2. 기본 통계 분석 및 상관관계 분석
  - 각 변수들의 기본적인 상관관계 분석을 통해 주요 변수들 간의 상호작용과 영향력을 파악, 또한 어떤 변수가 대출금액 및 기간에 영향을 미치는지 파악

3. 특성 선택과 피처 엔지니어링
  - 주요 변수들을 선택하고 필요에 따라 새로운 특성을 생성

4. 다양한 예측 모델을 개발 및 비교 :
  - Random Forest, Logistic Legression, Gradient Boosting 등이 포함되고, 각 모델의 성능을 최적화하고 비교하여 최적의 모델을 선택
  - 모델의 성능 평가를 위해 Kfold를 통한 교차 검증을 사용하고 f1_macro를 이용하여 모델을 성능을 평가

5. X-AI를 통한 해석
  - 어떤 요인들이 어떤 등급을 결정짓는데 양의 영향을 끼치는지 음의 영향을 끼치는지 시각화를 통해 해석

**<기대 효과 및 모델의 가치>**

1. 이 프로젝트를 통해 고객에게 맞춤형 대출 상품을 제안함으롰 고객의 만족도와 충성도를 높임
2. 대출 위험을 예측하고 관리함으로써 금융기관의 리스크를 줄임
3. 정확한 대출 조건의 예측은 금융 기관의 운영 효율성을 증가시키며, 잠재적인 손실을 줄이는 데 기여
4. 자동화를 통한 시간 효율 극대화
5. 기존 대출 가능 잠재 고객 발굴 가능

---

# Solution

![KakaoTalk_20240123_143845604](https://github.com/TaeseongYang/Loan_product_BI/assets/156265617/8249cd42-6d86-4a47-84da-d19477b44799)

||점수|월별이자부담|
|------|---|---|
|Altman_Z_Score|1.0000|-0.20657|
|월별이자부담|-0.20657|1.0000|

**높은 이자율은 고객의 폐업률을 높임**

=> 'Altman_Z_Score'와 '월별이자부담' 가중치를 부여하여 대출 등급과 상환률에 따른 이자율 감면 상품을 제안 

![image](https://github.com/TaeseongYang/Loan_product_BI/assets/156265617/b05d4078-4e5c-46d8-a94c-98fe463e6b34)

**EDA 결과 낮은 대출 등급의 고객들이 감면 받는 경우가 다수를 차지**
- 이자율 감면 상품의 경우에는 낮은 등급의 고객이 감면되는 경우가 다수를 차지하기 때문에 이자율 감면만을 노리는 고객으로 인해 기업의 재정 건정성을 악화시킬 수 있다는 단점도 존재할 수 있음
- 다만, 이는 'Altman_Z_Score'에 존재하는 '상환률'의 가중치를 높여 상환률이 높은 고객에 한해서 이자율 감면 혜택이 갈 수 있도록 설정
