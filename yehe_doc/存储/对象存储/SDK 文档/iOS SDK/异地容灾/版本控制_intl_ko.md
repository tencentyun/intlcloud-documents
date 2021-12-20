## 소개

본 문서는 버전 관리에 대한 API 개요 및 SDK 예시 코드를 제공합니다.

| API                                                          | 작업명       | 작업 설명                 |
| ------------------------------------------------------------ | ------------ | ------------------------ |
| [PUT Bucket versioning](https://intl.cloud.tencent.com/document/product/436/19889) | 버전 관리 설정 | 버킷의 버전 관리 기능 설정 |
| [GET Bucket versioning](https://intl.cloud.tencent.com/document/product/436/19888) | 버전 관리 확인 | 버킷의 버전 관리 정보 조회 |

## SDK API 참고

SDK 모든 인터페이스의 구체적인 매개변수와 방법 설명은 [SDK API](https://cos-ios-sdk-doc-1253960454.file.myqcloud.com/)를 참고하십시오.

## 버전 관리 설정

#### 기능 설명

버킷의 버전 관리 구성을 설정하는 데 사용됩니다. 활성화되면 버전 관리는 일시 중단만 가능하고 비활성화할 수는 없습니다.

#### 예시 코드
**Objective-C**

[//]: # ".cssg-snippet-put-bucket-versioning"
```objective-c
// 버전 관리 활성화
QCloudPutBucketVersioningRequest* request = [[QCloudPutBucketVersioningRequest alloc] init];

// BucketName-Appid로 구성된 버킷의 이름. COS 콘솔에서 확인 가능합니다. https://console.cloud.tencent.com/cos5/bucket
request.bucket =@"examplebucket-1250000000";

// 버전 관리의 구체적인 정보 설명
QCloudBucketVersioningConfiguration* versioningConfiguration =
    [[QCloudBucketVersioningConfiguration alloc] init];

request.configuration = versioningConfiguration;

// 버전 활성화 여부. 열거 값: QCloudCOSBucketVersioningStatusEnabled,
// QCloudCOSBucketVersioningStatusSuspended
versioningConfiguration.status = QCloudCOSBucketVersioningStatusEnabled;

[request setFinishBlock:^(id outputObject, NSError* error) {
    // outputObject는 상응하는 모든 http 헤더를 포함합니다.
    NSDictionary* info = (NSDictionary *) outputObject;
}];
[[QCloudCOSXMLService defaultCOSXML] PutBucketVersioning:request];
```

>?전체 예시는 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Objc/Examples/cases/BucketVersioning.m)를 참고하십시오.

**Swift**

[//]: # ".cssg-snippet-put-bucket-versioning"
```swift
// 버전 관리 활성화
let putBucketVersioning = QCloudPutBucketVersioningRequest.init();

// BucketName-Appid로 구성된 버킷의 이름. COS 콘솔에서 확인 가능합니다. https://console.cloud.tencent.com/cos5/bucket
putBucketVersioning.bucket = "examplebucket-1250000000";

// 버전 관리의 구체적인 정보 설명
let config = QCloudBucketVersioningConfiguration.init();

// 버전 활성화 여부. 열거 값: Suspended, Enabled
config.status = .enabled;

putBucketVersioning.configuration = config;

putBucketVersioning.finishBlock = {(result,error) in
    if let result = result {
        // result에 상응하는 header 정보 포함
    } else {
        print(error!);
    }
}
QCloudCOSXMLService.defaultCOSXML().putBucketVersioning(putBucketVersioning);
```

>?전체 예시는 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Swift/Examples/cases/BucketVersioning.swift)를 참고하십시오.

## 버전 관리 조회

#### 기능 설명

지정된 버킷의 버전 관리 정보를 쿼리합니다.

- 버킷 버전 관리 상태를 얻으려면 버킷에 대한 읽기 권한이 있어야 합니다.
- 버전 관리 상태는 버전 관리 비활성화, 버전 관리 활성화, 버전 관리 일시 중지 세 가지입니다.

#### 예시 코드
**Objective-C**

[//]: # ".cssg-snippet-get-bucket-versioning"
```objective-c
QCloudGetBucketVersioningRequest* request =
                            [[QCloudGetBucketVersioningRequest alloc] init];

// BucketName-Appid로 구성된 버킷의 이름. COS 콘솔에서 확인 가능합니다. https://console.cloud.tencent.com/cos5/bucket
request.bucket = @"examplebucket-1250000000";

[request setFinishBlock:^(QCloudBucketVersioningConfiguration* result,
                          NSError* error) {
    // 멀티 버전 상태 가져오기
    QCloudCOSBucketVersioningStatus * status = result.status;
}];

[[QCloudCOSXMLService defaultCOSXML] GetBucketVersioning:request];
```

>?전체 예시는 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Objc/Examples/cases/BucketVersioning.m)를 참고하십시오.

**Swift**

[//]: # ".cssg-snippet-get-bucket-versioning"
```swift
let getBucketVersioning = QCloudGetBucketVersioningRequest.init();

// BucketName-Appid로 구성된 버킷의 이름. COS 콘솔에서 확인 가능합니다. https://console.cloud.tencent.com/cos5/bucket
getBucketVersioning.bucket = "examplebucket-1250000000";

getBucketVersioning.setFinish { (config, error) in
    if let config = config {
        // 멀티 버전 상태
        let status = config.status
    } else {
        print(error!);
    }
       
}
QCloudCOSXMLService.defaultCOSXML().getBucketVersioning(getBucketVersioning);
```

>?전체 예시는 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Swift/Examples/cases/BucketVersioning.swift)를 참고하십시오.

