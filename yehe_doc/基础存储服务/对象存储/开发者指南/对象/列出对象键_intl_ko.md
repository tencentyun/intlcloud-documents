[객체 키(ObjectKey)](https://intl.cloud.tencent.com/document/product/436/13324)는 버킷에 있는 객체의 고유 식별자로, 일반적으로 파일 경로로 이해할 수 있습니다. 예를 들어 객체 키가 doc/picture.jpg라면, 이미지 파일 picture.jpg가 COS(Cloud Object Storage)의 doc 경로(또는 폴더)에 저장되어 있음을 의미합니다.

객체 키 나열은 지정한 객체 키에 따라 특정 객체를 불러오는 작업입니다. 이외에도 객체 키 접두사에 따라 객체를 불러올 수도 있습니다. 즉, 객체 키 앞 부분(예: doc)을 지정해 동일한 접두사인 doc를 가진 모든 객체를 불러올 수 있습니다.

## 적용 시나리오

Tencent Cloud COS는 접두사 순서에 따라 객체 키를 나열하므로, 객체 키에 `/`부호를 사용하여 기존의 파일 시스템과 유사한 계층적 구조를 구현할 수 있습니다. COS도 세퍼레이터에 따라 계층적 구조를 선택하고 조회할 수 있도록 지원합니다.

접두사의 UTF-8 이진법 순서에 따르거나, 접두사를 지정하고 객체 키를 필터링한 리스트를 선택하여 단일 버킷의 모든 객체 키를 나열할 수 있습니다. 예를 들어 매개변수 `t`를 추가하면 `tencent`의 객체를 나열하고 `a` 또는 기타 부호를 접두사로 하는 객체는 건너뜁니다.

추가한 `/` 세퍼레이터에 따라 객체 키를 재구성할 수 있습니다. 접두사와 세퍼레이터를 결합하여 폴더 인덱스와 비슷한 기능을 구현할 수 있습니다.

Tencent Cloud COS에는 단일 버킷의 객체 수량 제한이 없으므로, 객체 키 리스트가 매우 방대합니다. 편리한 관리를 위해 단일 객체 나열 인터페이스는 객체 리스트를 최대 1000개까지 반환하며, 동시에 인디케이터를 반환하여 잘린 부분이 있는지 알려줍니다. 잘린 부분이 있는 경우, 다음 페이지에 객체 리스트가 존재함을 표시합니다. 인디케이터와 세퍼레이터를 바탕으로 객체 키 나열 요청을 여러 번 전송해 모든 객체 키를 나열하거나 필요한 콘텐츠를 찾을 수 있습니다.

## 사용 방법

### COS 콘솔 사용

COS 콘솔을 이용해 객체를 검색할 수 있습니다. 자세한 내용은 [객체 검색](https://intl.cloud.tencent.com/document/product/436/13325) 콘솔 가이드 문서를 참조하십시오.

### REST API 사용

REST API를 이용해 객체 키 리스트를 요청할 수 있습니다. 자세한 내용은 [GET Bucket(List Objects)](https://intl.cloud.tencent.com/document/product/436/30614) API 문서를 참조하십시오.

### SDK 사용

직접 SDK의 객체 리스트 조회 방법을 호출할 수 있습니다. 자세한 내용은 아래 언어별 SDK 문서를 참조하십시오.

- [Android SDK](https://intl.cloud.tencent.com/document/product/436/37676)
- [C SDK](https://intl.cloud.tencent.com/document/product/436/31518)
- [C++ SDK](https://intl.cloud.tencent.com/document/product/436/31522)
- [.NET SDK](https://intl.cloud.tencent.com/document/product/436/30594)
- [Go SDK](https://intl.cloud.tencent.com/document/product/436/31526)
- [iOS SDK](https://intl.cloud.tencent.com/document/product/436/37685)
- [Java SDK](https://intl.cloud.tencent.com/document/product/436/31534)
- [JavaScript SDK](https://intl.cloud.tencent.com/document/product/436/31538)
- [Node.js SDK](https://intl.cloud.tencent.com/document/product/436/31710)
- [PHP SDK](https://intl.cloud.tencent.com/document/product/436/31542)
- [Python SDK](https://intl.cloud.tencent.com/document/product/436/31546)
- [미니프로그램 SDK](https://intl.cloud.tencent.com/document/product/436/32457)
