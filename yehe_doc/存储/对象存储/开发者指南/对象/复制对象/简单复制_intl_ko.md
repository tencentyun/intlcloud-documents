## 적용 시나리오

COS(Cloud Object Storage)에서 이미 저장된 객체를 간단한 복사 작업을 통해 신규 객체 복사본을 생성할 수 있습니다. 단일 작업 중, 최대 5GB의 객체를 복사할 수 있습니다. 객체가 5GB를 초과할 경우, 멀티파트 업로드 인터페이스를 사용해 복사해야 합니다. 객체 복사에는 다음과 같은 기능이 있습니다.

- 신규 객체 복사본을 생성합니다.
- 객체를 복사하고 이름을 수정한 뒤, 원본 객체를 삭제하여 이름 변경을 실행합니다.
- 객체의 스토리지 유형을 수정하는 경우, 복사 시 동일한 소스와 타깃의 객체 키를 선택하여 스토리지 유형을 수정합니다.
- 각각 다른 Tencent Cloud COS 리전에서 객체를 복사합니다.
- 객체의 메타데이터를 수정하는 경우, 복사 시 동일한 소스와 타깃 객체 키를 선택하고 해당 메타데이터를 수정합니다.

객체 복사 시, 기본적으로 원본 객체의 메타데이터를 상속받지만, 생성 날짜는 신규 객체 시간에 따라 계산됩니다.

>?
>- ARCHIVE 유형 객체의 복사 및 붙여넣기를 지원하지 않습니다.
>- 다중AZ 설정을 활성화한 버킷은 다중AZ 스토리지 유형을 단일 AZ 스토리지 유형으로 복사할 수 없습니다.
>- 서브 계정이 객체를 복사하려면 PutObject, GetObject, GetObjectACL의 3개 권한이 필요합니다.

## 사용 방법

### COS 콘솔 사용

COS 콘솔을 사용해 객체를 복사할 수 있습니다. 자세한 내용은 [객체 복사](https://intl.cloud.tencent.com/document/product/436/33456) 콘솔 가이드 문서를 참조하십시오.

### REST API 사용

직접 REST API를 사용해 객체 복사 요청을 실행할 수 있습니다. 자세한 내용은 [PUT Object - Copy](https://intl.cloud.tencent.com/document/product/436/10881) API 문서를 참조하십시오.

### SDK 사용

직접 SDK의 객체 설정 복사 방법을 호출할 수 있습니다. 자세한 내용은 아래 각 언어의 SDK 문서를 참조하십시오.

- [Android SDK](https://intl.cloud.tencent.com/document/product/436/37674)
- [C SDK](https://intl.cloud.tencent.com/document/product/436/31518)
- [C++ SDK](https://intl.cloud.tencent.com/document/product/436/31522)
- [.NET SDK](https://intl.cloud.tencent.com/document/product/436/38062)
- [Go SDK](https://intl.cloud.tencent.com/document/product/436/31526)
- [iOS SDK](https://intl.cloud.tencent.com/document/product/436/37683)
- [Java SDK](https://intl.cloud.tencent.com/document/product/436/31534)
- [JavaScript SDK](https://intl.cloud.tencent.com/document/product/436/31538)
- [Node.js SDK](https://intl.cloud.tencent.com/document/product/436/31710)
- [PHP SDK](https://intl.cloud.tencent.com/document/product/436/31542)
- [Python SDK](https://intl.cloud.tencent.com/document/product/436/31546)
- [미니프로그램 SDK](https://intl.cloud.tencent.com/document/product/436/32457)
