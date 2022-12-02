## 소개

**멀티파트 업로드**는 전체 객체를 여러 파트로 나누어 Cloud Object Storage(COS)에 멀티파트 업로드할 수 있습니다. 업로드 시 연속 일련번호에 따라 단일 업로드하거나 임의 순서대로 파트를 각각 업로드하면 마지막에 COS에서 파트 일련번호 순서대로 객체를 다시 결합합니다. 전송 실패한 파트가 생기더라도 재전송할 수 있으며 다른 파트나 콘텐츠 완성도에 영향을 주지 않습니다. 일반적으로 약한 네트워크 환경에서 단일 객체가 20MB보다 크면 우선적으로 멀티파트 업로드를 고려할 수 있으며 고대역폭에서는 100MB가 넘는 객체는 멀티파트 업로드를 진행합니다.

**멀티파트 업로드**는 큰 객체를 최대 10000개 파트로 분할할 수 있습니다. 분할한 파트의 크기는 일반적으로 1MB - 5GB입니다. 마지막 파트는 1MB보다 작을 수 있습니다.

>? 간단 업로드는 최대 5GB 파일까지 업로드할 수 있지만 멀티파트 업로드는 5GB 이상파일도 업로드 가능합니다.
>

## 적용 시나리오
멀티파트 업로드는 약한 네트워크 혹은 고대역폭 환경에서 크기가 비교적 큰 객체를 업로드할 경우 활용할 수 있습니다.

멀티파트 업로드의 장점은 다음과 같습니다.

- 약한 네트워크 환경에서 작은 크기의 파트로로 네트워크 연결 실패로 인한 업로드 중단 현상을 줄이고 객체 전송을 지속할 수 있습니다.
- 고대역폭 환경에서 객체 파트 동시 업로드 시 네트워크 대역폭을 충분히 이용할 수 있으며 비순차적 업로드가 최종 결합한 객체에 영향을 주지 않습니다.
- 멀티파트 업로드를 사용하면 언제든지 업로드를 중지하고 단일 대형 객체 업로드를 재개할 수 있습니다. 작업을 끝내지 않는 이상 작업 완료되지 않은 모든 객체는 언제든지 업로드를 지속할 수 있습니다.
- 멀티파트 업로드는 객체의 전체 크기를 모르는 상황에서 업로드할 때 활용하기도 합니다. 먼저 멀티파트 업로드를 진행한 후 객체를 결합하여 전체 크기를 얻을 수 있습니다.


## 사용 방법

### REST API 사용

REST API를 통해 즉각적으로 멀티파트 업로드 요청을 보낼 수 있습니다. 자세한 내용은 다음 API 문서를 참조하십시오.

- [Initiate Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7746)
- [Upload Part](https://intl.cloud.tencent.com/document/product/436/7750)
- [Complete Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7742)
- [Abort Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7740)

### SDK 사용

SDK 호출을 통해 즉각적으로 멀티파트 작업을 진행할 수 있습니다. 자세한 내용은 다음 언어별 SDK 문서를 참조하십시오.

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
- [Mini Program SDK](https://www.tencentcloud.com/document/product/436/43881)
