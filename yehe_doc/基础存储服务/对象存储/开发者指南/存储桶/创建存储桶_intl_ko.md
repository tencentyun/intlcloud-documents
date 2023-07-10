파일을 Cloud Object Storage(COS)에 보관할 경우, 우선 객체를 보관할 버킷을 생성해야 합니다. 콘솔, 툴, API 또는 SDK를 통해 버킷을 생성할 수 있습니다.

버킷 생성 후, 객체를 해당 버킷에 업로드할 수 있으며, 버킷을 위한 기타 기능을 설정할 수 있습니다. 예를 들어, [정적 웹 사이트 설정](https://intl.cloud.tencent.com/document/product/436/14984), [버킷 태그 설정](https://intl.cloud.tencent.com/document/product/436/30928), [버킷 암호화 설정](https://intl.cloud.tencent.com/document/product/436/33455) 등이 있습니다. 가이드 설정 관련 자세한 내용은 [콘솔 개요](https://intl.cloud.tencent.com/document/product/436/11365)를 참고하십시오.


## 제한 설명

1. 하나의 루트 계정은 최대 200개의 버킷을 생성할 수 있습니다.
2. 버킷 생성 완료 후에는 버킷 이름과 소속 리전을 수정할 수 없습니다.
3. 하나의 루트 계정에서 각 버킷은 고유한 이름을 가지며 이름을 변경할 수 없습니다.
4. 버킷 이름은 알파벳 소문자와 숫자, 즉 [a-z, 0-9], 하이픈 ‘-’ 만 사용 가능합니다. 버킷 이름의 최대 글자 수는 **[리전 약칭](https://intl.cloud.tencent.com/document/product/436/6224)** 및 **APPID** 글자 수의 영향을 받습니다. 완전한 요청 도메인의 최대 글자 수는 60자입니다. 예를 들어 요청 도메인 `123456789012345678901-1250000000.cos.ap-beijing.myqcloud.com`은 총 60자입니다.
5. 버킷 이름 생성 시, ‘-’으로 시작하거나 끝날 수 없습니다.


## 사용 방법

### COS 콘솔 사용

COS 콘솔을 사용하여 버킷을 생성할 수 있습니다. 자세한 내용은 [버킷 생성](https://intl.cloud.tencent.com/document/product/436/13309) 콘솔 문서를 참고하십시오.

### 툴 사용

COSBrowser, COSCMD 등의 툴을 사용하여 버킷을 생성할 수 있습니다. 자세한 내용은 [툴 개요](https://intl.cloud.tencent.com/document/product/436/6242)를 참고하십시오.

### REST API 사용

REST API를 사용하여 버킷 생성 요청을 실행할 수 있습니다. 자세한 내용은 [PUT Bucket](https://intl.cloud.tencent.com/document/product/436/7738) API 문서를 참고하십시오.

### SDK 사용

SDK 버킷 생성 메소드를 호출할 수 있습니다. 자세한 내용은 아래 각 언어로 된 SDK 문서를 참고하십시오.

- [Android SDK](https://intl.cloud.tencent.com/document/product/436/31463)
- [C SDK](https://intl.cloud.tencent.com/document/product/436/31464)
- [C++ SDK](https://intl.cloud.tencent.com/document/product/436/31465)
- [.NET SDK](https://intl.cloud.tencent.com/document/product/436/30595)
- [Go SDK](https://intl.cloud.tencent.com/document/product/436/31466)
- [iOS SDK](https://intl.cloud.tencent.com/document/product/436/31467)
- [Java SDK](https://intl.cloud.tencent.com/document/product/436/31468)
- [Node.js SDK](https://intl.cloud.tencent.com/document/product/436/31469)
- [PHP SDK](https://intl.cloud.tencent.com/document/product/436/31470)
- [Python SDK](https://intl.cloud.tencent.com/document/product/436/31471)
- [미니프로그램 SDK](https://intl.cloud.tencent.com/document/product/436/30609)

