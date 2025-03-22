# Medical image file format

## Digital Imageing and Communications in Medicine ( DICOM )

- 정보들의 경우 Information Object Definitions (IODs)로 표현

- IOD를 저장 후 DICOM을 다른 device에 보낼경우 이미지가 유실될 수 있음.
- Dicom Server Element (DIMSE) : IOD를 가지고 할 수 있는 행위 (저장, 찾기, 전송, 만들기, 가져오기 )
- 최종적으로 Service-Object Pair(SOP) = IOD + DIMSE class를 가지고 동작되어짐.

## Neuroimaging Informatics Technology Initiative (NIFTI)

![image](https://github.com/user-attachments/assets/55e47e80-b93b-4dc6-bb09-cd1fd24f7a6b)

https://irvifa.medium.com/dicom-and-nifti-f22cb411d378


- NIFTI : 파일 하나로 되어있음. 헤더가 적음. 파일 Path 단순.
- DICOM : 파일 여러가지로 되어있음. 헤더가 많음. 파일이 여러개로 저장되어 파일 Path가 복잡.

Nifti 1 : 8bit

Nifti 2 : 64 bit

## 시각화

- GUI :
- CLI : Pydicom ( DICOM ), Nibabel ( Nifti ), Pathology (Openslide)

## Whole Slide Imaging (WSI)

병리 영상 (Pathology image)의 경우 아직 PACS에 완전한 연결 시도하지 못했음.
