### 업로드 완료되지 않은 파일을 삭제하려면 어떤 API를 호출해야 합니까?

먼저 ListMultipartUploads API를 호출하여 업로드 완료되지 않은 파일을 나열합니다. 그 다음 Abort Multipart upload API를 호출하여 멀티파트 업로드를 포기하고 이미 업로드된 부분을 삭제합니다.

### 일괄 삭제 API를 호출한 후 올바르게 반환되지만 실제로 파일 삭제에 실패하면 어떻게 해야 합니까?

삭제할 파일의 경로를 확인하십시오. 파일 경로는 "/"로 시작하면 안 됩니다.

### XML API를 사용하여 JSON API를 통해 생성된 버킷과 업로드된 객체를 관리할 수 있습니까?

예, XML API는 COS 기본 아키텍처를 기반으로 합니다. JSON API로 생성된 데이터를 작업하는 데 사용할 수 있습니다.

### XML API와 JSON API의 관계는 무엇입니까?

 JSON API는 2016년 9월부터 사용자가 COS에 액세스하는 데 사용하는 API입니다. 업로드 도메인 이름은 `<Region>.file.mycloud.com`입니다. JSON API는 유지 보수 상태로 유지되며 정상적으로 사용할 수 있지만 새 기능을 개발하지 않습니다. 표준 XML API 기본 아키텍처와 동일하며 데이터 상호 연결되어 교차 사용할 수 있지만 API가 호환되지 않으며 도메인 이름이 일치하지 않습니다.

### XML API와 JSON API의 키를 공유할 수 있습니까?

예. 키는 [클라우드 API 키 콘솔](https://console.cloud.tencent.com/capi)에서 확인할 수 있습니다.

### XML API와 JSON API는 하나의 서명을 공유합니까?

아니요. XML API와 JSON API 서명이 따로 있습니다. 자세한 내용은 다음을 참조하십시오.

- [JSON API 서명](https://cloud.tencent.com/document/product/436/6054)
- [XML API 서명](https://intl.cloud.tencent.com/document/product/436/7778)

### XML API와 JSON API는 동일한 ACL 권한을 공유합니까?

아니요. XML API와 JSON API가 별도로 ACL 권한을 가집니다.

### Phthon SDK에 대한 임시 다운로드 URL을 얻으려면 어떻게 해야 합니까？

자세한 내용은 [사전 서명 다운로드 링크 가져오기](https://cloud.tencent.com/document/product/436/12270#.E8.8E.B7.E5.8F.96.E9.A2.84.E7.AD.BE.E5.90.8D.E4.B8.8B.E8.BD.BD.E9.93.BE.E6.8E.A5) 문서를 참조하십시오.

### CDN 가속 도메인 이름으로 SDK에 액세스할 수 있습니까?

예. 프로그래밍 언어에 따라 해당 [SDK 문서](https://cloud.tencent.com/document/sdk)를 참조하십시오.


### 미니 프로그램에서 여러 도메인 이름을 요청했거나 버킷 이름이 확실하지 않은 경우 화이트리스트를 구성하고 제한하려면 어떻게 해야 합니까?

SDK를 인스턴스화할 때 `ForcePathStyle:true`를 사용하여 후위식을 열 수 있습니다. 요청 url의 형식은 다음 `https://cos-ap-beijing.myqcloud.com/<BucketName-APPID>/<Key>` 후위식 요청와 같으면，서명할 때 버킷 이름 `/<BucketName-APPID>`도 서명 계산에 추가될 것입니다.

### 미니 프로그램의 이미지를 로컬로 어떻게 저장합니까?
먼저 `cos.getObjectUrl`을 사용하여 이미지 URL을 얻고, 그 다음 `wx.downloadFile`을 호출하여 이미지를 다운로드한 다음 임시 경로를 얻게 됩니다. 이미지 저장 버튼이 나타나면 버튼을 클릭하고 `wx.saveImageToPhotosAlbum`이 호출되어 이미지가 앨범에 저장됩니다.
