## 소개

본문은 객체를 업로드할 때 서버측 암호화를 활성화하는 방법을 설명합니다. 서버측 암호화에 사용할 수 있는 키는 다음 세 가지로 나뉩니다.

* COS 호스팅 암호화 키
* 고객 제공 암호화 키
* KMS 호스팅 암호화 키


## SDK API 참고

SDK 모든 인터페이스의 구체적인 매개변수와 방법 설명은 [SDK API](https://cos-ios-sdk-doc-1253960454.file.myqcloud.com/)를 참고하십시오.

### COS에서 호스팅하는 암호화 키를 사용한 서버 암호화(SSE-COS)로 데이터 보호

#### 기능 설명

Tencent Cloud COS에서 마스터 키를 호스팅하고 데이터를 관리합니다. COS는 데이터센터에 데이터를 쓸 때 자동으로 암호화하며, 해당 데이터 사용 시 자동으로 복호화합니다. 현재 COS의 마스터 키를 사용한 AES-256 데이터 암호화를 지원합니다.

#### 예시 코드
**Objective-C**

[//]: # (.cssg-snippet-put-object-sse)
```objective-c
QCloudCOSXMLUploadObjectRequest *request = [QCloudCOSXMLUploadObjectRequest new];
[request setCOSServerSideEncyption];
```

>?전체 예시는 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Objc/Examples/cases/PutObjectSSE.m)를 참고하십시오.

**Swift**

[//]: # (.cssg-snippet-put-object-sse)
```swift
request.setCOSServerSideEncyption();
```

>?더 많은 전체 예시는 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Swift/Examples/cases/PutObjectSSE.swift)를 참고하십시오.

### 고객이 제공한 암호화 키를 사용한 서버 암호화(SSE-C)로 데이터 보호

#### 기능 설명

암호화 키는 사용자가 직접 제공하는 것이며, 객체를 업로드할 때 COS는 사용자가 제공한 암호화 키로 사용자의 데이터에 AES-256 암호화를 적용합니다.

> !
>- 해당 암호화로 실행되는 서비스는 HTTPS를 사용해 요청해야 합니다.
>- 숫자, 문자 및 부호의 조합인 32바이트 문자열을 키로 제공해야 하며 중국어는 지원되지 않습니다.
>- 파일이 업로드될 때 키 암호화를 설정한 경우 GET(다운로드) 또는 HEAD(쿼리) 요청에 동일한 키를 포함해야 정상적으로 응답됩니다.

#### 예시 코드
**Objective-C**

[//]: # (.cssg-snippet-put-object-sse-c)
```objective-c
QCloudCOSXMLUploadObjectRequest *request = [QCloudCOSXMLUploadObjectRequest new];
NSString *customKey = @"123456qwertyuioplkjhgfdsazxcvbnm";
[request setCOSServerSideEncyptionWithCustomerKey:customKey];
```

>? 전체 예시는 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Objc/Examples/cases/PutObjectSSE.m)를 참고하십시오.
>

**Swift**

[//]: # (.cssg-snippet-put-object-sse-c)
```swift
let customKey = "123456qwertyuioplkjhgfdsazxcvbnm";
request.setCOSServerSideEncyptionWithCustomerKey(customKey);
```

>? 더 많은 전체 예시는 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Swift/Examples/cases/PutObjectSSE.swift)를 참고하십시오.
>

### KMS에서 호스팅하는 암호화 키를 사용한 서버 암호화(SSE-KMS)로 데이터 보호

#### 기능 설명

SSE-KMS 암호화는 KMS가 키를 호스팅하여 관리하는 서버 암호화 방식입니다. KMS는 Tencent Cloud가 선보인 보안 관리형 서비스로서 3rd party가 인증하는 하드웨어 보안 모듈(HSM, Hardware Security Module)로 보안키를 생성하여 보호합니다. KMS로 보안키를 간편하게 생성하고 관리할 수 있어 다양한 애플리케이션과 작업에 필요한 보안키 관리가 편리할 뿐만 아니라 모니터링과 컴플라이언스 니즈를 충족할 수 있습니다. KMS 서비스 활성화 방법은 [서버 암호화 개요](https://intl.cloud.tencent.com/document/product/436/18145)를 참고하십시오.

#### 예시 코드
**Objective-C**

[//]: # (.cssg-snippet-put-object-sse-kms)
```objective-c
QCloudCOSXMLUploadObjectRequest *request = [QCloudCOSXMLUploadObjectRequest new];
NSString *customKey = @"123456qwertyuioplkjhgfdsazxcvbnm";
NSString *arrJsonStr = @"{\"key\":\"value\"}";
[request setCOSServerSideEncyptionWithKMSCustomKey:customKey jsonStr:arrJsonStr];
```

>? 전체 예시는 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Objc/Examples/cases/PutObjectSSE.m)를 참고하십시오.
>

**Swift**

[//]: # (.cssg-snippet-put-object-sse-kms)
```swift
let customKey = "123456qwertyuioplkjhgfdsazxcvbnm";
let arrJsonStr = "{\"key\":\"value\"}";
self.advancedRequest?.setCOSServerSideEncyptionWithKMSCustomKey(customKey, jsonStr: arrJsonStr);
```

>? 더 많은 전체 예시는 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Swift/Examples/cases/PutObjectSSE.swift)를 참고하십시오.
>
