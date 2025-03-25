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
