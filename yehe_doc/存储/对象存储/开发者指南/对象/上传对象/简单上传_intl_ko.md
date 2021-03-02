## 적용 시나리오

이 작업은 5GB 이하 객체 업로드의 단일 요청을 하는 경우 활용할 수 있습니다.

>
>1. 5GB 이상 객체를 업로드하는 경우 반드시 [멀티파트 업로드](https://intl.cloud.tencent.com/document/product/436/14112)를 사용해야 합니다.
>2. 고대역폭 혹은 약한 네트워크 환경에서 업로드하는 객체 크기가 100MB 이상(5GB보다는 적음) 등 비교적 크기가 큰 경우 우선적으로 [멀티파트 업로드](https://intl.cloud.tencent.com/document/product/436/14112) 사용을 권장합니다. 멀티파트 업로드는 여러 멀티파트 전송을 병행할 수 있습니다. 고대역폭 환경에서 리소스를 효과적으로 이용할 수 있습니다. 약한 네트워크 환경에서 단일 멀티파트 업로드를 실패한 경우 업로드 완료한 다른 멀티파트에 영향을 주지 않기 때문에 실패 건만 다시 업로드 시도하여 전체 업로드 성공률을 높입니다. 약한 네트워크 환경에서의 모바일 클라이언트 업로드 관련 사항은 [약한 네트워크에서의 멀티파트 업로드 재개 실행](https://intl.cloud.tencent.com/document/product/436/30932)을 참고하십시오.



## 사용 방법

### COS 콘솔 사용
COS 콘솔을 통해 객체를 업로드할 수 있습니다. 자세한 내용은 [객체 업로드](https://intl.cloud.tencent.com/document/product/436/13321) 콘솔 가이드 문서를 참조하십시오.

### REST API 사용

REST API를 통해 즉각적으로 객체 간단 업로드 요청을 보낼 수 있습니다. 자세한 내용은 [PUT Object](https://cloud.tencent.com/document/product/436/7749) API 문서를 참조하십시오.

### SDK 사용
SDK 호출을 통해 즉각적으로 객체 간단 업로드를 진행할 수 있습니다. 자세한 내용은 다음 언어별 SDK 문서를 참조하십시오.
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
