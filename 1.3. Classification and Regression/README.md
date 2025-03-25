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
 
![image](https://github.com/user-attachments/assets/4410fa34-7298-4faf-8f54-95e710e52228)

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
- Cross entropy : 다중 Class일떄 사용하며 label과 prediction의 확률 분포 차이를 계산
- Kullback-Leibler divergence loss : 서로 다른 두 분포의 차이를 측정함

## Regression

같은 질병이라도 심각도에 따라 다름

Classification의 경우 Class를 나누지만 Regression의 경우 연속적인 값을 가짐
![image](https://github.com/user-attachments/assets/4b3c4fad-a0e4-4ff5-adf2-288b28e831df)

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
![image](https://github.com/user-attachments/assets/9a500fb2-a276-4be4-8797-14181fcad6c3)
![image](https://github.com/user-attachments/assets/ea1b851d-5c94-4a54-9566-271ffe512993)

- 
