## 소개

본문은 로깅과 관련된 API 및 SDK 코드 샘플에 대한 개요를 제공합니다.

| API                                                          | 작업명       | 작업 설명                 |
| ------------------------------------------------------------ | ------------ | -------------------------- |
| [PUT Bucket logging](https://intl.cloud.tencent.com/document/product/436/17054) | 로깅 설정 | 소스 버킷에 대한 로깅 활성화     |
| [GET Bucket logging](https://intl.cloud.tencent.com/document/product/436/17053) | 로깅 구성 쿼리 | 소스 버킷의 로깅 구성 쿼리 |

## SDK API 참고

SDK 모든 인터페이스의 구체적인 매개변수와 방법 설명은 [SDK API](https://cos-ios-sdk-doc-1253960454.file.myqcloud.com/)를 참고하십시오.

## 로그 관리 설정

#### 기능 설명

이 API(PUT Bucket logging)는 소스 버킷에 대한 로깅을 활성화하고 지정된 대상 버킷에 액세스 로그를 저장하는 데 사용됩니다.

#### 예시 코드
**Objective-C**

[//]: # (.cssg-snippet-put-bucket-logging)
```objective-c
QCloudPutBucketLoggingRequest *request = [QCloudPutBucketLoggingRequest new];

// 로깅 설정의 상태를 기술합니다. 서브 노드 정보가 없으면 로깅을 끈다는 의미입니다.
QCloudBucketLoggingStatus *status = [QCloudBucketLoggingStatus new];

// 버킷 logging에 의해 설정되는 특정 정보, 주로 대상 버킷
QCloudLoggingEnabled *loggingEnabled = [QCloudLoggingEnabled new];

// 로그를 저장하기 위한 대상 버킷은 동일한 버킷(권장되지 않음)이거나 동일한 계정 및 동일한 리전에 있는 버킷일 수 있습니다.
loggingEnabled.targetBucket = @"examplebucket-1250000000";

// 로그는 대상 버킷의 지정된 경로에 저장됩니다.
loggingEnabled.targetPrefix = @"mylogs";

status.loggingEnabled = loggingEnabled;
request.bucketLoggingStatus = status;

// BucketName-Appid로 구성된 버킷의 이름. COS 콘솔에서 확인 가능합니다. https://console.cloud.tencent.com/cos5/bucket
request.bucket = @"examplebucket-1250000000";

[request setFinishBlock:^(id outputObject, NSError *error) {
   // outputObject는 상응하는 모든 http 헤더를 포함합니다.
   NSDictionary* info = (NSDictionary *) outputObject;
}];
[[QCloudCOSXMLService defaultCOSXML] PutBucketLogging:request];
```

>?전체 예시는 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Objc/Examples/cases/BucketLogging.m)를 참고하십시오.

**Swift**

[//]: # (.cssg-snippet-put-bucket-logging)
```swift
let req = QCloudPutBucketLoggingRequest.init();

// 로깅 설정의 상태를 기술합니다. 서브 노드 정보가 없으면 로깅을 끈다는 의미입니다.
let status = QCloudBucketLoggingStatus.init();

// 버킷 logging에 의해 설정되는 특정 정보, 주로 대상 버킷
let loggingEnabled = QCloudLoggingEnabled.init();

// 로그를 저장하기 위한 대상 버킷은 동일한 버킷(권장되지 않음)이거나 동일한 계정 및 동일한 리전에 있는 버킷일 수 있습니다.
// BucketName-Appid로 구성된 버킷의 이름. COS 콘솔에서 확인 가능합니다. https://console.cloud.tencent.com/cos5/bucket
loggingEnabled.targetBucket = "examplebucket-1250000000";

// 로그는 대상 버킷의 지정된 경로에 저장됩니다.
loggingEnabled.targetPrefix = "logs/";

status.loggingEnabled = loggingEnabled;
req.bucketLoggingStatus = status;

// BucketName-Appid로 구성된 버킷의 이름. COS 콘솔에서 확인 가능합니다. https://console.cloud.tencent.com/cos5/bucket
req.bucket = "examplebucket-1250000000";
req.finishBlock = {(result,error) in
    if let result = result {
        // result에 상응하는 header 정보 포함
    } else {
        print(error!);
    }
}

QCloudCOSXMLService.defaultCOSXML().putBucketLogging(req);
```

>?전체 예시는 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Swift/Examples/cases/BucketLogging.swift)를 참고하십시오.

## 쿼리 로그 관리

#### 기능 설명

GET Bucket logging은 지정된 버킷의 로그 구성 정보를 쿼리하는 데 사용됩니다.

#### 예시 코드
**Objective-C**

[//]: # (.cssg-snippet-get-bucket-logging)
```objective-c
QCloudGetBucketLoggingRequest *getReq = [QCloudGetBucketLoggingRequest new];

// BucketName-Appid로 구성된 버킷의 이름. COS 콘솔에서 확인 가능합니다. https://console.cloud.tencent.com/cos5/bucket
getReq.bucket = @"examplebucket-1250000000";

[getReq setFinishBlock:^(QCloudBucketLoggingStatus * _Nonnull result,
                         NSError * _Nonnull error) {
    // 로그 설정 정보
    QCloudLoggingEnabled *loggingEnabled = result.loggingEnabled;
}];
[[QCloudCOSXMLService defaultCOSXML]GetBucketLogging:getReq];
```

>?전체 예시는 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Objc/Examples/cases/BucketLogging.m)를 참고하십시오.

**Swift**

[//]: # (.cssg-snippet-get-bucket-logging)
```swift
let req = QCloudGetBucketLoggingRequest.init();

// BucketName-Appid로 구성된 버킷의 이름. COS 콘솔에서 확인 가능합니다. https://console.cloud.tencent.com/cos5/bucket
req.bucket = "examplebucket-1250000000";
req.setFinish { (result, error) in
    if let result = result {
        // 로그 설정 정보
        let enabled = result.loggingEnabled
    } else {
        print(error!);
    }
};
QCloudCOSXMLService.defaultCOSXML().getBucketLogging(req);
```

>?전체 예시는 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Swift/Examples/cases/BucketLogging.swift)를 참고하십시오.

