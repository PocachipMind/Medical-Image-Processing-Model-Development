# Resource Optimized Neural Architecture Search for 3D Medical Image Segmentation

원문 논문 : 

https://arxiv.org/abs/1909.00548

전반적으로 3D Medical Image Segmentation을 Neural Architecture Search 를 통해서 옵티마이즈 하는 방안에 대해 제안을 했습니다.

## Abstract
- What is Network Architecture Search(NAS)?
  - Neural Networks의 최적화 되어진 모델을 찾아주는 프레임워크
- 많은 Natural image분야에서 사용되어지고 있다.
- Medical + 3D Segmentation 에 연구는 안되어지고 있음.
  - 시간과 computational cost가 너무 큼
- Small cost, 3D medical에 대한 해결을 제한

## Related work

- Why need NAS?
  - 성능이 최적화된 Network를 찾기 위해서는 hyperparameters를 변경해가며
  실험을 해야된다.
  - 연구자가 반복적인 실험은 비효율적임 자동적으로 최적의 parameter를 찾는
  방법을 연구 -> Automated Machine Learning (AutoML)
  - AutoML에서 최적인 network를 만들어주는 방법인 Neural Architecture 
  Search(NAS)로 발전.

- Search Space (검색공간)
  - Architecture에 영향을 받는 변수에 대한 정의
- Search Strategy (검색 전략)
  - 검색공간을 탐색하는 방법으로 빠르게 찾는 방안이 제안이 됨.
- Performance Estimation Strategy (성능 추적 전략)
  - 측정하고자 하는 데이터에 대해 높은 성능을 달성하는 전략
  - 시간이 오래 걸림으로 단축이 필요

![image](https://github.com/user-attachments/assets/679dd40f-827c-448a-8edd-8c374545c3f7)


- Efficient Neural Architecture Search via Parameter Sharing
- 많은 연산량을 줄이는데 초점을 맞춤.
  - 일반적으로 RNN을 이용한 Controller를 사용하지만 자원이 많이 소비됨
  - 치명적인 이유 중 하나는 학습되었던 child model weight를 버리기 때문
- 저자는 child model를 서로 공유하도록 만듬
  - 그림에 있는 바와 같이 subgroup 즉 child model끼리 연결되어 있음.
 
![image](https://github.com/user-attachments/assets/cbb2f0ed-5086-43c5-818a-3c3e84ad35f2)


- Method 
  - 빨간 edge부분에 대해서는 활성화
  - 1>2>3 , 1>4 처럼 각각의 영역에 왔을 때 이전에 사용하였던 노드와 함께 합쳐서 진행이 됨. (3,4의 평균)
 
![image](https://github.com/user-attachments/assets/9b4a0dcd-6844-4a1f-9248-84d35b6c5d34)

- Designing Convolutional Networks
  - 어떤 노드를 연결?
  - 어떤 computation operation을 연결?
  - 후보군 생성
  - 3 x 3 or 5 x 5 conv filters 
  - 3 x 3 or 5 x 5 depth-wise-separable conv filters 
  - Average or max pooling with 3 x 3 kernel size
 
![image](https://github.com/user-attachments/assets/e5b97cf8-ad4a-421d-8afb-4415bb8aad43)

- Scalable Neural Architecture Search for 3D Medical Image Segmentation (SCNAS)
- 3D medical image NAS의 처음 적용한 논문
  - 최적화 속도를 위해서 아래과같은 방법 제안
  - stochastic sampling algorithm
  - Gumbel-Softmax relaxation
- Encoder, decoder, reduction, expansion으로 구성되어있음.

![image](https://github.com/user-attachments/assets/b0e7fdd7-d33b-4a14-b865-ae04964586d6)

## Method

- Proposed Searching Space
  - RNN base controller를 사용
  - 다른 spacing의 사용을 다르게 접근함.
  - anisotropic(이방성) 이미지 특성 사용 : 4×155×240×240, 1×[90∼130]×320×320, 2×[11∼24]×[256∼ 384]×[256∼384]
  - receptive field확장을 위해 Dilation rate, pooling을 포함.
  - Memory의 사용을 줄이기 위해서 Micro Search을 적용
 
![image](https://github.com/user-attachments/assets/6a044a46-9857-4531-b427-ac7c984a0603)

![image](https://github.com/user-attachments/assets/1189627a-9de0-4bc5-82ed-dbe771cd0dd2)


- Unet에 들어있는 Skip connection의 경우 Add로 사용하여 memory를 줄임
- Depth-wise convolution을 이용
- Model 에 들어가는 input의 경우 height(H), width(W), and depth(D)로 설정하여 stride(S)여 결정한다.

![image](https://github.com/user-attachments/assets/acb16c45-4ed0-448f-a14e-e9543432753d)


- Proposed base Architecture
- Skip connection되는 부분을 1x1x1 convolution으로 변경

![image](https://github.com/user-attachments/assets/c3fff396-7ca7-44ed-9be9-b1efb9f76b24)


- ENAS(Efficient Neural Architecture Search via Parameter Sharing)방법론을 적용
- NAS가 반복하는 모든 Search Space를 하나의 Directed Acyclic Graph (DAG, 유향 비순환 그래프)로 나타내어서 접근.

![image](https://github.com/user-attachments/assets/35ec1663-6ce3-428c-bf16-f5729320a4aa)

## Experiment

- 3D shape, channel size이 영상마다 모두 다르기 때문에 다양한 dataset에서 검증이 필요
- decathlon challenge dataset 사용
  - Brain , Heart, Prostate image
- 5-fold cross validation evaluation 사용

![image](https://github.com/user-attachments/assets/fd1089d8-ea44-4b9b-8510-7fc1d510a228)


- Z-score normalization
  - Image의 mean과 std가 각각 0,1이 되도록 변환 (x – μ) / σ
- Detail
  - Brain image : voxel이 0많이 때문에 (background) 최솟값으로 cropping함 (foreground) 
  - Weight decay : 0.001 and 0.0001
  - Adam optimizer
  - Controller : Epochs 150~500 
  - Child model : Epochs 3
  - 모델의 memory방지를 위해서 첫 child model은 maximum size로 학습
 
## Result

- Scalable neural architecture search for 3d medical image (SCNAS) & nnUnet과 비교한 결과
- GPU와 TTA의 사용유무를 제외하더라도 더 좋은 성능 달성함.
  - 앙상블 없이 단일 network로 SOTA달성
  - Patching기법 사용하지 않음.
 
![image](https://github.com/user-attachments/assets/c4fcfac7-827e-49c1-bb5d-c8b6738178e3)

- Entropy와 각 task마다 reward를 추적한 결과 entropy증가와 reward가 잘 되어지고 있음을 볼 수 있음.
- Network 구조가 optimal 하게 만들어짐을 볼 수 있음.

![image](https://github.com/user-attachments/assets/fdfc2c4c-aa32-4e0d-86a5-c894b757bf74)

## Conclusion

- 3D Medical image segmentation에 특화된 NAS를 제안함.
- Memory와 속도적인 측면에서도 뛰어난 성능을 보여주었으며 SOTA를 달성함을 볼 수 있음.
- 새로운 데이터가 오더라도 optimal 한 network를 구성할수 있음.
