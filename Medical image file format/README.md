# Medical image file format

### Digital Imageing and Communications in Medicine ( DICOM )

- 정보들의 경우 Information Object Definitions (IODs)로 표현

- IOD를 저장 후 DICOM을 다른 device에 보낼경우 이미지가 유실될 수 있음.
- Dicom Server Element (DIMSE) : IOD를 가지고 할 수 있는 행위 (저장, 찾기, 전송, 만들기, 가져오기 )
- 최종적으로 Service-Object Pair(SOP) = IOD + DIMSE class를 가지고 동작되어짐.

### Neuroimaging Informatics Technology Initiative (NIFTI)

![image](https://github.com/user-attachments/assets/55e47e80-b93b-4dc6-bb09-cd1fd24f7a6b)

https://irvifa.medium.com/dicom-and-nifti-f22cb411d378
