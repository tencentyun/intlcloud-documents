간편 업로드란 PUT Object 인터페이스를 사용해 객체를 업로드하는 것을 의미하며, 5GB 이하 단일 객체 업로드 요청에 사용됩니다.

5GB를 초과하는 단일 객체는 다음 방법을 사용하여 업로드할 수 있습니다.

- 콘솔을 통한 업로드: 콘솔을 이용해 최대 512GB의 단일 객체를 업로드할 수 있습니다. 자세한 내용은 [객체 업로드](https://intl.cloud.tencent.com/document/product/436/13321) 콘솔 가이드 문서를 참조하십시오.
- API/SDK를 통한 멀티파트 업로드: 최대 48.82TB(50000GB)의 단일 객체를 업로드할 수 있습니다. 자세한 내용은 [멀티파트 업로드](https://intl.cloud.tencent.com/document/product/436/14112)를 참조하십시오.
- COSCMD 툴을 사용해 최대 40TB의 단일 객체를 업로드할 수 있습니다. 자세한 내용은 [COSCMD 툴](https://intl.cloud.tencent.com/document/product/436/10976)을 참조하십시오.

>? 지정된 폴더 또는 경로로 업로드를 요청하는 경우 `/`를 사용할 수 있습니다(예시: picture.png를 doc 폴더에 업로드 하는 경우 객체 키를 doc/picture.png로 설정).
>

## 적용 시나리오

간편 업로드는 5GB 이하의 객체 업로드에 활용할 수 있습니다.

고대역폭 혹은 약한 네트워크 환경에서 업로드하는 객체 크기가 큰 경우(100MB 이상~5GB 이하인 경우) 우선적으로 [멀티파트 업로드](https://intl.cloud.tencent.com/document/product/436/14112) 사용을 권장합니다. 멀티파트 업로드는 여러 개의 파트가 병렬 전송되며, 고대역폭 환경에서 리소스를 효과적으로 이용할 수 있습니다. 약한 네트워크 환경에서 단일 파트 업로드에 실패한 경우, 이미 업로드된 다른 파트에 영향을 주지 않기 때문에 실패한 부분만 다시 업로드하여 전체 업로드 성공률을 높여 줍니다. 약한 네트워크 환경에서의 모바일 업로드에 대한 자세한 내용은 [약한 네트워크에서의 멀티파트 업로드 재개 실행](https://intl.cloud.tencent.com/document/product/436/30932)을 참조하십시오.


## 사용 방법

### REST API 사용

REST API를 통해 직접 객체 간편 업로드 요청을 보낼 수 있습니다. 자세한 내용은 [PUT Object](https://intl.cloud.tencent.com/document/product/436/7749) API 문서를 참조하십시오.

### SDK 사용
SDK 호출을 통해 직접 객체 간편 업로드를 진행할 수 있습니다. 자세한 내용은 다음 언어별 SDK 문서를 참조하십시오.
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


