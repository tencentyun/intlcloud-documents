## 소개

본문은 버킷 Referer 에 대한 얼로우/블록리스트의 API 개요 및 SDK 예시 코드를 제공합니다.

| API                                                          | 작업 이름         | 작업 설명                   |
| ------------------------------------------------------------ | -------------- | -------------------------- |
| [PUT Bucket referer](https://intl.cloud.tencent.com/document/product/436/31423) | 버킷 Referer 설정 | 버킷 Referer 얼로우 또는 블록리스트 설정 |
| [GET Bucket referer](https://intl.cloud.tencent.com/document/product/436/30615) | 버킷 Referer 쿼리 | 버킷 Referer 얼로우 또는 블록리스트 쿼리 |

## SDK API 참고

SDK 모든 인터페이스의 구체적인 매개변수와 방법 설명은 [SDK API](https://cos-ios-sdk-doc-1253960454.file.myqcloud.com/)를 참고하십시오.

## 버킷 Referer 설정

#### 기능 설명  

버킷의 Referer의 얼로우 또는 블록리스트를 설정합니다(PUT Bucket referer).

>! COS iOS SDK 버전은 v5.9.6 이상이어야 합니다.
>

#### 요청 예시
**Objective-C**

[//]: # ".cssg-snippet-put-bucket-referer"
```objective-c
QCloudPutBucketRefererRequest* request = [QCloudPutBucketRefererRequest new];

// 링크 도용 방지 유형, 열거 값: Black-List, White-List
request.refererType = QCloudBucketRefererTypeBlackList;

// 링크 도용 방지 활성화 여부, 열거 값: Enabled, Disabled
request.status = QCloudBucketRefererStatusEnabled;

// 빈 Referer 액세스 허용 여부, 열거 값: Allow, Deny, 기본값은 Deny
request.configuration = QCloudBucketRefererConfigurationDeny;

// 적용 도메인 리스트. 여러 도메인 및 접두사 매칭 지원, 포트가 있는 도메인 및 IP 지원, 와일드카드* 지원, 2단계 수준 도메인 또는 다중 단계 도메인에 대해 와일드카드 수행
request.domainList = @[@"*.com",@"*.qq.com"];

// BucketName-APPID 형식의 버킷 이름
request.bucket = @"examplebucket-1250000000";

[request setFinishBlock:^(id outputObject, NSError *error) {
    if (error){
        // 링크 도용 방지 추가 실패
    }else{
        // 링크 도용 방지 추가 실패
    }

}];
[[QCloudCOSXMLService defaultCOSXML] PutBucketReferer:request];
```

>? 전체 예시는 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Objc/Examples/cases/BucketReferer.m)를 참고하십시오.
>

**Swift**

[//]: # ".cssg-snippet-put-bucket-referer"
```swift
let request = QCloudPutBucketRefererRequest.init();

// 링크 도용 방지 유형, 열거 값: Black-List, White-List
request.refererType = QCloudBucketRefererType.blackList;

// 링크 도용 방지 활성화 여부, 열거 값: Enabled, Disabled
request.status = QCloudBucketRefererStatus.enabled;

// 빈 Referer 액세스 허용 여부, 열거 값: Allow, Deny, 기본값: Deny
request.configuration = QCloudBucketRefererConfiguration.allow;

// 적용 도메인 리스트. 여러 도메인 및 접두사 매칭 지원, 포트가 있는 도메인 및 IP 지원, 와일드카드* 지원, 2단계 수준 도메인 또는 다중 단계 도메인에 대해 와일드카드 수행
request.domainList = ["*.com","*.qq.com"];

// BucketName-APPID 형식의 버킷 이름
request.bucket = "examplebucket-1250000000";

request.finishBlock = {(result,error) in
    if (error != nil){
        // 링크 도용 방지 추가 실패
    }else{
        // 링크 도용 방지 추가 실패
    }
}
QCloudCOSXMLService.defaultCOSXML().putBucketReferer(request);
```

>? 전체 예시는 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Swift/Examples/cases/BucketReferer.swift)를 참고하십시오.
>
## 버킷 Referer 쿼리

#### 기능 설명

버킷의 Referer의 얼로우 또는 블록리스트를 쿼리합니다(PUT Bucket referer).

>! COS iOS SDK 버전은 v5.9.6 이상이어야 합니다.
>


#### 요청 예시
**Objective-C**

[//]: # ".cssg-snippet-get-bucket-referer"
```objective-c
QCloudGetBucketRefererRequest* request = [QCloudGetBucketRefererRequest new];

// BucketName-APPID 형식의 버킷 이름
request.bucket = @"examplebucket-1250000000";

[request setFinishBlock:^(QCloudBucketRefererInfo * outputObject, NSError *error) {
    // outputObject에서 요청한 링크 도용 방지. 자세한 필드는 api 문서 또는 SDK 소스 코드를 참고하십시오.
    // QCloudBucketRefererInfo 유형.
}];
[[QCloudCOSXMLService defaultCOSXML] GetBucketReferer:request];     
```
>?전체 예시는 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Objc/Examples/cases/BucketReferer.m)를 참고하십시오.

**Swift**

[//]: # ".cssg-snippet-get-bucket-referer"
```swift
let request = QCloudGetBucketRefererRequest.init();

// BucketName-APPID 형식의 버킷 이름
request.bucket = "examplebucket-1250000000";

request.finishBlock = {(result,error) in
    // outputObject에서 요청한 링크 도용 방지. 자세한 필드는 api 문서 또는 SDK 소스 코드를 참고하십시오.
    // QCloudBucketRefererInfo 유형.
}
QCloudCOSXMLService.defaultCOSXML().getBucketReferer(request);
```

>? 전체 예시는 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Swift/Examples/cases/BucketReferer.swift)를 참고하십시오.
>



