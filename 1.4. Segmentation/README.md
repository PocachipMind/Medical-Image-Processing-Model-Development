![image](https://github.com/user-attachments/assets/9cc44d49-a1ac-488b-8d58-d361eb3294b7)# Segmentation

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

![image](https://github.com/user-attachments/assets/6abf59f9-7cc3-46c7-9874-ba05591941d0)
 
- Post Processing
  - Edge Enhancement 
  - Boundary 영역의 증가시켜 Noise제거
  - Hole filling : image의 내부의 영역을 동일한 mask로 채우는 방법

<img src="https://github.com/user-attachments/assets/cfe2a66d-b65c-4eba-9532-bb41b66b7ba0" width="30%" height="30%"/>

<img src="https://github.com/user-attachments/assets/02ccd0a5-4851-4eff-9db4-237636854e71" width="30%" height="30%"/>
