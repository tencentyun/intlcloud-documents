## 적용 시나리오

5GB 이상의 객체를 복사해야 할 때, 파트 복사 방법을 선택해 구현해야 합니다. 멀티파트 업로드한 API를 사용해 신규 객체를 생성하고 Upload Part - Copy 기능을 사용하여 x-cos-copy-source 헤더를 가져와 원본 객체를 지정합니다. 과정은 다음과 같습니다.

1. 멀티파트 업로드한 객체를 초기화합니다.
2. 원본 객체의 데이터를 복사하면 x-cos-copy-source-range 헤더를 지정할 수 있으며, 한 번에 최대 5GB의 데이터만 복사할 수 있습니다.
3. 멀티파트 업로드를 완성합니다.

>?Tencent Cloud COS가 제공하는 SDK를 사용하면 블록 복사 기능을 쉽게 수행할 수 있습니다.

## 사용 방법

### REST API 사용

REST API를 직접 사용해 블록 복사 요청을 실행할 수 있습니다. 다음 API 문서를 참조하십시오.

- [Initiate Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7746)
- [Upload Part - Copy](https://intl.cloud.tencent.com/document/product/436/8287)
- [Complete Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7742)
- [Abort Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7740)

### SDK 사용

SDK의 블록 복사 방법을 직접 호출할 수 있습니다. 아래 각 언어로 된 SDK 문서를 참조하십시오.


- [Android SDK](https://intl.cloud.tencent.com/document/product/436/37674#.E5.A4.8D.E5.88.B6.E5.88.86.E5.9D.97)
- [C SDK](https://www.tencentcloud.com/document/product/436/44872)
- [C++ SDK](https://intl.cloud.tencent.com/document/product/436/31522#.E5.A4.8D.E5.88.B6.E5.88.86.E5.9D.97)
- [.NET(C#) SDK](https://www.tencentcloud.com/document/product/436/40171)
- [Go SDK](https://www.tencentcloud.com/document/product/436/44064)
- [iOS SDK](https://intl.cloud.tencent.com/document/product/436/37683#.E5.A4.8D.E5.88.B6.E5.88.86.E5.9D.97)
- [Java SDK](https://intl.cloud.tencent.com/document/product/436/31534#.E5.A4.8D.E5.88.B6.E5.88.86.E5.9D.97)
- [JavaScript SDK](https://intl.cloud.tencent.com/document/product/436/31538#.E5.A4.8D.E5.88.B6.E5.88.86.E5.9D.97)
- [Node.js SDK](https://intl.cloud.tencent.com/document/product/436/31710#.E5.A4.8D.E5.88.B6.E5.88.86.E5.9D.97)
- [PHP SDK](https://intl.cloud.tencent.com/document/product/436/31542#.E5.A4.8D.E5.88.B6.E5.88.86.E5.9D.97)
- [Python SDK](https://intl.cloud.tencent.com/document/product/436/31546#.E5.A4.8D.E5.88.B6.E5.88.86.E5.9D.97)
- [Mini Program SDK](https://www.tencentcloud.com/document/product/436/43885)
