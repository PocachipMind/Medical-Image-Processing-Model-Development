# Medical image acquisition

## Image 종류
### X-ray

- 대부분 2차원 이미지.

- 영상마다 품질이 다 다르기 때문에 크기, 반전여부, 각도, 문구, 밀도 등 전처리가 필수임.

### Compuuted tomography (CT)

- X-ray에서 더 발전된 3D 영역으로 확장시켜 영상 획득

- Hounsfuekd unit(HU)로 표현이 됨.
  - 물 흡수에 의해 정의

![image](https://github.com/user-attachments/assets/46b2d1c9-c036-4c1c-95b7-934fe0480bab)

- 원하는 조직 영상 시각화 위해 전처리 필요.
- Window width와 Window level을 통해 0~255 로 변경하여 사용.

![image](https://github.com/user-attachments/assets/7c4959af-a794-42bf-b406-b17bd0fd787a)

- 중요 Parameter :
  - Z축 distance ( Z축으로 얼마인지 )
  - 픽셀당 Width와 Height
  - Voxel 간의 거리
  - Smooth, Reconstruction filters

### Magnetic Resonance Imaging (MRI)

- 높은 해상도
- CT와 reconstruction하는 과정 비슷

- (공명주파수)RF function을 준 후 전자들이 원 위치로 돌아가는데 걸리는 시간에 따라 다양한 image영상 획득
  - T1 : z방향으로 다시 돌아갈때 발생한 영상 ( 지방조직을 밝게 )
  - T2 : T1보다 영상이 짧으며 회복시간이 짧음 ( 높은 수분이 있는 영역을 밝게 )
 
- K-space : 주파수 방향으로 여러 이미지 만들어 냄

### Pathology 

- Digital Pathology
  - Whole slide image는 모든 정보 포함
    - 여러 해상도 제공, stiched 되어 기가 픽셀의 이미지를 가지고 있음.
  - image resolution이 커서 전체 분석은 시간 소요가 많이 되어짐
    - 일반적으로 작은 patch로 잘라서 분석.
  - Patch간의 좌표 보정이 필요.

- microns per pixel (mpp) : pixel마다 실제 distance를 의미
  - ex ) 0.25 mm 인 경우 :  1 micro meter를 저장하기 위해서 4~5 pixel이 필요
- Multi-scale or scale 통일 전처리 필요.

- WSI 만드는 과정, 많은 artifact 발생.
  - 조직 손상, 염색 부족, scanning 장비의 문제 등

- Radiology 영상과 다르게 RGB color 표현. 다양할 수 있음.
  - 해결 방법 적용
    - Gray scale
    - Blind Color deconvolution
    - Color normalize
    - Augmentation
   
- Zoom in 된 patch와 Zoom out된 patch들 간 전처리 필요. 연관성 있는 patch 생성 중요.
- Color augmentation을 통해 분포를 넓혀 사용하는 방식도 사용

## Medical image preprocessing

### Medical image data
- 장비간 얻어지는 Pixel간 distance 있음.
- 3D의 경우 slice distance도 고려하여 맞춰줘야함.
- Image size를 맞추기 위해 voxel spacing을 활용.

### Voxel spacing
- 물리적인 위치이기에 실제 위치와 다름
- phys_coords = origin + voxel_spacing * voxel_coord
   
### Look Up Table ( LUT ) : 다이콤 이미지에서 많이 사용
- Modaility LUT
  - Device에서 나온 pixel의 값 변환, Load할 때 값 사용.
- VOI LUT
  - 원하는 조직 영역 보기위해 적용
- Presentation LUT
  - Device마다 영상을 Gray scale의 표현값을 설정
 
![image](https://github.com/user-attachments/assets/ba5b52ba-0b14-4b36-bce2-08a995e02e9e)

- Histogram equalization
