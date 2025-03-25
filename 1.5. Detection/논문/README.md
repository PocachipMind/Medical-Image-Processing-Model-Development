# nnDetection: A Self-configuring Method for Medical Object Detection

https://arxiv.org/abs/2106.00817


## Introduction

- Object Detection : Localization & categorization의 문제를 동시에 풀어야함.
- Segmentation의 경우 annotation의 획득 시간에 많은 시간소요
- 정확한 평가를 위해서 개별적인 post-processing이 필요.
- 이러한 반복들을 피할 수 없을까?

![image](https://github.com/user-attachments/assets/e232fdd9-9f66-40e4-9f93-80558359edef)


## Realted work 

- Unet처럼 segmentation의 방법과 달리 detection의 방법은 많은 변수들이 있음.
  - Positive patch, Anchor box , NMS등..
  - 이러한 방법들은 오히려 많은 시간이 소요가 되어짐.
- 반복적인 작업과 처리를 피하기 위해서 자동화를 할 수 있도록 제안함.
- 자동화를 바탕으로 10개의 dataset에서 SOTA를 달성함.

- nnu-net: a self-configuring method for deep learning-based biomedical image segmentation

![image](https://github.com/user-attachments/assets/d03634e6-0df5-42cc-8641-6c6df9920d43)

- AutoML vs nnUnet
  - AutoML의 경우 Neural Architecture Search (NAS)처럼 network를 구성함. 
  - 반면 nnUnet의 경우 학습에 관여하는 loss, metric, preprocessing을 조절


--------


- Annotation과 image만으로 좋은 Network를 자동적으로 학습하도록 구성되어짐.
  - 이를 통해서 데이터마다 모델 구성과 최적의 변수를 찾는 시간이 단축이 됨.
- Fixed parameter (Blue)
  - 모델이 학습이 되어질때 고정이 되어지는 변수
- Rule-Based parameter (Green) 
      - data에 의하여 사용되어지는 함수
- Empirical parameter (Orange)
  - 자동적으로 적용되어지는 방법
 
![image](https://github.com/user-attachments/assets/caff698f-beb0-433e-9c7f-73b0a04a2d2d)

- Fixed parameter 
  - Optimizer : poly learning rate
  - Loss function : Dice + cross entropy
  - Network : Unet
  - Augmentation 
  - Rotate, scale, blur, etc…
  - Inference method : sliding window
  - Epoch
 
![image](https://github.com/user-attachments/assets/1a7a273c-aaf3-4ebe-bf64-dbaa782036e4)


- Rule-Based parameter
  - GPU가 최소 2개의 batch로 학습될수 있도록 설정
  - MRI 또는 CT에 따라 normalize의 방법다름.
  - 들어오는 이미지에 pixel spacing을 똑같이 만들어줌.
  - Batch, Patch size의 경우 Domain에 따라 다르게 적용
 
![image](https://github.com/user-attachments/assets/ba87736d-b03d-4f32-9cea-965b60e340ac)

- Realted work 
  - 경험적 Parameter 
  - Cross validation의 performance가 향상되는가?
  - 2D, 3D모델중에 어떠한 network가 성능이 더 좋은가?
  - Network에 대한 앙상블 진행

![image](https://github.com/user-attachments/assets/94ed32fa-9584-44fd-bc01-4da339aab385)

![image](https://github.com/user-attachments/assets/72bdf722-501d-4477-804d-d5159069f554)

- 모든 데이터에 대해서 SOTA달성

![image](https://github.com/user-attachments/assets/2ee5bc8c-c320-47ab-b813-e3515044a7cc)

## Method

- nnDetection Development
  - 자동적으로 medical object detection의 3가지의 type으로 접근을 하였음.
  - Fixed parameter
  - Rule-Based Parameter
  - Empirical Parameter
![image](https://github.com/user-attachments/assets/72f91727-6ed7-4e0f-875c-6b36d26ade35)

- nnDetection Development
  - 자동적으로 medical object detection의 3가지의 type으로 접근을 하였음.
- Fixed parameter (Blue) 
- 모델이 학습이 되어질때 고정이 되어지는 변수
- Rule-Based parameter (Green) 
  - data에 의하여 사용되어지는 함수
- Empirical parameter (Orange)
  - 자동적으로 적용되어지는 방법
 
![image](https://github.com/user-attachments/assets/e13a5eee-4269-4628-9c90-3a7f5aff727c)

- Fixed parameter
  - Loss function , Optimizer
    - Hard negative mining : positive(1/3), negative(2/3)
    - CE loss & Generalized IOU loss
    - SGD, 60 epoch
  - Network
![image](https://github.com/user-attachments/assets/8a0c6492-0084-4de5-900a-f5dd52512af2)

![image](https://github.com/user-attachments/assets/8e5600c3-6beb-4092-9615-44388903ebdb)


- Rule-base parameter
  - heuristic rules를 기반하여 설정
  - Image domain마다 resampling의 기법이 다름.
  - 고 해상도의 모델은 context가 못찾을 때 저 해상도의 모델로 변경됨.
  - Anchor box를 찾아줌.
  - 반본적으로 IOU가 최대값일 때로 적용
 
![image](https://github.com/user-attachments/assets/adfa7c50-cd88-4c44-96df-0c9481091851)



- Empirical Parameters
  - Post-processing의 과정에 해당하는 부분
  - Non-maximum Suppression (NMS)의 경우 GPU메모리 제한을 피하기 위해 sliding window를 적용
  - Weighted Box Clustering를 적용

![image](https://github.com/user-attachments/assets/d4011744-75ed-4b05-9784-48f5d2d88587)

- Give New data
  - 새로운 데이터가 들어왔을 때 image의 modality마다 다르게 전처리가 자동을 되어진다.
  - 이때 5-fold의 데이터를 생성함.
  - 최종적으로 교차검증들을 앙상블하여 최종 평가 나옴
 
![image](https://github.com/user-attachments/assets/829c27d6-22e0-4dce-b32f-d8d954843213)

## Result
- Experiments
  - 13개의 데이터 셋과 제안한 방법간의 성능 비교 분석을 진행함.
  - FROC와 Mean Average Precision (mAP)에 따른 성능 비교를 진행.
 
![image](https://github.com/user-attachments/assets/204993b1-68c3-425a-9645-348ffdb70fd3)

- 여러 domain(brain, Lung, Rib, Kidney)에서 우수한 성능 달성.
  - Segmentation과도 비교와 해본결과도 우수함.
- 40%의 테스트 데이터에 셋에 대해서도 높은 성능이 유지됨을 볼 수 있음.

![image](https://github.com/user-attachments/assets/4d2d1a62-2089-43a9-a1b9-b3eedc47dfab)

정성적인 평가
• small object에 대해서도 뛰어난 성능을 보여줌

![image](https://github.com/user-attachments/assets/2a842834-b426-4d46-a5e6-d979d3139290)

## Conclusion
- Discussion & Future
  - 모든 데이터셋에 대해서 SOTA를 찍은건 아님
  - 하지만 7개의 데이터셋은 기존의 방법과 상당한 차이를 보여주었음.
  - Detection의 경우도 자동적으로 성능을 최적화 할 수 있는 tool를 공개.
  - 코드의 custom이 어려움.
