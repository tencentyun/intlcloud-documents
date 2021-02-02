### 미니프로그램에서 다수의 도메인을 요청하거나 버킷명이 정확하지 않을 경우, 화이트리스트 설정 및 제한 이슈를 어떻게 해결해야 하나요?

SDK 인스턴스화할 때 `ForcePathStyle:true`를 사용하여 접미사를 활성화할 수 있습니다. `https://cos-ap-beijing.myqcloud.com/<BucketName-APPID>/<Key>` url 포맷으로 접미사를 정식 요청하면 서명 시 버킷 이름 `/<BucketName-APPID>`도 서명 계산에 포함됩니다.

### 미니프로그램으로 어떻게 이미지를 로컬 디바이스에 저장하나요?

`cos.getObjectUrl`을 통해 이미지 url을 획득한 후 `wx.downloadFile`을 호출하여 이미지 다운로드할 임시 경로를 얻습니다. 인터페이스에 이미지 저장 버튼이 표시되며, 사용자가 버튼을 클릭하면 `wx.saveImageToPhotosAlbum`을 호출하여 앨범에 이미지를 저장하게 됩니다.
