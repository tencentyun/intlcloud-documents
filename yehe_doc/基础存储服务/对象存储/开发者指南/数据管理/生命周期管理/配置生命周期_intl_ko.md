## 적용 시나리오

라이프사이클 설정을 통해 규칙에 부합한 객체가 지정된 조건 하에 일부 조작을 자동 수행할 수 있습니다. 예시:

- 스토리지 유형 전환: 생성된 객체를 지정 시간 후 표준IA 스토리지 유형(STANDARD_IA), INTELLIGENT TIERING(INTELLIGENT_TIERING), CAS(ARCHIVE) 유형 및 DEEP ARCHIVE로 전환할 수 있습니다.
- 만료 삭제: 객체의 만료시간을 설정하면 객체가 만료된 후 자동으로 삭제됩니다.

자세한 내용은 [라이프사이클 개요](https://intl.cloud.tencent.com/document/product/436/17028) 문서 및 [라이프사이클 설정 요소](https://intl.cloud.tencent.com/document/product/436/17029) 문서를 참조하십시오.

## 사용 방법

### COS 콘솔 사용

COS 스토리지 콘솔을 사용해 라이프사이클을 설정할 수 있습니다. 자세한 내용은 [라이프사이클 설정](https://intl.cloud.tencent.com/document/product/436/14605) 콘솔 가이드 문서를 참조해 주십시오.

### REST API 사용

REST API를 직접 사용해 버킷 중 객체의 라이프사이클을 설정 및 관리할 수 있습니다. 자세한 내용은 다음 API 문서를 참조해 주십시오.

- [PUT Bucket lifecycle](https://intl.cloud.tencent.com/document/product/436/8280)
- [GET Buket lifecycle](https://intl.cloud.tencent.com/document/product/436/8278)
- [DELETE Bucket lifecycle](https://intl.cloud.tencent.com/document/product/436/8284)

### SDK 사용

SDK의 라이프사이클을 직접 호출할 수 있습니다. 자세한 내용은 아래 각 언어로 된 SDK 문서를 참조해 주십시오.

- [Android SDK](https://intl.cloud.tencent.com/document/product/436/36197)
- [C SDK](https://intl.cloud.tencent.com/document/product/436/31519#.E7.94.9F.E5.91.BD.E5.91.A8.E6.9C.9F)
- [C++ SDK](https://intl.cloud.tencent.com/document/product/436/12301)
- [.NET SDK](https://intl.cloud.tencent.com/document/product/436/35269)
- [Go SDK](https://intl.cloud.tencent.com/document/product/436/39152)
- [iOS SDK](https://intl.cloud.tencent.com/document/product/436/37855)
- [Java SDK](https://intl.cloud.tencent.com/document/product/436/10199)
- [JavaScript SDK](https://intl.cloud.tencent.com/document/product/436/35806)
- [Node.js SDK](https://intl.cloud.tencent.com/document/product/436/35860)
- [PHP SDK](https://intl.cloud.tencent.com/document/product/436/35002)
- [Python SDK](https://intl.cloud.tencent.com/document/product/436/31547)
- [Mini Program SDK](https://www.tencentcloud.com/document/product/436/35851)
