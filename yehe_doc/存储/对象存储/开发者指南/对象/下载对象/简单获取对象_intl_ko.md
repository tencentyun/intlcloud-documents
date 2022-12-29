## 적용 시나리오

COS(Cloud Object Storage)의 객체 얻기 요청을 실행할 수 있습니다. 객체 얻기는 아래 기능을 지원합니다.

- 완전한 단일 객체 얻기: GET 요청을 통해 완전한 객체 데이터를 얻을 수 있습니다.
- 단일 객체의 일부 콘텐츠 얻기: GET 요청에서 Range 요청 헤더를 전송할 수 있습니다. 특정 바이트 범위 인덱스는 지원하지만 다중 범위 인덱스는 지원하지 않습니다.

객체의 메타데이터는 HTTP 응답 헤더로써 객체 콘텐츠와 함께 반환되며, GET 요청은 URL 매개변수를 사용하여 응답한 일부 메타데이터 값 덮어쓰기를 지원합니다.
예를 들어 Content-Disposition 응답 값이 있으며, 수정을 지원하는 응답 헤더는 다음과 같습니다.
- Content-Type
- Content-Language
- Expires
- Cache-Control
- Content - Disposition
- Content-Encoding

## 사용 방법

### COS 콘솔 사용

COS 콘솔을 이용해 객체를 얻을 수 있습니다. 자세한 내용은 [객체 다운로드](https://intl.cloud.tencent.com/document/product/436/13322) 콘솔 가이드 문서를 참조하십시오.

### REST API 사용

REST API를 이용해 객체 얻기 요청을 실행할 수 있습니다. 자세한 내용은 [GET Object](https://intl.cloud.tencent.com/document/product/436/7753) API 문서를 참조하십시오.

### SDK 사용

SDK의 객체 다운로드 방식을 호출할 수 있습니다. 자세한 내용은 아래 언어별 SDK 문서를 참조하십시오.

- [Android SDK](https://intl.cloud.tencent.com/document/product/436/37675#.E4.B8.8B.E8.BD.BD.E5.AF.B9.E8.B1.A1)
- [C SDK](https://intl.cloud.tencent.com/document/product/436/31464#.E4.B8.8B.E8.BD.BD.E5.AF.B9.E8.B1.A1)
- [C++ SDK](https://intl.cloud.tencent.com/document/product/436/31465#.E4.B8.8B.E8.BD.BD.E5.AF.B9.E8.B1.A1)
- [.NET SDK](https://intl.cloud.tencent.com/document/product/436/30594)
- [Go SDK](https://intl.cloud.tencent.com/document/product/436/31466#.E4.B8.8B.E8.BD.BD.E5.AF.B9.E8.B1.A1)
- [iOS SDK](https://intl.cloud.tencent.com/document/product/436/37684#.E8.8E.B7.E5.8F.96.E5.AF.B9.E8.B1.A1)
- [Java SDK](https://intl.cloud.tencent.com/document/product/436/31468#.E4.B8.8B.E8.BD.BD.E5.AF.B9.E8.B1.A1)
- [JavaScript SDK](https://intl.cloud.tencent.com/document/product/436/31477#.E4.B8.8B.E8.BD.BD.E5.AF.B9.E8.B1.A1)
- [Node.js SDK](https://intl.cloud.tencent.com/document/product/436/31469#.E4.B8.8B.E8.BD.BD.E5.AF.B9.E8.B1.A1)
- [PHP SDK](https://intl.cloud.tencent.com/document/product/436/31470#.E4.B8.8B.E8.BD.BD.E5.AF.B9.E8.B1.A1)
- [Python SDK](https://intl.cloud.tencent.com/document/product/436/31471#.E4.B8.8B.E8.BD.BD.E5.AF.B9.E8.B1.A1)
- [Mini Program SDK](https://www.tencentcloud.com/document/product/436/43882)
