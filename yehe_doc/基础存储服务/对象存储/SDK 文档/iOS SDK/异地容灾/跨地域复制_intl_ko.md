## 소개

본문은 리전 간 복제 관련 API 개요 및 SDK 코드 예시를 제공합니다.

| API                                                          | 작업 이름         | 작업 설명                   |
| ------------------------------------------------------------ | -------------- | -------------------------- |
| [PUT Bucket replication](https://intl.cloud.tencent.com/document/product/436/19223) | 리전 간 복제 설정 | 버킷의 리전 간 복제 규칙 설정 |
| [GET Bucket replication](https://intl.cloud.tencent.com/document/product/436/19222) |리전 간 복제 쿼리 | 버킷의 리전 간 복제 규칙 쿼리 |
| [DELETE Bucket replication](https://intl.cloud.tencent.com/document/product/436/19221) | 리전 간 복제 삭제 | 버킷의 리전 간 복제 규칙 삭제 |

## SDK API 참고

SDK 모든 인터페이스의 구체적인 매개변수와 방법 설명은 [SDK API](https://cos-ios-sdk-doc-1253960454.file.myqcloud.com/)를 참고하십시오.

## 리전 간 복제 설정

#### 기능 설명

지정된 버킷의 리전 간 복제 규칙을 설정합니다.

#### 예시 코드
**Objective-C**

[//]: # (.cssg-snippet-put-bucket-replication)
```objective-c
QCloudPutBucketReplicationRequest* request = [[QCloudPutBucketReplicationRequest alloc] init];

// BucketName-Appid로 구성된 버킷의 이름. COS 콘솔에서 확인 가능합니다. https://console.cloud.tencent.com/cos5/bucket
request.bucket = @"examplebucket-1250000000";

// 모든 리전 간 설정 정보를 설명합니다.
QCloudBucketReplicationConfiguation* replConfiguration =
                            [[QCloudBucketReplicationConfiguation alloc] init];

// 요청자 신분 표시
replConfiguration.role = @"qcs::cam::uin/100000000001:uin/100000000001";

// 특정 설정 정보
QCloudBucketReplicationRule* rule = [[QCloudBucketReplicationRule alloc] init];

// 특정 Rule의 이름을 표시하는 데 사용
rule.identifier = @"identifier";
rule.status = QCloudCOSXMLStatusEnabled;

// 리소스 식별자
QCloudBucketReplicationDestination* destination = [[QCloudBucketReplicationDestination alloc] init];
NSString* destinationBucket = @"destinationbucket-1250000000";

// 타깃 버킷의 위치
NSString* region = @"ap-beijing";
destination.bucket = [NSString stringWithFormat:@"qcs::cos:%@::%@",region,destinationBucket];

// 타깃 버킷 정보
rule.destination = destination;

// 접두사 매칭 정책. 중복 불가. 중복 시 오류 코드 반환.
rule.prefix = @"prefix1";
replConfiguration.rule = @[rule];
request.configuation = replConfiguration;

[request setFinishBlock:^(id outputObject, NSError* error) {
    // outputObject는 상응하는 모든 http 헤더를 포함합니다.
    NSDictionary* info = (NSDictionary *) outputObject;
    
}];
[[QCloudCOSXMLService defaultCOSXML] PutBucketRelication:request];
```

>?전체 예시는 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Objc/Examples/cases/BucketReplication.m)를 참고하십시오.

**Swift**

[//]: # (.cssg-snippet-put-bucket-replication)
```swift
let putBucketReplication = QCloudPutBucketReplicationRequest.init();

// BucketName-Appid로 구성된 버킷의 이름. COS 콘솔에서 확인 가능합니다. https://console.cloud.tencent.com/cos5/bucket
putBucketReplication.bucket = "examplebucket-1250000000";

// 모든 리전 간 설정 정보를 설명합니다.
let config = QCloudBucketReplicationConfiguation.init();
config.role = "qcs::cam::uin/100000000001:uin/100000000001";

// 요청자 신분 표시
let rule = QCloudBucketReplicationRule.init();
 
// 특정 Rule의 이름을 표시하는 데 사용
rule.identifier = "rule1";
// 규칙 활성화 상태. 옵션 .enabled, .disabled
rule.status = .enabled;

// 타깃 버킷 정보
let destination = QCloudBucketReplicationDestination.init();
let destinationBucket = "destinationbucket-1250000000";
let region = "ap-beijing";
destination.bucket = "qcs::cos:\(region)::\(destinationBucket)";
rule.destination = destination;

// 접두사 일치 정책. 중복 불가. 중복 시 오류 코드 반환.
rule.prefix = "dir/";

config.rule = [rule];

putBucketReplication.configuation = config;

putBucketReplication.finishBlock = {(result,error) in
    if let result = result {
        // result에 상응하는 header 정보 포함
    } else {
        print(error!);
    }
}
QCloudCOSXMLService.defaultCOSXML().putBucketRelication(putBucketReplication);
```

>?전체 예시는 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Swift/Examples/cases/BucketReplication.swift)를 참고하십시오.

## 리전 간 복제 쿼리

#### 기능 설명

지정된 버킷의 리전 간 복제 규칙을 쿼리합니다.

#### 예시 코드
**Objective-C**

[//]: # (.cssg-snippet-get-bucket-replication)
```objective-c
QCloudGetBucketReplicationRequest* request = [[QCloudGetBucketReplicationRequest alloc] init];

// BucketName-Appid로 구성된 버킷의 이름. COS 콘솔에서 확인 가능합니다. https://console.cloud.tencent.com/cos5/bucket
request.bucket = @"examplebucket-1250000000";

[request setFinishBlock:^(QCloudBucketReplicationConfiguation* result,
                          NSError* error) {
    // 특정 구성 정보, 최대 1000개 지원, 모든 정책은 하나의 타깃 버킷만 가리킬 수 있습니다.
    NSArray *rules = result.rule;
}];
[[QCloudCOSXMLService defaultCOSXML] GetBucketReplication:request];
```

>?전체 예시는 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Objc/Examples/cases/BucketReplication.m)를 참고하십시오.

**Swift**

[//]: # (.cssg-snippet-get-bucket-replication)
```swift
let getBucketReplication = QCloudGetBucketReplicationRequest.init();
getBucketReplication.bucket = "examplebucket-1250000000";
getBucketReplication.setFinish { (config, error) in
    if let config = config {
        // 설정 정보 목록
        let rule = config.rule
    } else {
        print(error!);
    }
}
QCloudCOSXMLService.defaultCOSXML().getBucketReplication(getBucketReplication);
```

>?전체 예시는 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Swift/Examples/cases/BucketReplication.swift)를 참고하십시오.

## 리전 간 복제 삭제

#### 기능 설명

지정된 버킷에 대한 리전 간 복제 규칙을 삭제합니다.

#### 예시 코드
**Objective-C**

[//]: # (.cssg-snippet-delete-bucket-replication)
```objective-c
QCloudDeleteBucketReplicationRequest* request =
                        [[QCloudDeleteBucketReplicationRequest alloc] init];

// BucketName-Appid로 구성된 버킷의 이름. COS 콘솔에서 확인 가능합니다. https://console.cloud.tencent.com/cos5/bucket
request.bucket = @"examplebucket-1250000000";

[request setFinishBlock:^(id outputObject, NSError* error) {
    // outputObject는 상응하는 모든 http 헤더를 포함합니다.
    NSDictionary* info = (NSDictionary *) outputObject;
    
}];
[[QCloudCOSXMLService defaultCOSXML] DeleteBucketReplication:request];
```

>?전체 예시는 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Objc/Examples/cases/BucketReplication.m)를 참고하십시오.

**Swift**

[//]: # (.cssg-snippet-delete-bucket-replication)
```swift
let deleteBucketReplication = QCloudDeleteBucketReplicationRequest.init();
deleteBucketReplication.bucket = "examplebucket-1250000000";
deleteBucketReplication.finishBlock = {(result,error) in
    if let result = result {
        // result에 상응하는 header 정보 포함
    } else {
        print(error!);
    }
}
QCloudCOSXMLService.defaultCOSXML().deleteBucketReplication(deleteBucketReplication);
```

>?전체 예시는 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Swift/Examples/cases/BucketReplication.swift)를 참고하십시오.

