# Classification and Regression

## Classification
- image classification은 2가지 type으로 분류
  - Category label ( Classification )
  - Continuous value ( Regression )
 
- Machine learning(ML)의 경우
  - Wavelet frame transform, Fuzzy C-means

 ### ML Feature extractor 

 - 기존 feature를 classification 하는 방법
   - 나이브 베이즈 ( Naive Bayes )
   - 의사결정트리 ( Decision Trees )
   - 선형 분류 ( Linear classification )
   - 최근접 이웃 ( K-Nearest Neighbors - KNN )
   - 서포트 백터 머신 ( Support Vector Machines - SVM )

### Deep learning을 활용한 Classification

- Challenges
  - Limited data → Fine tuning
  - Large data → Crop
  - Demographic score → Multi label ( Regression )

<img src="https://github.com/user-attachments/assets/4410fa34-7298-4faf-8f54-95e710e52228" width="60%" height="60%"/>

- 이미지 분류
  - 전체 이미지 입력
  - Batch size 한계 존재
- 병변 분류 
  - 해당 영역을 Cropping
  - Multi scale를 이용하여 병변 분류

- Classifiaction에는 3가지 task 존재
  - Binary classification
    - 질병 유무 분류
    - ex ) MRI : 알츠하이머 병 진단 - T,F
  - Multi label classification
    - 질병 타입 분류
    - Softmax 적용
    - ex ) Lung CT - Normal, Emphysema, Ground glass, Fibrosis
  - Multi class classification
    - 한개의 이미지에 중복된 label 있는 경우
    - ex ) Sigmoid를 사용
    - 
- Medical image classification trick
  - Many augmentation
  - Large batch data
  - Learning rate
  - Other model
 
- Binary cross entropy : 특정 질병의 유무를 판단하기 위한 Loss
<img src="https://github.com/user-attachments/assets/14c4216d-a0ae-4b61-a8cb-69a7bdcd02bb" width="30%" height="30%"/>

- Cross entropy : 다중 Class일떄 사용하며 label과 prediction의 확률 분포 차이를 계산
<img src="https://github.com/user-attachments/assets/a22be743-4fe9-4f61-bbb6-85bb0223111e" width="30%" height="30%"/>

- Kullback-Leibler divergence loss : 서로 다른 두 분포의 차이를 측정함
<img src="https://github.com/user-attachments/assets/d57bb704-1406-4071-b033-ef5b19040449" width="30%" height="30%"/>


## Regression

같은 질병이라도 심각도에 따라 다름

Classification의 경우 Class를 나누지만 Regression의 경우 연속적인 값을 가짐
<img src="https://github.com/user-attachments/assets/4b3c4fad-a0e4-4ff5-adf2-288b28e831df" width="60%" height="60%"/>

- 과거 image regression method
  - Decision Tree Regression 
    - Dataset을 작은 단위로 나누어서
  - Random Forest Regression 
    - 여러개의 Decision tree를 만드는 방법
    - 앙상블할떄 Bagging, Boosting방법을 사용
  - Gradient Boosting
    - decision Tree를 조합해서 사용하는 Ensemble 기법
    - XGBoost : Regression, Classification 사용 가능
   
- Medical image regression trick
  - K fold cross validation
  - imbalanced data
  - Augmentation ( SMOTE )

- ex Diabetic retinopathy (DR) : 망막의 혈관을 손상시키는 당뇨병의 합병증, Lung CT

<img src="https://github.com/user-attachments/assets/9a500fb2-a276-4be4-8797-14181fcad6c3" width="60%" height="60%"/>
<img src="https://github.com/user-attachments/assets/ea1b851d-5c94-4a54-9566-271ffe512993" width="20%" height="20%"/>

 
- L1loss
  - 실제값과 예측값의 차이값에 오차합을 최소화 하기 위해사용
  - 미분이 안되는 지점이 존재 (0인 지점)
  - 오차값에 대한 Robustness하다는 점이 있음.
  - <img src="https://github.com/user-attachments/assets/d8c7ef5e-2563-42b9-84dd-39d58cfb9842" width="30%" height="30%"/>

- L2loss
  - 실제값과 예측값의 제곱의 차이
  - 안정적인 미분 가능 하지만 이상치에 민감하게 반응
  - Stability하다는 장점이 있음
  - <img src="https://github.com/user-attachments/assets/0f7dcf11-acd1-40a6-97f3-21883291d7de" width="30%" height="30%"/>

- Huber loss, Smooth L1 loss
  - 모든 지점에서 미분이 가능
  - Outlier에 robust
  - <img src="https://github.com/user-attachments/assets/758e12e0-087e-4ce2-8fd9-384e3bac002e" width="30%" height="30%"/>
  - <img src="https://github.com/user-attachments/assets/e622e500-9a83-49bc-961a-48f28bf37507" width="30%" height="30%"/>

## Evaluation

https://89douner.tistory.com/253

예측이 맞냐 틀리냐 : T, F
어떻게 예측 했느냐 : P, N

- True Positive(TP) : 실제로 positive인데, 모델의 예측값도 Positive일 때
- False Positive(FP) : 실제로 Negative인데, 모델의 예측값은 Positive일 때
- False Negative(FN) : 실제로 Positive인데, 모델의 예측값은 Negative일 때
- True Negative(TN) : 실제로 Negative인데, 모델의 예측값도 Negative일 때


- Accuracy
  - 모델이 바르게 예측을 한 결과
![image](https://github.com/user-attachments/assets/01c43b01-933a-4273-93b7-f35df062a201)

- Recall (재현도)
  - 실제값이 positive인 것 중에 model 이 positive라고 한 비율
![image](https://github.com/user-attachments/assets/95436b0f-4346-4170-9a56-d066705837dd)

- Precision (정밀도)
  - 모델이 positive라고 예측한 것 중에 실제값이 positive일 경우
![image](https://github.com/user-attachments/assets/d643cda7-8a30-422c-8fb5-09abb3675dcb)
