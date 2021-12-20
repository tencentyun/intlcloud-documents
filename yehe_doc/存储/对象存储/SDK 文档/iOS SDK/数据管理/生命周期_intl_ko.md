## 소개
본 문서는 라이프사이클에 대한 API 개요 및 SDK 예시 코드를 제공합니다.

| API                                                          | 작업 이름       | 작업 설명                     |
| ------------------------------------------------------------ | ------------ | ------------------------------ |
| [PUT Bucket lifecycle](https://intl.cloud.tencent.com/document/product/436/8280) | 라이프사이클 설정 | 버킷의 라이프사이클 관리 구성 설정 |
| [GET Bucket lifecycle](https://intl.cloud.tencent.com/document/product/436/8278) | 라이프사이클 쿼리| 버킷 라이프사이클 관리 설정 쿼리   |
| [DELETE Bucket lifecycle](https://intl.cloud.tencent.com/document/product/436/8284) | 라이프사이클 삭제 | 버킷 라이프사이클 관리 구성 삭제   |

## SDK API 참고

SDK 모든 인터페이스의 구체적인 매개변수와 방법 설명은 [SDK API](https://cos-ios-sdk-doc-1253960454.file.myqcloud.com/)를 참고하십시오.

## 라이프사이클 설정

#### 기능 설명

버킷의 라이프사이클을 설정하는 데 사용됩니다.

#### 예시 코드
**Objective-C**

[//]: # (.cssg-snippet-put-bucket-lifecycle)
```objective-c
QCloudPutBucketLifecycleRequest* request = [QCloudPutBucketLifecycleRequest new];

// BucketName-Appid로 구성된 버킷 이름. COS 콘솔에서 볼 수 있습니다. https://console.cloud.tencent.com/cos5/bucket
request.bucket = @"examplebucket-1250000000";
__block QCloudLifecycleConfiguration* lifecycleConfiguration =
[[QCloudLifecycleConfiguration alloc] init];

// 규칙 설명
QCloudLifecycleRule* rule = [[QCloudLifecycleRule alloc] init];

// 규칙을 고유하게 식별하는 데 사용됩니다.
rule.identifier = @"identifier";

// 규칙의 활성화 여부를 나타냅니다. 열거 값: Enabled, Disabled
rule.status = QCloudLifecycleStatueEnabled;

// Filter는 규칙의 영향을 받는 Object 집합을 설명하는 데 사용됩니다.
QCloudLifecycleRuleFilter* filter = [[QCloudLifecycleRuleFilter alloc] init];

// 규칙이 적용되는 접두사를 지정합니다. 접두사와 일치하는 객체는 이 규칙의 영향을 받으며 Prefix는 최대 하나일 수 있습니다.
filter.prefix = @"prefix1";

// Filter는 규칙의 영향을 받는 Object 집합을 설명하는 데 사용됩니다.
rule.filter = filter;

// 객체가 Standard_IA 또는 Archive로 변환될 때의 규칙 변환 속성
QCloudLifecycleTransition* transition = [[QCloudLifecycleTransition alloc] init];

// 객체의 마지막 수정 날짜로부터 규칙에 해당하는 작업이 실행되기까지의 일수 지정:
transition.days = 100;

// Object 전환 타깃 스토리지 유형 지정. 열거 값: STANDARD_IA, ARCHIVE
transition.storageClass = QCloudCOSStorageStandardIA;
rule.transition = transition;
request.lifeCycle = lifecycleConfiguration;

// 라이프사이클 설정
request.lifeCycle.rules = @[rule];
[request setFinishBlock:^(id outputObject, NSError* error) {
    // outputObject는 상응하는 모든 http 헤더를 포함합니다.
    NSDictionary* info = (NSDictionary *) outputObject;
}];

[[QCloudCOSXMLService defaultCOSXML] PutBucketLifecycle:request];
```

>?전체 예시는 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Objc/Examples/cases/BucketLifecycle.m)를 참고하십시오.


**Swift**

[//]: # (.cssg-snippet-put-bucket-lifecycle)
```swift
let putBucketLifecycleReq = QCloudPutBucketLifecycleRequest.init();

// BucketName-Appid로 구성된 버킷 이름. COS 콘솔에서 볼 수 있습니다. https://console.cloud.tencent.com/cos5/bucket
putBucketLifecycleReq.bucket = "examplebucket-1250000000";

let config = QCloudLifecycleConfiguration.init();

// 규칙 설명
let rule = QCloudLifecycleRule.init();

// 규칙을 고유하게 식별하는 데 사용
rule.identifier = "swift";

// 규칙의 활성화 여부를 나타냅니다. 열거 값: Enabled, Disabled
rule.status = .enabled;

// Filter는 규칙의 영향을 받는 Object 집합을 설명하는 데 사용됩니다.
let fileter = QCloudLifecycleRuleFilter.init();

// 규칙이 적용되는 접두사를 지정합니다. 접두사와 일치하는 객체는 이 규칙의 영향을 받으며 Prefix는 최대 하나일 수 있습니다.
fileter.prefix = "0";

// Filter는 규칙의 영향을 받는 Object 집합을 설명하는 데 사용됩니다.
rule.filter = fileter;

// 객체가 Standard_IA 또는 Archive로 변환될 때의 규칙 변환 속성
let transition = QCloudLifecycleTransition.init();

// 객체의 마지막 수정 날짜로부터 규칙에 해당하는 작업이 실행되기까지의 일수 지정:
transition.days = 100;

// Object 전환 타깃 스토리지 유형 지정. 열거 값: STANDARD_IA, ARCHIVE
transition.storageClass = .standardIA;

rule.transition = transition;

putBucketLifecycleReq.lifeCycle = config;

// 라이프사이클 설정
putBucketLifecycleReq.lifeCycle.rules = [rule];

putBucketLifecycleReq.finishBlock = {(result,error) in
    if let result = result {
        // result에 상응하는 header 정보 포함
    } else {
        print(error!);
    }
}
QCloudCOSXMLService.defaultCOSXML().putBucketLifecycle(putBucketLifecycleReq);
```

>?전체 예시는 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Swift/Examples/cases/BucketLifecycle.swift)를 참고하십시오.


## 라이프사이클 쿼리

#### 기능 설명

버킷 라이프사이클 관리 설정 쿼리

#### 예시 코드
**Objective-C**

[//]: # (.cssg-snippet-get-bucket-lifecycle)
```objective-c
QCloudGetBucketLifecycleRequest* request = [QCloudGetBucketLifecycleRequest new];

// BucketName-Appid로 구성된 버킷 이름. COS 콘솔에서 볼 수 있습니다. https://console.cloud.tencent.com/cos5/bucket
request.bucket = @"examplebucket-1250000000";
[request setFinishBlock:^(QCloudLifecycleConfiguration* result,NSError* error) {
    // result에서 반환 정보를 얻을 수 있습니다.
    // result.rules는 규칙의 배열입니다.
 
}];
[[QCloudCOSXMLService defaultCOSXML] GetBucketLifecycle:request];
```

>?전체 예시는 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Objc/Examples/cases/BucketLifecycle.m)를 참고하십시오.

**Swift**

[//]: # (.cssg-snippet-get-bucket-lifecycle)
```swift
let getBucketLifeCycle = QCloudGetBucketLifecycleRequest.init();
getBucketLifeCycle.bucket = "examplebucket-1250000000";
getBucketLifeCycle.setFinish { (config, error) in
    if let config = config {
        // 라이프 사이클 규칙
        let rules = config.rules
    } else {
        print(error!);
    }
 
};
QCloudCOSXMLService.defaultCOSXML().getBucketLifecycle(getBucketLifeCycle);
```

>?전체 예시는 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Swift/Examples/cases/BucketLifecycle.swift)를 참고하십시오.

## 라이프사이클 삭제

#### 기능 설명

버킷 라이프사이클 관리 설정 삭제

#### 예시 코드
**Objective-C**

[//]: # (.cssg-snippet-delete-bucket-lifecycle)
```objective-c
QCloudDeleteBucketLifeCycleRequest* request =
[[QCloudDeleteBucketLifeCycleRequest alloc ] init];

// BucketName-Appid로 구성된 버킷 이름. COS 콘솔에서 볼 수 있습니다. https://console.cloud.tencent.com/cos5/bucket
request.bucket = @"examplebucket-1250000000";

[request setFinishBlock:^(QCloudLifecycleConfiguration* deleteResult, NSError* error) {
    // 삭제 결과 반환
}];
[[QCloudCOSXMLService defaultCOSXML] DeleteBucketLifeCycle:request];
```

>?전체 예시는 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Objc/Examples/cases/BucketLifecycle.m)를 참고하십시오.

**Swift**

[//]: # (.cssg-snippet-delete-bucket-lifecycle)
```swift
let deleteBucketLifeCycle = QCloudDeleteBucketLifeCycleRequest.init();
deleteBucketLifeCycle.bucket = "examplebucket-1250000000";
deleteBucketLifeCycle.finishBlock = { (result, error) in
    if let result = result {
        // result에 상응하는 header 정보 포함
    } else {
        print(error!);
    }
};
QCloudCOSXMLService.defaultCOSXML().deleteBucketLifeCycle(deleteBucketLifeCycle);
```

>?전체 예시는 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Swift/Examples/cases/BucketLifecycle.swift)를 참고하십시오.

