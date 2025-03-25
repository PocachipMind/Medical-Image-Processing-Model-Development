# Instance segmentation

- Semantic segmentation & Object detection의 문제를 합침
  - Localization & classification을 동시에 해결하는 방안. 
  - 객체의 class뿐만 아니라 객체의 object mask도 생성
  - Instance간의 경계도 구분이 필요함.

![image](https://github.com/user-attachments/assets/87951ee9-2ec4-4d97-bfda-8f54bd3fea1b)

- Challenge
  - Resolution이 떨어지기 때문에 Small object segmentation은 어려움.
  - CNN의 특성 layer가 깊으면 feature가 손실이있음.
  - Occlusions의 현상에 대해 대응하기 어려움
    - Object가 다른 object에 의해서 가려지는 경우
   
- One-stage & Two stage의 형태로 나뉘어져 있음. 
  - FCN & R-CNN으로도 분류가 되어짐
  - Detection base & Segmentation base

- Two-stage
  - Region proposal에서 나온 Bounding box에서 mask추출
 ![image](https://github.com/user-attachments/assets/91154efe-7b8f-4cb8-b4b9-f3cd2bde0beb)

- One-stage
  - Yolo처럼 segmentation & Detection을 병렬적으로 동시에 수행.
  - Prototype 마스크 생성 -> 같은 mask를 가지는것과 예측
 
![image](https://github.com/user-attachments/assets/b8b855a1-2a94-4b32-a563-42da7a43a214)

## Medical image Instance segmentation

- Object의 shape를 보기 위해선 분할이 필요
- Dense하게 있는 object의 경우 경계선이 붙어있음.
  - 각 영역마다 붙어 있는 경우 분할이 필요함.
- Real-time으로 사용하기 위해서는 속도도 중요함. (Surgical 용도)

![image](https://github.com/user-attachments/assets/8b9b181d-67b9-48c2-acda-32259f474ba5)


- Preprocessing
  - Copy and pastes
  - Contour mask 
  - Gradient map
- Network
  - Two-stage
  - One-stage
- Post-processing
  - Mask post-processing

### Augmentation

- Copy and pastes augmentation
  - Object의 mask가 있는 이미지를 다른 이미지에 붙이는 방법
  - Jittering의 방법과 Scaling과 방법과 함께 적용
  - Self-training 기술로도 유용함

### Preprocessing

- Contour mask
  - Image의 Contour(경계면)을 학습
  - Instance mask와 Contour mask 사용
    - Instance마다 분할에 도움을 줄 수 있도록 학습.

<img src="https://github.com/user-attachments/assets/30f742f1-d4d8-449a-82d8-e126fa0a84c6" width="50%" height="50%"/>
   
<img src="https://github.com/user-attachments/assets/b920edb1-c3a9-4504-befb-3f701da058c8" width="30%" height="30%"/>

- Gradient Map
  - Horizontal & vertical distance map을 만들어 활용
  - Nuclear pixel, gradient prediction, classification을 동시에 학습.
    - Regression과 classification을 동시에 loss로 적용
    - Post processing일때 gradient를 활용하여 instance 분할
   
![image](https://github.com/user-attachments/assets/030b9e82-a5d0-4940-8e89-ad869cf6baf0)

### Network (Two-stage)
- Mask-RCNN
  - 3D network상에서도 two stage로 문제를 품
    - Edge map을 활용하여 input image와 결합.
    - Region proposal network(RPN)를 사용하여 중복된 부분을 제거
    - RPN간의 유사도를 이용하여 후보를 남기기도 한다.
   
### Network (one-stage)
- YOLACT++
  - One-stage로 한번에 segmentation 과 detection의 문제도 푸는 방안도 있음.
  - 속도의 장점을 활용하여 Surgical에서 사용 되어짐
  - Multi scale, Attention을 사용하여 더 많은 정보 활용.
 
### Post-processing

- Watershed
  - Binary image를 경계선에 있는 영역을 나누기 위해서 사용
  - 골짜기에 물을 점진적으로 부어 segmentation을 하는 개념
  - Noise가 많을 경우 위험.
 
## Evaluation

- Precision-Recall
  - 각 예측이 나온 segmentation 는 probability를 가지고 있음.
  - Probability의 값을 변경하면 Precision, Recall이 변경이 됨
 
![image](https://github.com/user-attachments/assets/5ea310e3-97a1-41d6-b285-495248a3abeb)

### Medical Image detection
- IOU Mean Average precision
  - Probability를 기준으로 threshold를 점진적으로 주었을 때 나오는 그래프
  - 한 지점은 F1 score(빨간색) 로 표현이 가능하다.
  - 해당영역(주황색) 의 넓이는 Average Precision(AP).
  - 모든 Class마다 평균을 구하면 MAP
![image](https://github.com/user-attachments/assets/62b1a025-145c-42ad-94fc-f565df6dac67)
