## 적용 시나리오

기본적으로 버킷과 객체는 개인 소유입니다. 3rd party가 버킷에 객체를 업로드할 수 있지만 CAM 계정 혹은 임시 키 사용을 원치 않는 경우 임시 업로드 작업을 완료하기 위해 URL 사전 서명을 사용해 3rd party에게 서명을 제출합니다. 유효한 서명 URL을 받은 계정은 모두 객체 업로드를 진행할 수 있습니다.

URL 사전 서명 시 서명에 객체 키를 설정하여 지정한 객체 키만 업로드할 수 있도록 허용합니다. 절차에서 사전 서명 URL의 유효 기간을 지정하여 해당 URL 기간 만료 후 사용 권한이 없는 계정의 사용을 막을 수 있습니다.

## 사용 방법

### SDK 사용

SDK에서 사전 서명된 URL 메서드를 직접 호출할 수 있습니다. 자세한 내용은 다음 언어별 SDK 문서를 참조하십시오.

- [Android SDK](https://intl.cloud.tencent.com/document/product/436/37680)
-  [C SDK](https://intl.cloud.tencent.com/document/product/436/31520)
- [C++ SDK](https://intl.cloud.tencent.com/document/product/436/31524)
- [.NET SDK](https://intl.cloud.tencent.com/document/product/436/38068)
- [Go SDK](https://intl.cloud.tencent.com/document/product/436/31528)
- [iOS SDK](https://intl.cloud.tencent.com/document/product/436/37690)
- [Java SDK](https://intl.cloud.tencent.com/document/product/436/31536)
- [JavaScript SDK](https://intl.cloud.tencent.com/document/product/436/31540)
- [Node.js SDK](https://intl.cloud.tencent.com/document/product/436/32455)
- [PHP SDK](https://intl.cloud.tencent.com/document/product/436/31544)
- [Python SDK](https://intl.cloud.tencent.com/document/product/436/31548)
