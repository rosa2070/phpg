* 인공지능
    -정의
        - 튜링 테스트(turing test)는 인간의 것과 동등하거나 구별할 수 없는$$ 지능적인 행동을 보여주는 기계의 능력에 대한 테스트
        - 인간이 판단했을때 그럴싸한 지능
    * 머신러닝
        - 처리된 데이터가 증가될수록 학습$$ 효과가 더 있어야 한다.
        - 만약 컴퓨터 프로그램이 특정한 태스크 T를 수행할 때 성능 P 만큼 개선되는 경험 E를 보이면 그 컴퓨터 프로그램은 태스크와 성능 P에 대해 경험 E를 학습했다라고 할 수 있다 [카네기 멜론, 톰미셀]
        * 딥러닝
            - 처리데이터 증가에 따라 효율이 증가-> 학습효과

        * 머신러닝
            - 지도학습: 전문가가 데이터를 주고(라벨링) 모방하게 하는
                - 회귀
                    - 순서에 흐름에 따른 추정
                        - 회귀
                        - 각종 머신러닝 기법의 회귀 
                - 분류
                    - 구별
                        - 로지스틱회귀
                        - 나이브베이즈 조건부 확률정리기반 머신러닝
                        - KNN 최근접이웃
                        - SVM 서포트벡터머신
                        - DT 결정트리 Decision Tree
                        - RF[앙상블] 랜덤포리스트

            - 비지도 학습: 전문가의 지도(라벨링)가 없는 상태에서 다양한 계산에 의해 학습을 하는 방법
                - 군집?
                - 패턴?
                - 차원축소? 
        * 딥러닝
            - NN을 본딴 알고리즘(퍼셉트론)으로 만들었는가?
            - 범용 AI

        * MSE 에러함수

* 머신러닝 방법
    - EDA(Exploratory Data Analysis, 탐색적 데이터 분석)
        - 데이터 전처리
        - 데이터 성질 : info()
        - 기초 통계량 : describe()
            * 분포
                - 정규분포하는가?
                - 통계처리가 가능한가?
        - 시각화
            - 직관적 처리 방법
                - 히스토그램 .hist()
                - 산점도 .plot.scatter()
                - 고급 시각화 seaborn
            - 데이터 전처리 방향

    - 머신러닝
        - 모델선정
            - 시각화 기반으로 분리가 일어나는가
        - 학습용데이터 만들기
            - 데이터로부터 train(학습)데이터와
            - test (시험)데이터로 분리 
        - 모델
            - KNN
            - SVM
            - DT
            - RF * - DT 배깅모델
            - GB

        - 배깅과 부스팅
            - 배깅 - 병렬처리
            - 부스팅 - 순차처리
    - 평가지표
        - 정확도 Accuracy 일반적 성능에 대한 평가지표

            |구분|거짓(N)이라고 예측|참(P)이라고 예측|
            |--|--|--|
            |진짜 거짓(N)|[TN] 거짓이라고 예측한게 맞음 |[FP] 참이아닌데 참이라고 함|
            |진짜 참(P)|[FN] 거짓이 아닌데 거짓이라고함|[TP] 참이라고 예측한게 잠음|

        - 정밀도(Precision)
            * 예측기반
                - P로 예측한값이 일치 (TP)/(FP+TP) P로 예측한것들
        - 재현율(Recall)
            * 실제값 불러오기
                - P로 예측한 값이 일치 (TP)/(FN+TP) 실제값이 P인것들
        - 정밀도와 재현율은 트레이드 오프관계에 있다.
            - F1 Score = 2*(정밀도*재현율)/(정밀도+재현율)
        - ROC_AUC커브 ->ROC_AUC_SCORE
            - 모델의 적합성 평가
# AUTOML
    - pycaret ^
# NLP
    - 자연어 처리
    - 말의 구조
        - 책 -챕터 -문단 -문장 -단어 - 형태소* - 음절 -음소 

     나는 네가 못생기고 능력없고 돈도 없고
     그래서 네가 좋아 1 앞선 문장 인정 감성긍정
     그런데 네가 좋아 2 부정적으로 평가하면서 긍정
     그러나 네가 좋아 3 






