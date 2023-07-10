### 미니프로그램에서 다수의 도메인을 요청하거나 버킷명이 정확하지 않을 경우, 얼로우리스트 설정 및 제한 이슈를 어떻게 해결해야 하나요?

SDK를 인스턴스화할 때 `ForcePathStyle:true`를 사용하여 접미사 스타일을 활성화하십시오. 다음 형식의 url에서 접미사 스타일을 요청하는 경우:
```
https://cos-ap-beijing.myqcloud.com/<BucketName-APPID>/<Key>
```
버킷 이름 `/<BucketName-APPID>`도 서명 계산에 추가됩니다.

### 미니프로그램으로 어떻게 이미지를 로컬 디바이스에 저장하나요?

1. `cos.getObjectUrl`을 사용하여 이미지 url을 가져옵니다.
2. `wx.downloadFile`을 호출하여 이미지를 다운로드하여 임시 경로를 얻습니다.
3. 버튼을 클릭하여 `wx.saveImageToPhotosAlbum`을 호출하여 이미지를 사진첩에 저장합니다.


### QQ 미니프로그램은 미니프로그램 SDK를 사용해 COS에 파일을 업로드할 수 있나요?

COS는 현재 WeChat 미니프로그램만 지원합니다. QQ 미니프로그램과 WeChat 미니프로그램은 상호 통신이 불가능하므로 미니프로그램 SDK를 사용할 수 없습니다.

### 미니프로그램에서 cos-wx-sdk-v5로 버킷에 파일을 업로드할 때 getAuthorization 함수는 어떤 역할을 하나요?

미니프로그램 SDK의 getAuthorization 함수는 백그라운드에서 임시 키를 획득하여 프런트 엔드로 전달하는 역할을 하며, 프런트 엔드에서 서명을 계산한 후 업로드, 삭제 등의 작업을 진행합니다. 키 유출 방지를 위해 임시 키 형식 사용을 권장합니다. 자세한 내용은 [미니프로그램 SDK에서 COS 인스턴스 생성 예시](https://intl.cloud.tencent.com/document/product/436/30609)를 참조하십시오.

