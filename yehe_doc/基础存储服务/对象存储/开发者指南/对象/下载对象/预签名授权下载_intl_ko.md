## 사용 사례

버킷과 객체는 기본적으로 개인 소유입니다. 3rd party가 객체를 다운로드할 수 있도록 허용하지만 CAM 계정 또는 임시 키 사용을 제한하고 싶은 경우, URL 사전 서명 방식으로 3rd party에 서명을 제출함으로써 다운로드 작업을 완료할 수 있습니다. 유효한 URL 사전 서명을 받은 계정은 모두 객체 다운로드를 진행할 수 있습니다.

URL 사전 서명 시 서명에 객체 키를 설정하여 지정한 객체만 다운로드할 수 있도록 허용합니다. 또한 프로세스에서 URL 사전 서명 유효 기간을 지정하여, 해당 기간 만료 후 권한이 없는 계정의 사용을 제한할 수 있습니다.

>!
> - CDN 도메인 이름에 액세스하려면 CDN 인증 프로세스를 따라야 하며, COS 서명을 사용할 수 없으므로 사전 서명된 URL은 CDN 도메인 이름을 사용할 수 없습니다.
> - 사용자는 임시 키를 사용하여 사전 서명을 생성하고, 임시 승인을 통해 사전 서명 업로드 및 다운로드 요청의 보안성을 강화할 것을 권장합니다. 임시 키 신청 시, [최소 권한의 원칙 관련 가이드](https://intl.cloud.tencent.com/document/product/436/32972)를 준수하여 타깃 버킷이나 객체 이외의 리소스가 유출되지 않도록 하시기 바랍니다.
> - 사전 서명을 생성하기 위해 영구 키를 사용해야 하는 경우 위험을 방지하기 위해 영구 키의 권한 범위를 업로드 또는 다운로드 작업으로 제한하는 것이 좋습니다. 그리고 생성된 서명의 유효 기간은 업로드 또는 다운로드 작업을 완료하는 데 필요한 가장 짧은 기간으로 설정합니다. 지정된 사전 서명된 URL의 유효 기간이 만료되면 요청이 중단되기 때문에 새 서명을 신청한 후 실패한 요청은 다시 실행해야 하며, 체크포인트 재시작을 지원하지 않습니다.
> 


## 사용 방법

### SDK 사용

SDK의 URL 사전 서명 방식을 호출할 수 있습니다. 자세한 내용은 다음 언어별 SDK 문서를 참조하십시오.

- [Android SDK](https://intl.cloud.tencent.com/document/product/436/37680)
- [C SDK](https://intl.cloud.tencent.com/document/product/436/31520)
- [C++ SDK](https://intl.cloud.tencent.com/document/product/436/31524)
- [.NET SDK](https://intl.cloud.tencent.com/document/product/436/38068)
- [Flutter SDK](https://www.tencentcloud.com/document/product/436/54513)
- [Go SDK](https://intl.cloud.tencent.com/document/product/436/31528)
- [iOS SDK](https://intl.cloud.tencent.com/document/product/436/37690)
- [Java SDK](https://intl.cloud.tencent.com/document/product/436/31536)
- [JavaScript SDK](https://intl.cloud.tencent.com/document/product/436/31540)
- [Node.js SDK](https://intl.cloud.tencent.com/document/product/436/32455)
- [PHP SDK](https://intl.cloud.tencent.com/document/product/436/31544)
- [Python SDK](https://intl.cloud.tencent.com/document/product/436/31548)
- [React Native SDK](https://www.tencentcloud.com/document/product/436/54312)
- [미니프로그램 SDK](https://intl.cloud.tencent.com/document/product/436/31711)
