# 팀명 : 뉴럴링크 

● 팀장 : 정재연

● 팀원 : 박주연, 양태성, 이도훈, 임나연 

![프로필](https://github.com/TaeseongYang/Loan_product_BI/assets/156265617/6c0b6d4c-affa-4b7d-af9c-1414700c0963)


---

# Dacon modeling & analysis project

# </br> <주제>
</br> :pencil2: 큰 주제 : Dacon에서 제공한 데이터를 통해 고객의 대출 등급을 분류하는 모델링 작업 진행

- 세부 주제 : 예측 성능이 높은 모델을 통해 대출 등급이 낮은 고객의 행동 패턴을 분석
- 세부 주제 : 상환률을 높이기 위한 대출 상품을 제안

```
Q. 대출 등급이 낮은 고객의 패턴을 분석한 이유는?
=> 대출의 경우에는 상환률에 따라 금융기관의 재정 건전성에 영향을 미치는데, 대출 등급이 낮은 고객의 경우에 상환률이 낮게 집게 됨. 

Q. 상환률을 높이기 위한 대출 상품의 아이디어는?
=> 상환률과 가장 높은 상관관계를 보이는 feature를 기반으로 하여 대출 상품을 제안.

Q. 궁극적인 목표는?
=> 개인화된 대출 상품을 제공하고, 대출 위험 관리를 보다 효율적으로 수행할 수 있도록 지원.
=> 대출 상품의 조건을 더 정확하게 설정하여 고객 만족도를 향상시킬 수 있음. 
```

# </br> <자료>
</br> :pushpin: 자료 출처 : Dacon

|ID|대출금|대출기간|주택소유상태|연간소득|총계좌수|대출목적|총상환원금|총상환이자|총연체금액|대출등급|
|------|---|------|---|------|---|------|---|------|---|------|
|TRAIN_00000|12480000|36 months|RENT|72000000|15|부채 통합|0|0|0|C|
|TRAIN_00001|14400000|60 months|MORTGAGE|130800000|21|주택 개선|373572|234060|0|B|
|TRAIN_00002|12000000|36 months|MORTGAGE|96000000|14|부채 통합|928644|151944|0|A|
|TRAIN_00003|14400000|36 months|MORTGAGE|132000000|15|부채 통합|325824|153108|0|C|	
|TRAIN_00004|18000000|60 months|RENT|71736000|19|주요 구매|228540|148956|0|B|
  
```
이외에도 부채 대비소득 비율, 연체 금액, 근로기간의 feature들도 존재

대출등급 : A,B,C,D,E,F,G 등급이 존재하며, 높은 등급일수록 신용 점수가 높은 것임
대출기간 : str을 수치형 자료로 변환 
근로기간 : str을 수치형 자료로 변환
주택소유상태 : any를 가장 빈도가 높은 mortage로 변환
```
① 대출 등급에 따른 질적 자료 분석 

- 근로기간

 </br>![image](https://github.com/TaeseongYang/Loan_product_BI/assets/156265617/27081790-a763-437b-9b9a-bcab623795ad)

- 주택소유상태

 </br>![image](https://github.com/TaeseongYang/Loan_product_BI/assets/156265617/5d4b7099-f805-47c7-ad9e-ec48351c51a3)

- 대출목적

 </br>![image](https://github.com/TaeseongYang/Loan_product_BI/assets/156265617/7e7ce39c-f215-47c1-924d-ae5f68941c29)

② 대출 등급에 따른 양적 자료 분석 

- 대출 금액

</br>![image](https://github.com/TaeseongYang/Loan_product_BI/assets/156265617/cf6911df-fd37-4308-b81a-a649740a47a8)

- 대출 기간

 </br>![image](https://github.com/TaeseongYang/Loan_product_BI/assets/156265617/af32c1a3-75e0-40af-bef0-1e6a6d378540)

- 연간 소득

</br>![image](https://github.com/TaeseongYang/Loan_product_BI/assets/156265617/a852dc5d-717e-4a72-a496-334e86bef3fd)

- 부채 대비 소득 비율

</br>![image](https://github.com/TaeseongYang/Loan_product_BI/assets/156265617/abf9d22e-3cc0-4b04-9746-42fb1951f79b)

- 총계좌수

</br>![image](https://github.com/TaeseongYang/Loan_product_BI/assets/156265617/a2b02dbb-ab5c-4755-8546-984a323091fc)

- 최근 2년간 연체 횟수

 </br>![image](https://github.com/TaeseongYang/Loan_product_BI/assets/156265617/a6cdcc2f-43aa-43ff-8538-5f394f849368)

- 총상환원금

 </br>![image](https://github.com/TaeseongYang/Loan_product_BI/assets/156265617/ecc97bf6-ad41-425a-92f5-c9c31e326aeb)

# </br> 모델링링 방법

```
1. 데이터 전처리 단계
=> 결측치 처리와 범주형 데이터 인코딩을 수행

2. 기본 통계 분석 및 상관관계 분석
=> 각 변수들의 기본적인 상관관계 분석을 통해 주요 변수들 간의 상호작용과 영향력을 파악, 또한 어떤 변수가 대출금액 및 기간에 영향을 미치는지 파악

3. 특성 선택과 피처 엔지니어링
=> 주요 변수들을 선택하고 필요에 따라 새로운 특성을 생성

4. 다양한 예측 모델을 개발 및 비교 :
=> Random Forest, Logistic Legression, Gradient Boosting 등이 포함되고, 각 모델의 성능을 최적화하고 비교하여 최적의 모델을 선택
=> 모델의 성능 평가를 위해 Kfold를 통한 교차 검증을 사용하고 f1_macro를 이용하여 모델을 성능을 평가

```
|모델|점수|
|------|---|
|LGBMClassifier|0.9214193067987015|
|CatBoostClassifier|0.902585399277785|
|XGBClassifier|0.9241019412174871|
|VotingClassifier|0.922350214373026|

※ optuna를 통한 각 모델의 하이퍼파라미터를 구했습니다. 

---
# 대출등급이 낮은 고객의 패턴 분석 

![image](https://github.com/TaeseongYang/Loan_product_BI/assets/156265617/1cfc3ba9-e1f0-477a-964d-7dbd4a326339)

```
=> 대출 등급이 가장 낮은 G등급의 고객 중에서도 G등급의 평균 상환률보다도 낮은 상환률을 보이는 고객의 대출목적에 따른 평균 대출 금액을 시각적으로 표현
=> 휴가와 주택개선에서 높은 평균 대출금액 수준을 보임
```

![image](https://github.com/TaeseongYang/Loan_product_BI/assets/156265617/052ab09e-18f9-4f16-9b2c-410ddcdbfecb)

```
=> 대출 등급이 가장 낮은 G등급의 고객 중에서도 G등급의 평균 상환률보도 높은 상환률을 보이는 고객의 대출목적에 따른 평균 대출 금액을 시각적으로 표현
=> 위의 자료와 달리 휴가에서의 대출은 집계되지 않음
=> 대출 등급이 G등급의 고객 중에서 '휴가'를 목적으로 대출을 받는 고객의 경우에는 상환 가능성이 굉장히 낮다는 결론에 도달 
```
![image](https://github.com/TaeseongYang/Loan_product_BI/assets/156265617/d7af18b6-df35-432b-ae7d-4cb71b6c869e)

```
=> G등급 중에서도 상환률이 낮은 그룹에서 휴가를 목적으로 대출을 받는 경우에는 굉장히 낮은 근로기간을 보여줌
=> 근로기간이 낮다는 것은 사회적 경험이 다소 적은 사회 초년생의 가능성이 높기 때문에 사회초년생이 휴가를 목적으로 대출을 받는 경우에 상환률이 낮을 수 있다는 결론에 도달할 수 있게 된다. 
```

---

# 대출등급에 따른 상환률 감면 대출 상품 제안 

![KakaoTalk_20240123_143845604](https://github.com/TaeseongYang/Loan_product_BI/assets/156265617/8249cd42-6d86-4a47-84da-d19477b44799)

||점수|월별이자부담|
|------|---|---|
|Altman_Z_Score|1.0000|-0.20657|
|월별이자부담|-0.20657|1.0000|

**높은 이자율은 고객의 폐업률을 높임**

=> 'Altman_Z_Score'와 '월별이자부담' 가중치를 부여하여 대출 등급과 상환률에 따른 이자율 감면 상품을 제안 

```
def create_loan_product(row):
    # 조건에 따라 감면 대출상품 여부를 결정
    if (row['Altman_Z_Score'] <= np.percentile(loan_product_data['Altman_Z_Score'], 20) and
        row['월별이자부담'] >= np.percentile(loan_product_data['월별이자부담'], 80) and
        row['총상환원금_대비_대출금액비율'] <= np.percentile(loan_product_data['총상환원금_대비_대출금액비율'], 20)and
        row['대출_대비_소득_비율']<=np.percentile(loan_product_data['대출_대비_소득_비율'], 20),
        row['총상환이자_대비_총상환원금']<=np.percentile(loan_product_data['총상환이자_대비_총상환원금'], 20)):
        
        # 감면 대출상품 조건을 만족하는 경우에만 감면률 설정 함수 실행
        # 감면률 설정 함수
        def set_interest_and_reduction_rate(row):
            # 기본 감면률
            base_reduction_rate = 0.5

            # 피처에 대한 가중치
            weights = {'월별이자부담': 0.4, 'Altman_Z_Score': 0.55, '총상환원금_대비_대출금액비율': 0.3}

            # 가중 평균을 통해 피처들을 종합하여 감면률 설정
            weighted_sum = sum(row[feature] * weights[feature] for feature in weights)

            # 등급에 따라 추가 감면률 부여 (등급이 낮을수록 더 많은 감면)
            additional_grade_reduction = max(0, 0.2 * (10 + row['대출등급']))

            # 최종 감면률 계산
            reduction_rate = base_reduction_rate + weighted_sum + additional_grade_reduction

            return reduction_rate

        # 감면률 설정 함수를 실행하고 결과를 반환
        return set_interest_and_reduction_rate(row)
    
    else:
        # 감면 대출상품 조건을 만족하지 않으면 0을 반환
        return 0
```

![image](https://github.com/TaeseongYang/Loan_product_BI/assets/156265617/d631e473-c8ae-42ce-b503-2e367aa3ee39)

```
=> 실제 금융권에서 사용하고 있는 이자율을 가공하여 대출 등급에 따른 이자율 feature를 생성 
=> 대출등급에 따라 감면 감면되는 수준을 확인할 수 있음
```

![image](https://github.com/TaeseongYang/Loan_product_BI/assets/156265617/b05d4078-4e5c-46d8-a94c-98fe463e6b34)

**EDA 결과 낮은 대출 등급의 고객들이 감면 받는 경우가 다수를 차지**
- 이자율 감면 상품의 경우에는 낮은 등급의 고객이 감면되는 경우가 다수를 차지하기 때문에 이자율 감면만을 노리는 고객으로 인해 기업의 재정 건정성을 악화시킬 수 있다는 단점도 존재할 수 있음
- 다만, 이는 'loan_product'에 존재하는 '상환률'의 가중치를 높여 상환률이 높은 고객에 한해서 이자율 감면 혜택이 갈 수 있도록 설정
