## 적용 시나리오

COS(Cloud Object Storage)에서 객체 다운로드 요청을 직접 시작할 수 있습니다. 다음 기능이 지원됩니다.

- 전체 객체 다운로드: GET 요청을 시작하여 전체 객체 데이터를 다운로드합니다.
- 객체의 일부 다운로드: GET 요청에서 Range 요청 헤더를 사용하여 객체의 특정 바이트 범위를 검색합니다. 여러 범위 검색은 지원되지 않습니다.

객체의 메타데이터는 객체의 콘텐츠와 함께 HTTP 응답 헤더로 반환됩니다. GET 요청은 URL 매개변수를 사용하여 응답에서 특정 메타데이터 값 덮어쓰기를 지원합니다.
예를 들어 Content-Disposition의 응답 값을 덮어쓸 수 있습니다. 수정을 지원하는 응답 헤더는 다음과 같습니다.
- Content-Type
- Content-Language
- Expires
- Cache-Control
- Content - Disposition
- Content-Encoding

## 사용 방법

### COS 콘솔 사용

COS 콘솔에서 객체를 다운로드합니다. 자세한 내용은 콘솔 가이드의 [객체 다운로드](https://intl.cloud.tencent.com/document/product/436/13322)를 참고하십시오.

### REST API 사용

REST API를 사용하여 객체 다운로드 요청을 시작합니다. 자세한 내용은 [GET Object](https://intl.cloud.tencent.com/document/product/436/7753)를 참고하십시오.

### SDK 사용

SDK에서 객체 다운로드 메소드를 직접 호출합니다. 자세한 내용은 아래의 해당 프로그래밍 언어에 대한 SDK 문서를 참고하십시오.

- [Android SDK](https://intl.cloud.tencent.com/document/product/436/37675)
- [C SDK](https://intl.cloud.tencent.com/document/product/436/44873)
- [C++ SDK](https://intl.cloud.tencent.com/document/product/436/31522)
- [.NET SDK](https://intl.cloud.tencent.com/document/product/436/30594)
- [Go SDK](https://intl.cloud.tencent.com/document/product/436/44065)
- [iOS SDK](https://intl.cloud.tencent.com/document/product/436/37684)
- [Java SDK](https://intl.cloud.tencent.com/document/product/436/44016)
- [JavaScript SDK](https://intl.cloud.tencent.com/document/product/436/43862)
- [Node.js SDK](https://intl.cloud.tencent.com/document/product/436/43872)
- [PHP SDK](https://intl.cloud.tencent.com/document/product/436/45499)
- [Python SDK](https://intl.cloud.tencent.com/document/product/436/46469)
- [미니프로그램 SDK](https://intl.cloud.tencent.com/document/product/436/43882)

