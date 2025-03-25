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

- Copy and pastes augmentation
• Object의 mask가 있는 이미지를 다른 이미지에 붙이는 방법
• Jittering의 방법과 Scaling과 방법과 함께 적용
• Self-training 기술로도 유용함
