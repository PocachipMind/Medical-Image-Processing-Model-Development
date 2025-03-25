# Detection

- Segmentation의 경우 같은 semantic간의 label이 되었음.
- Detection의 경우 각 객체마다 annotation으로 되어있음.

![image](https://github.com/user-attachments/assets/318c49ad-0b70-4402-b837-4d8a8ba106f7)


- Preprocessing 
  - Data sampling
  - Resize & augmentation 
- Network 
  - One-stage 
  - Two-stage
- Loss
  - Focal loss
- Post-processing 
  - Non-maximum suppression(NMS)
 
### Preprocessing 

- Online Hard Negative Mining (OHNM)
  - Negative 의 sample이 많이 때문에 불균형의 문제를 해결함
  - 특히 모델이 예측이 어려움 Hard negative sample를 사용함으로 모델이 강인해짐
  - 파란 박스내에서 topk의 빨간박스를 선택하여 학습을 진행함.
 
- Multi-scale sample 
  - Resample이 되어지는 이미지마다 bounding box의 의미는 달라짐
  - Scale에 variant 한 small object의 경우 multi scale에 효과적임
  - 하지만 Inference 속도는 느려짐
 
![image](https://github.com/user-attachments/assets/f37d8bad-00fd-430c-b3bb-a0ae40374ab9)


- Basic augmentation
  - Flip, Rotate, Cutout 등
  - Bounding box와 함께 적용함.
- Mosaic augmentation 
  - 4장의 각기 다른 이미지의 Patch와 조합하여 만듬.
  - 적은 batch로 학습이 가능

![image](https://github.com/user-attachments/assets/9ed68780-13e9-41e8-a953-2824145cfdb5)

### Network - Two Stage

- Faster-RCNN
  - Anchor box approach
  - R-CNN -> Fast R-CNN -> Faster R-CNN 순서로 발전
1. Region proposal network 에서 해당영역을 bounding box영역을 추출
2. 추출된 영역 (Region)에서 원본 layer로 pooling시켜 classification

- Why use Region proposal ?
  - 기존에서는 sliding window를 통해서 모든 영역에 대해서 detection후보를 뽑음.
  - Region을 network로 학습 시킴으로 효율성 증가.
- 기존의 방법보다 속도 개선 하지만 느림

### Network (Neck)
- Feature Pyramid Network (FPN)
  - Computation & memory의 부담
  - single-scale 이미지를 CNN에 입력하여 다양한 scale feature map활용
  - Loss의 사용 증가로 Computational cost커짐

### Network - One Stage

- You Only Look Once (YOLO)
  - Faster R-CNN보다 성능은 낮지만 속도의 개선이 뛰어남. -> 6배 빠르게 발전
  - Cell로 나누어 anchor box로 사용 (cell이 중심 기준으로 width, height 예측)
  - Classification과 localization을 동시에 진행함
    - Confidence가 높으면 box를 굵게 + cell단위로 classification 진행
    - X,Y좌표 width, height, confidence동시에 학습.

- Fully Convolutional One-Stage Object Detection (FCOS)
  - 이전의 방법의 경우 Anchor box size나 scale를 custom하게 설정해주어야함. 
  - 물체의 center를 예측하여 anchor box 튜닝이 필요없어짐. (Anchor-free)
  - 작은 object에 대해서는 centerness를 이용하여 처리. 
  - 더 많은 양의 positive sample사용가능

- End-to-End Object Detection with Transformers (DETR)
  - 기존의 방법들을 한번에 풀도록 정의
    - Pre-defined anchorbox -> model -> predict -> post-processing
  - bipartite matching을 사용
    - Matching cost가 최소인 permutation 추출 (GIOU 사용)
  - Faster R-CNN과 동급의 정확도 및 런타임 속도를 보였다.
    - 속도의 개선에 관한 연구
<img src="https://github.com/user-attachments/assets/a5cb7076-d9ea-40ac-9f8d-3c29086471ff" width="30%" height="30%"/>

### Post-processing
- Non-maximum suppression
  - Detection에서는 수많은 output이 나오기 때문에 후처리가 필요하다.
  - Anchor box 나 Anchor-free나 target하는 object가 중첩되어 나옴
  - IOU > threshold중 probability가 높은 영역만 보존
  - 후처리의 성능향상 위해 IOU의 개선연구도 진행됨.

![image](https://github.com/user-attachments/assets/7452d415-f76d-4ad7-b326-ea07bd69e59d)

- Sliding window
  - 작은 객체 탐지를 위해서 patch단위로 잘라서 Inference도 이루어진다.
 
### Loss

- Focal loss
  - One-stage detector의 정확도의 개선이 되어지기 위해 제안됨
  - Anchor box나 Anchor-free의 경우에서 Negative의 비율이 많음. 
  - 이는 학습의 영향에 저하.
  - Negative부분에 대해서는 가중치를 많이 부여.

<img src="https://github.com/user-attachments/assets/1058b610-99fb-4a44-a148-89f902c001cc" width="50%" height="50%"/>

## Evaluation

- Intersection of Union (IOU)
  - 예측된 box와 ground truth의 box가 일치하는지에 따른 값
  - Ex) 겹치는 영역이 80% 이상일때 TP
  - Ex) 겹치는 영역이 20% 미만일때 FP
  - GT의 영역에 predict이 없는 경우 FN
  - 이를 통해서 confusion matrix를 만들수 있음.

![image](https://github.com/user-attachments/assets/6af7ddff-de98-4177-b4d9-2aaba9b2203c)

- Precision-Recall
  - 각 예측이 나온 bounding box는 probability를 가지고 있음.
  - Probability의 값을 변경하면 Precision, Recall이 변경이 됨

![image](https://github.com/user-attachments/assets/01fd799c-ccf9-4d9a-bf55-5513e7f8b2d6)
