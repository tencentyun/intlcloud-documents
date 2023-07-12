## 적용 시나리오

복제 작업은 단일 요청에서 최대 5GB의 COS(Cloud Object Storage) 객체 사본을 작성합니다. 5GB가 넘는 객체를 복제하려면 [멀티파트 복제](https://intl.cloud.tencent.com/document/product/436/14118) API를 사용하십시오. 복제 작업으로 다음을 수행할 수 있습니다.

- 객체의 복제본을 생성합니다.
- 객체를 복제하고 원래 객체를 삭제하여 객체 이름을 바꿉니다.
- 객체의 스토리지 클래스를 수정합니다. 소스 및 대상 모두로 동일한 객체 키를 선택하고 스토리지 클래스를 수정할 수 있습니다.
- 각각 다른 Tencent Cloud COS 리전에서 객체를 복제합니다.
- 객체 메타데이터를 수정합니다. 소스 및 대상 모두로 동일한 객체 키를 선택하고 객체 메타데이터를 수정할 수 있습니다.

복제 작업에서 원본 객체의 메타데이터는 기본적으로 상속되지만 생성 날짜는 대상 객체의 생성 날짜에 따릅니다.

>?
>- ARCHIVE 스토리지 클래스의 객체는 복제 및 붙여넣기가 지원되지 않습니다.
>- MAZ 버킷의 객체는 OAZ 버킷에 복제할 수 없습니다.
>- 서브 계정에는 PutObject, GetObject, GetObjectACL 객체 복제 권한이 부여되어야 합니다.

## 사용 방법

### COS 콘솔 사용

COS 콘솔에서 객체를 복제합니다. 자세한 내용은 콘솔 가이드의 [객체 복사](https://intl.cloud.tencent.com/document/product/436/33456)를 참고하십시오.

### REST API 사용

REST API를 사용해 객체 복제 요청을 시작합니다. 자세한 내용은 [PUT Object - Copy](https://intl.cloud.tencent.com/document/product/436/10881)를 참고하십시오.

### SDK 사용

SDK에서 객체 복제 메소드를 직접 호출합니다. 자세한 내용은 아래의 해당 프로그래밍 언어에 대한 SDK 설명서를 참고하십시오.

- [Android SDK](https://intl.cloud.tencent.com/document/product/436/40494)
- [C SDK](https://intl.cloud.tencent.com/document/product/436/44872)
- [C++ SDK](https://intl.cloud.tencent.com/document/product/436/31522)
- [.NET SDK](https://intl.cloud.tencent.com/document/product/436/40171)
- [Go SDK](https://intl.cloud.tencent.com/document/product/436/44064)
- [iOS SDK](https://intl.cloud.tencent.com/document/product/436/40495)
- [Java SDK](https://intl.cloud.tencent.com/document/product/436/44019)
- [JavaScript SDK](https://intl.cloud.tencent.com/document/product/436/43865)
- [Node.js SDK](https://intl.cloud.tencent.com/document/product/436/43874)
- [PHP SDK](https://intl.cloud.tencent.com/document/product/436/45498)
- [Python SDK](https://intl.cloud.tencent.com/document/product/436/46470)
- [미니프로그램 SDK](https://intl.cloud.tencent.com/document/product/436/43885)
