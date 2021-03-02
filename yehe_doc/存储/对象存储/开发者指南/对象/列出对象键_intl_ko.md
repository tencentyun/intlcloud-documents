## 적용 시나리오

Tencent Cloud COS는 접두사 순서에 따라 객체 키를 나열하므로, 객체 키에 `/`부호를 사용하여 기존의 파일 시스템과 유사한 계층적 구조를 구현할 수 있습니다. COS도 세퍼레이터에 따라 계층적 구조를 선택하고 조회할 수 있도록 지원합니다.

접두사의 UTF-8 이진법 순서에 따르거나, 접두사를 지정하여 객 체 키 리스트를 필터링하는 방법으로 단일 버킷의 모든 객체 키를 나열할 수 있습니다. 예를 들어, 매개변수 `t`를 넣어 `tencent`의 객체를 나열하면 `a` 또는 기타 부호를 접두사로 하는 객체는 건너뜁니다.

추가된 `/` 세퍼레이터에 따라 객체 키를 재구성할 수 있습니다. 접두사와 세퍼레이터를 결합하여 폴더 인덱스와 비슷한 기능을 구현할 수 있습니다.

Tencent Cloud COS가 단일 버킷에서 지원하는 객체 수량에는 제한이 없으므로, 객체 키 리스트가 매우 방대합니다. 편리하게 관리하기 위해 단일 객체 인터페이스를 나열하면 키 값을 최대 1000개 반환하며, 인디케이터를 반환하여 잘린 부분이 있는지 알려줍니다. 인디케이터와 세퍼레이터를 바탕으로 객체 키 나열 요청을 보내면 키 값을 나열하거나 필요한 콘텐츠를 찾을 수 있습니다.

## 사용 방법

### COS 콘솔 사용

COS 콘솔을 이용해 객체를 검색할 수 있습니다. 자세한 내용은 [객체 검색](https://intl.cloud.tencent.com/document/product/436/13325) 콘솔 가이드 문서를 참조하십시오.

### REST API 사용

REST API를 이용해 객체 키 리스트를 요청할 수 있습니다. 자세한 내용은 [GET Bucket](https://intl.cloud.tencent.com/document/product/436/7734) API 문서를 참조하십시오.

### SDK 사용

SDK의 객체 리스트 조회 방식을 호출할 수 있습니다. 자세한 내용은 아래 언어별 SDK 문서를 참조하십시오.

- [Android SDK](https://intl.cloud.tencent.com/document/product/436/31463#.E6.9F.A5.E8.AF.A2.E5.AF.B9.E8.B1.A1.E5.88.97.E8.A1.A8)
- [C SDK](https://intl.cloud.tencent.com/document/product/436/31464#.E6.9F.A5.E8.AF.A2.E5.AF.B9.E8.B1.A1.E5.88.97.E8.A1.A8)
- [C++ SDK](https://intl.cloud.tencent.com/document/product/436/31465#.E6.9F.A5.E8.AF.A2.E5.AF.B9.E8.B1.A1.E5.88.97.E8.A1.A8)
- [.NET SDK](https://intl.cloud.tencent.com/document/product/436/30594)
- [Go SDK](https://intl.cloud.tencent.com/document/product/436/31466#.E6.9F.A5.E8.AF.A2.E5.AF.B9.E8.B1.A1.E5.88.97.E8.A1.A8)
- [iOS SDK](https://intl.cloud.tencent.com/document/product/436/31467#.E8.8E.B7.E5.8F.96.E5.AF.B9.E8.B1.A1.E5.88.97.E8.A1.A8)
- [Java SDK](https://intl.cloud.tencent.com/document/product/436/31468#.E6.9F.A5.E8.AF.A2.E5.AF.B9.E8.B1.A1.E5.88.97.E8.A1.A8)
- [JavaScript SDK](https://intl.cloud.tencent.com/document/product/436/31477#.E6.9F.A5.E8.AF.A2.E5.AF.B9.E8.B1.A1.E5.88.97.E8.A1.A8)
- [Node.js SDK](https://intl.cloud.tencent.com/document/product/436/8629)
- [PHP SDK](https://intl.cloud.tencent.com/document/product/436/31470#.E6.9F.A5.E8.AF.A2.E5.AF.B9.E8.B1.A1.E5.88.97.E8.A1.A8)
- [Python SDK](https://intl.cloud.tencent.com/document/product/436/31471#.E6.9F.A5.E8.AF.A2.E5.AF.B9.E8.B1.A1.E5.88.97.E8.A1.A8)
- [미니프로그램 SDK](https://intl.cloud.tencent.com/document/product/436/30609)
