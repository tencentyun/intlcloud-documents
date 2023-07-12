## 적용 시나리오

Tencent Cloud COS는 객체 일괄 삭제를 지원합니다. 콘솔, API, SDK 등 다양한 방식으로 객체 일괄 삭제를 진행할 수 있습니다.

삭제 작업이 성공적으로 이뤄진 경우 일반적으로 반환 내용이 없습니다. 오류가 발생할 경우 오류 정보를 반환합니다.

>!1회당 최대 객체 1000개의 삭제 요청이 가능하며 더 많은 객체 삭제가 필요한 경우 리스트를 분할하여 요청을 보내십시오.

## 사용 방법

### COS 콘솔 사용

COS 콘솔을 통해 여러 객체를 일괄 삭제할 수 있습니다. 자세한 내용은 [객체 삭제](https://intl.cloud.tencent.com/document/product/436/13323) 콘솔 가이드 문서를 참조하십시오.

### REST API 사용

REST API를 통해 즉각적으로 객체 일괄 삭제 요청을 보낼 수 있습니다. 자세한 내용은 [DELETE Multiple Objects](https://intl.cloud.tencent.com/document/product/436/8289) API 문서를 참조하십시오.

### SDK 사용

SDK 호출을 통해 즉각적으로 객체 일괄 삭제를 진행할 수 있습니다. 자세한 내용은 다음 언어별 SDK 문서를 참조하십시오.

- [Android SDK](https://intl.cloud.tencent.com/document/product/436/37674)
- [C SDK](https://intl.cloud.tencent.com/document/product/436/31518)
- [C++ SDK](https://intl.cloud.tencent.com/document/product/436/31522)
- [.NET SDK](https://intl.cloud.tencent.com/document/product/436/38065)
- [Go SDK](https://intl.cloud.tencent.com/document/product/436/31526)
- [iOS SDK](https://intl.cloud.tencent.com/document/product/436/37683)
- [Java SDK](https://intl.cloud.tencent.com/document/product/436/31534)
- [JavaScript SDK](https://intl.cloud.tencent.com/document/product/436/31538)
- [Node.js SDK](https://intl.cloud.tencent.com/document/product/436/31710)
- [PHP SDK](https://intl.cloud.tencent.com/document/product/436/31542)
- [Python SDK](https://intl.cloud.tencent.com/document/product/436/31546)
- [Mini Program SDK](https://www.tencentcloud.com/document/product/436/43884)
