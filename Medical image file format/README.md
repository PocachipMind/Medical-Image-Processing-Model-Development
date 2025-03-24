# Medical image file format

## Digital Imageing and Communications in Medicine ( DICOM )

- 정보들의 경우 Information Object Definitions (IODs)로 표현

- IOD를 저장 후 DICOM을 다른 device에 보낼경우 이미지가 유실될 수 있음.
- Dicom Server Element (DIMSE) : IOD를 가지고 할 수 있는 행위 (저장, 찾기, 전송, 만들기, 가져오기 )
- 최종적으로 Service-Object Pair(SOP) = IOD + DIMSE class를 가지고 동작되어짐.

<img src="https://github.com/user-attachments/assets/1cf38325-862c-4dac-9205-69a65434a776" width="60%" height="60%"/>


## Neuroimaging Informatics Technology Initiative (NIFTI)

<img src="https://github.com/user-attachments/assets/55e47e80-b93b-4dc6-bb09-cd1fd24f7a6b" width="60%" height="60%"/>

https://irvifa.medium.com/dicom-and-nifti-f22cb411d378

<img src="https://github.com/user-attachments/assets/b5d2dbf0-fcce-47af-837e-bb55cbc1c145" width="60%" height="60%"/>


- NIFTI : 파일 하나로 되어있음. 헤더가 적음. 파일 Path 단순.
- DICOM : 파일 여러가지로 되어있음. 헤더가 많음. 파일이 여러개로 저장되어 파일 Path가 복잡.

Nifti 1 : 8bit

Nifti 2 : 64 bit

## 시각화

- GUI : 3D slicer, Qupath
- CLI : Pydicom ( DICOM ), Nibabel ( Nifti ), Pathology (Openslide)

## Whole Slide Imaging (WSI)

![image](https://github.com/user-attachments/assets/f03d6ce4-b2ac-476b-992c-9b3dd8033c77)

병리 영상 (Pathology image)의 경우 아직 PACS에 완전한 연결 시도하지 못했음.

( PACS : 메디컬 디바이스부터 이미지 전처리 이후 사람한테 까지 보이는 경로의 시스템을 의미. 병리영상은 Radiology 보다 디지털 영상화가 늦었다는 단점이 있음. 고화질 영상기술 필요 -> 큰용량 필요.)

### WSI format 

- Z stack 기술 사용
