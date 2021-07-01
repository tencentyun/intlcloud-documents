### 미니프로그램에서 다수의 도메인을 요청하거나 버킷 이름이 정확하지 않을 경우, 화이트리스트 설정 및 제한 이슈를 어떻게 해결해야 하나요?

SDK를 인스턴스화할 때 `ForcePathStyle:true`를 사용하여 접미사를 활성화할 수 있습니다. `https://cos-ap-beijing.myqcloud.com/<BucketName-APPID>/<Key>` url 포맷으로 접미사를 정식 요청하면 서명 시 버킷 이름 `/<BucketName-APPID>`도 서명 계산에 추가됩니다.

### 미니프로그램으로 어떻게 이미지를 로컬 디바이스에 저장하나요?

`cos.getObjectUrl`을 통해 이미지 url을 획득한 후 `wx.downloadFile`을 호출하여 이미지를 다운로드할 임시 경로를 획득합니다. 인터페이스에 이미지 저장 버튼이 표시되며, 사용자가 버튼을 클릭하면 `wx.saveImageToPhotosAlbum`을 호출하여 앨범에 이미지를 저장하게 됩니다.


### QQ 미니프로그램은 미니프로그램 SDK를 사용해 COS에 파일을 업로드할 수 있나요?

COS는 현재 WeChat 미니프로그램만 지원합니다. QQ 미니프로그램과 WeChat 미니프로그램은 상호 통신이 불가능하므로 미니프로그램 SDK를 사용할 수 없습니다.

### 미니프로그램에서 cos-wx-sdk-v5로 버킷에 파일을 업로드할 때 getAuthorization 함수는 어떤 역할을 하나요?

미니프로그램 SDK의 getAuthorization 함수는 백그라운드에서 임시 키를 획득하여 프런트 엔드로 전달하는 역할을 하며, 프런트 엔드에서 서명을 계산한 후 업로드, 삭제 등의 작업을 진행합니다. 키 유출 방지를 위해 임시 키 형식 사용을 권장합니다. 자세한 내용은 [미니프로그램 SDK에서 COS 인스턴스 생성 예시](https://intl.cloud.tencent.com/document/product/436/30609)를 참조하십시오.

### COS 미니프로그램에서 다수의 도메인을 요청하거나 버킷 이름이 정확하지 않을 경우, 화이트리스트 설정 및 제한 이슈를 어떻게 해결해야 하나요?

SDK를 인스턴스화할 때 ForcePathStyle:true를 사용하여 접미사를 활성화할 수 있습니다. 다음과 같은 포맷으로 접미사를 정식 요청하면 서명 시 버킷 이름 `/<BucketName-APPID>`도 서명 계산에 추가됩니다.
```
https://cos-ap-beijing.myqcloud.com/<BucketName-APPID>/<Key>
```
