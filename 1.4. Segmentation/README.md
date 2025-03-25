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

