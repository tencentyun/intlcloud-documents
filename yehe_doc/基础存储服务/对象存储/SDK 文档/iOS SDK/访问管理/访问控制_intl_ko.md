## 소개

본 문서는 버킷, 객체의 액세스 제어에 대한 리스트(ACL) 관련 API 개요 및 SDK 샘플 코드를 제공합니다.

**버킷 ACL**

| API                                                          | 작업명         | 작업 설명                             |
| ------------------------------------------------------------ | -------------- | --------------------------------------- |
| [PUT Bucket acl](https://intl.cloud.tencent.com/document/product/436/7737) | 버킷 ACL 설정 | 지정 버킷의 액세스 권한 제어 리스트(ACL) 설정 |
| [GET Bucket acl](https://intl.cloud.tencent.com/document/product/436/7733) |버킷 ACL 조회 | 지정 버킷의 액세스 권한 제어 리스트(ACL) 조회 |

**객체 ACL**

| API                                                          | 작업명       | 작업 설명                                      |
| ------------------------------------------------------------ | ------------ | --------------------------------------------- |
| [PUT Object acl](https://intl.cloud.tencent.com/document/product/436/7748) | 객체 ACL 설정 | 버킷의 특정 객체의 액세스 제어 리스트 설정 |
| [GET Object acl](https://intl.cloud.tencent.com/document/product/436/7744) | 객체 ACL 조회 | 객체 액세스 제어 리스트 조회             |

## SDK API 참고

SDK 모든 인터페이스의 구체적인 매개변수와 방법 설명은 [SDK API](https://cos-ios-sdk-doc-1253960454.file.myqcloud.com/)를 참고하십시오.


## 버킷 ACL

### 버킷 ACL 설정

#### 기능 설명

지정 버킷의 액세스 권한 리스트(ACL)를 설정합니다.

#### 예시 코드
**Objective-C**

[//]: # (.cssg-snippet-put-bucket-acl)
```objective-c
QCloudPutBucketACLRequest* putACL = [QCloudPutBucketACLRequest new];

// 권한을 부여한 계정 ID
NSString* uin = @"100000000001";
NSString *ownerIdentifier = [NSString stringWithFormat:@"qcs::cam::uin/%@:uin/%@"
                             , uin,uin];
NSString *grantString = [NSString stringWithFormat:@"id=\"%@\"",ownerIdentifier];

// 권한을 부여받은 대상에게 읽기/쓰기 권한 부여
putACL.grantFullControl = grantString;

// 권한을 부여받은 대상에게 읽기 권한 부여
putACL.grantRead = grantString;

// BucketName-Appid로 구성된 버킷의 이름. COS 콘솔에서 확인 가능 https://console.cloud.tencent.com/cos5/bucket
putACL.bucket = @"examplebucket-1250000000";

[putACL setFinishBlock:^(id outputObject, NSError *error) {
    // outputObject에서 서버에 반환되는 header 정보를 획득할 수 있습니다.
    NSDictionary * result = (NSDictionary *)outputObject;

}];
// acl 설정
[[QCloudCOSXMLService defaultCOSXML] PutBucketACL:putACL];
```

>?전체 예시는 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Objc/Examples/cases/BucketACL.m)를 참고하십시오.

**Swift**

[//]: # (.cssg-snippet-put-bucket-acl)
```swift
let putBucketACLReq = QCloudPutBucketACLRequest.init();

// BucketName-Appid로 구성된 버킷의 이름. COS 콘솔에서 확인 가능 https://console.cloud.tencent.com/cos5/bucket
putBucketACLReq.bucket = "examplebucket-1250000000";

// 권한을 부여한 계정 ID
let appTD = "100000000001";
let ownerIdentifier = "qcs::cam::uin/\(appTD):uin/\(appTD)";
let grantString = "id=\"\(ownerIdentifier)\"";
// 권한을 부여받은 대상에게 쓰기 권한 부여
putBucketACLReq.grantWrite = grantString;

// 권한을 부여받은 대상에게 읽기 권한 부여
putBucketACLReq.grantRead = grantString;

// 권한을 부여받은 대상에게 읽기/쓰기 권한 부여 grantFullControl == grantRead + grantWrite
putBucketACLReq.grantFullControl = grantString;

putBucketACLReq.finishBlock = {(result,error) in
    if let result = result {
        // result에서 서버 반환의 header 정보를 획득할 수 있습니다.
    } else {
        print(error!)
    }
}
QCloudCOSXMLService.defaultCOSXML().putBucketACL(putBucketACLReq);
```

>?전체 예시는 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Swift/Examples/cases/BucketACL.swift)를 참고하십시오.

### 버킷 ACL 조회

#### 기능 설명

지정 버킷의 액세스 권한 리스트(ACL)를 조회합니다.

#### 예시 코드
**Objective-C**

[//]: # (.cssg-snippet-get-bucket-acl)
```objective-c
QCloudGetBucketACLRequest* getBucketACl = [QCloudGetBucketACLRequest new];

// BucketName-APPID 포맷의 버킷 이름
getBucketACl.bucket = @"examplebucket-1250000000";

[getBucketACl setFinishBlock:^(QCloudACLPolicy * _Nonnull result,
                                       NSError * _Nonnull error) {
    // 권한을 부여받은 대상과 권한 정보
    QCloudAccessControlList *acl = result.accessControlList;
}];

[[QCloudCOSXMLService defaultCOSXML] GetBucketACL:getBucketACl];
```

>?전체 예시는 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Objc/Examples/cases/BucketACL.m)를 참고하십시오.

**Swift**

[//]: # (.cssg-snippet-get-bucket-acl)
```swift
let getBucketACLReq = QCloudGetBucketACLRequest.init();

// BucketName-Appid로 구성된 버킷의 이름. COS 콘솔에서 확인 가능 https://console.cloud.tencent.com/cos5/bucket
getBucketACLReq.bucket = "examplebucket-1250000000";

getBucketACLReq.setFinish { (result, error) in
    if let result = result {
        // ACL 라이선스 정보
        let acl = result.accessControlList;
    } else {
        print(error!)
    }
}
QCloudCOSXMLService.defaultCOSXML().getBucketACL(getBucketACLReq)
```

>?전체 예시는 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Swift/Examples/cases/BucketACL.swift)를 참고하십시오.

## 객체 ACL

### 객체 ACL 설정

#### 기능 설명

버킷의 한 객체의 액세스 제어 리스트(ACL)를 설정합니다.

#### 예시 코드
**Objective-C**

[//]: # (.cssg-snippet-put-object-acl)
```objective-c
QCloudPutObjectACLRequest* request = [QCloudPutObjectACLRequest new];

// 객체 키. 객체의 COS 상의 전체 경로로, 디렉터리가 있을 경우 형식은 "video/xxx/movie.mp4"입니다.
request.object = @"exampleobject";

// BucketName-Appid로 구성된 버킷의 이름. COS 콘솔에서 확인 가능 https://console.cloud.tencent.com/cos5/bucket
request.bucket = @"examplebucket-1250000000";

NSString *grantString = [NSString stringWithFormat:@"id=\"%@\"",@"100000000001"];

// grantFullControl는 grantRead + grantWrite와 동등
// 권한을 부여받은 대상에게 읽기/쓰기 권한 부여.
request.grantFullControl = grantString;
// 권한을 부여받은 대상에게 읽기 권한 부여.
request.grantRead = grantString;

[request setFinishBlock:^(id outputObject, NSError *error) {
    // outputObject에서 response의 etag 또는 사용자 정의 헤더 등 정보 획득 가능
    NSDictionary* info = (NSDictionary *) outputObject;
}];

[[QCloudCOSXMLService defaultCOSXML] PutObjectACL:request];
```

>?전체 예시는 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Objc/Examples/cases/ObjectACL.m)를 참고하십시오.

**Swift**

[//]: # (.cssg-snippet-put-object-acl)
```swift
let putObjectACl = QCloudPutObjectACLRequest.init();

// BucketName-Appid로 구성된 버킷의 이름. COS 콘솔에서 확인 가능 https://console.cloud.tencent.com/cos5/bucket
putObjectACl.bucket = "examplebucket-1250000000";

// 객체 키. 객체의 COS 상의 전체 경로로, 디렉터리가 있을 경우 형식은 "video/xxx/movie.mp4"입니다.
putObjectACl.object = "exampleobject";
let grantString = "id=\"100000000001\"";

// grantFullControl는 grantRead + grantWrite와 동등
putObjectACl.grantFullControl = grantString;
// 권한을 부여받은 대상에게 읽기 권한 부여.
putObjectACl.grantRead = grantString;


putObjectACl.finishBlock = {(result,error)in
    if let result = result {
        // result에 상응하는 header 정보 포함
    } else {
        print(error!);
    }
}
QCloudCOSXMLService.defaultCOSXML().putObjectACL(putObjectACl);
```

>?전체 예시는 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Swift/Examples/cases/ObjectACL.swift)를 참고하십시오.

### 객체 ACL 조회

#### 기능 설명

객체의 액세스 제어 리스트를 조회합니다.

#### 예시 코드
**Objective-C**

[//]: # (.cssg-snippet-get-object-acl)
```objective-c
QCloudGetObjectACLRequest *request = [QCloudGetObjectACLRequest new];

// 객체 키. 객체의 COS 상의 전체 경로로, 디렉터리가 있을 경우 형식은 "video/xxx/movie.mp4"입니다.
request.object = @"exampleobject";

// BucketName-Appid로 구성된 버킷의 이름. COS 콘솔에서 확인 가능 https://console.cloud.tencent.com/cos5/bucket
request.bucket = @"examplebucket-1250000000";

__block QCloudACLPolicy* policy;
[request setFinishBlock:^(QCloudACLPolicy * _Nonnull result,
                          NSError * _Nonnull error) {
    
    policy = result;
    // result.accessControlList; 권한을 부여받은 대상과 권한 정보
    // result.owner; 소유자 정보
}];

[[QCloudCOSXMLService defaultCOSXML] GetObjectACL:request];
```
>?전체 예시는 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Objc/Examples/cases/ObjectACL.m)를 참고하십시오.



**Swift**

[//]: # (.cssg-snippet-get-object-acl)
```swift
let getObjectACL = QCloudGetObjectACLRequest.init();

// BucketName-Appid로 구성된 버킷의 이름. COS 콘솔에서 확인 가능 https://console.cloud.tencent.com/cos5/bucket
getObjectACL.bucket = "examplebucket-1250000000";

// 객체 키. 객체의 COS 상의 전체 경로로, 디렉터리가 있을 경우 형식은 "video/xxx/movie.mp4"입니다.
getObjectACL.object = "exampleobject";
getObjectACL.setFinish { (result, error) in
    if let result = result {
        // 객체 라이선스 정보
        let acl = result.accessControlList
    } else {
        print(error!);
    }
}
QCloudCOSXMLService.defaultCOSXML().getObjectACL(getObjectACL);
```
>?전체 예시는 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Swift/Examples/cases/ObjectACL.swift)를 참고하십시오.



