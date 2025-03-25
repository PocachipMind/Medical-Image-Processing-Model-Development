# Segmentation

- Medical Image Segmentation
  - 병변의 Region of interest(ROI)를 분할하기 위한 방법으로 많이 사용
    - Tumor의 size나 치료할 병변의 위치를 정확하게 분할
    - 특정 조직의 구조를 분석
  - 진단 효율성과 정확성이 크게 향상
 
- Preprocessing
  - Pretrained model
  - Patching, Resampling, 
- Augmentation 
  - 기하학적 변환
- Difference architecture
  - Unet, DeepLabv3, UNETR
- Inference 
  - Test time Augmentation (TTA)

### Preprocessing
- 적은 data를 문제를 해결하기 위해 Pretrained model 사용
  - ImageNet 1k : natural image dataset
  - Self-supervised model : image representation을 학습한 model
- Patching & oversampling
- 특정영역에 random patch로 생성
- 영상의 크기가 큰 경우 Patch로 나뉘어서 학습에 반영

### Augmentation 
- Overfitting의 영향을 줄이기 위해 사용
- Flipping, cropping, rotate, color jittering

![image](https://github.com/user-attachments/assets/4975699a-86c0-4913-bda5-0cfaf5ed0743)

- Hard Aug
  - Cutout : 영상의 특정 부위를 masking
  - Mixup : 두 영상을 합하여 만듬.
  - Cutmix : 특정 부위를 다른 영상으로 대체

![image](https://github.com/user-attachments/assets/3d66a705-bf34-4c8b-93c4-4be9825037e3)


### Trick
- Test time augmentation (TTA)
  - Inference할때 이미지를 augmentation한 후 앙상블한 결과

<img src="https://github.com/user-attachments/assets/6abf59f9-7cc3-46c7-9874-ba05591941d0" width="50%" height="50%"/>

 
- Post Processing
  - Edge Enhancement 
  - Boundary 영역의 증가시켜 Noise제거
  - Hole filling : image의 내부의 영역을 동일한 mask로 채우는 방법

<img src="https://github.com/user-attachments/assets/cfe2a66d-b65c-4eba-9532-bb41b66b7ba0" width="30%" height="30%"/>

<img src="https://github.com/user-attachments/assets/02ccd0a5-4851-4eff-9db4-237636854e71" width="30%" height="30%"/>


### Loss

- Cross entropy

- Dice coefficient loss
  - Intersection of Union (IOU)처럼 A,B의 영역에 대해서 얼마나 겹쳐지는 지

<img src="https://github.com/user-attachments/assets/a56aba44-c5bf-40ac-ad45-7002476f9a78" width="50%" height="50%"/>

![image](https://github.com/user-attachments/assets/ddf0bb77-3e8b-4f40-8e51-6fff52ad325a)


- Jaccard/Intersection over Union (IoU) Loss
  - A,B의 영역에 얼마나 많이 겹치는지 판단하는 지표
 
![image](https://github.com/user-attachments/assets/bc328653-3219-48c5-b6c2-132ba06be119)

- Dice vs Jaccard 
  - 두 loss의 경우 영역의 유사도로를 보기 때문에 비슷하게 동작함.
  - Dice의 경우 0~1로 볼수 있음으로 직관적임.
 
## Evaluation

- Pixel wise or image level evaluation등 다양한 방법이 있음.
- Annotator마다 성능의 차이가 크게 남 & 정확한 평가 guideline이 없음.

- Dice & Jaccard index 
  - 전체 영역 중 Intersection된 영역에 대한 비율을 보는 방법
  - 따라서 1에 값이 가까워질수록 좋아지고 멀어질수록 좋아지지 않는다.

![image](https://github.com/user-attachments/assets/57a88b1c-f696-44ff-bf73-a33d5698e476)

![image](https://github.com/user-attachments/assets/4cbdee93-f97c-43da-a6aa-0ec669404ea1)


