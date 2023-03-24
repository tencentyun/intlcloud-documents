임의 상황에서 버킷을 삭제해야 할 경우, 콘솔, 툴, API 또는 SDK 방식으로 버킷을 삭제할 수 있습니다.

>!버킷을 삭제한 후에는 복구할 수 없으니 신중히 하시기 바랍니다.

## 제한 설명

- 현재는 데이터가 이미 비어 있는 버킷 삭제만 지원합니다. 버킷에 객체나 파일 조각이 여전히 있을 경우 삭제에 실패합니다. 버킷 삭제 실행 전에 버킷 내부에 객체가 비어 있는지 확인하십시오. 자세한 내용은 [버킷 비우기](https://intl.cloud.tencent.com/document/product/436/30926)에서 알아보십시오.
- 버킷 삭제 시, 작업자가 해당 작업에 대한 권한을 보유했는지, 정확한 버킷 이름(Bucket)과 리전(Region) 매개변수가 전달되었는지 확인해야 합니다.


## 사용 방법

### COS 콘솔 사용

객체 스토리지 콘솔을 사용하여 버킷을 삭제할 수 있습니다. 자세한 내용은 [버킷 삭제](https://intl.cloud.tencent.com/document/product/436/30361) 콘솔 가이드 문서를 참조하십시오.

### 사용 툴

COSBrowser, COSCMD 등의 툴을 사용하여 버킷을 삭제할 수 있습니다. 자세한 내용은 [툴 개요](https://intl.cloud.tencent.com/document/product/436/6242)를 참조하십시오.

### REST API 사용

REST API를 사용하여 버킷 삭제 요청을 실행할 수 있습니다. 자세한 내용은 [DELETE Bucket](https://intl.cloud.tencent.com/document/product/436/7732) API 문서를 참조하십시오.

### SDK 사용

SDK의 버킷 삭제 메서드를 호출할 수 있습니다. 자세한 내용은 아래 각 언어로 된 SDK 문서를 참조하십시오.

- [Android SDK](https://intl.cloud.tencent.com/document/product/436/31463)
- [C SDK](https://intl.cloud.tencent.com/document/product/436/31464)
- [C++ SDK](https://intl.cloud.tencent.com/document/product/436/31465)
- [.NET SDK](https://intl.cloud.tencent.com/document/product/436/30595)
- [Go SDK](https://intl.cloud.tencent.com/document/product/436/31466)
- [iOS SDK](https://intl.cloud.tencent.com/document/product/436/31467)
- [Java SDK](https://intl.cloud.tencent.com/document/product/436/31468)
- [JavaScript SDK](https://intl.cloud.tencent.com/document/product/436/31477)
- [Node.js SDK](https://intl.cloud.tencent.com/document/product/436/31469)
- [PHP SDK](https://intl.cloud.tencent.com/document/product/436/31470)
- [Python SDK](https://intl.cloud.tencent.com/document/product/436/31471)
- [Mini Program SDK](https://www.tencentcloud.com/document/product/436/31472)

