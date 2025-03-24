# Medical image acquisition

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
