## 소개

본 문서는 객체 메타데이터 작업 조회에 대한 API 개요 및 SDK 예시 코드를 제공합니다.

| API                                                          | 작업명         | 작업 설명                                  |
| ------------------------------------------------------------ | -------------- | ----------------------------------------- |
| [HEAD Object](https://intl.cloud.tencent.com/document/product/436/7745) | 객체 메타데이터 조회 | 객체의 메타데이터 정보 조회                  |

## SDK API 참고

SDK 모든 인터페이스의 구체적인 매개변수와 방법 설명은 [SDK API](https://cos-ios-sdk-doc-1253960454.file.myqcloud.com/)를 참고하십시오.

## 객체 메타데이터 조회

#### 기능 설명

Object의 Meta 정보를 조회합니다.

#### 예시 코드
**Objective-C**

[//]: # (.cssg-snippet-head-object)
```objective-c
QCloudHeadObjectRequest* headerRequest = [QCloudHeadObjectRequest new];

// 객체 키. 객체의 COS 상의 전체 경로로, 디렉터리가 있을 경우 형식은 "video/xxx/movie.mp4"입니다.
headerRequest.object = @"exampleobject";

// versionId 버전 제어 활성화 시, 조회할 버전 ID를 지정하며 지정하지 않을 경우 객체의 최신 버전을 조회합니다.
headerRequest.versionID = @"versionID";

// BucketName-Appid로 구성된 버킷 이름. COS 콘솔에서 확인 가능합니다. https://console.cloud.tencent.com/cos5/bucket
headerRequest.bucket = @"examplebucket-1250000000";

[headerRequest setFinishBlock:^(NSDictionary* result, NSError *error) {
    // result 구체적인 정보 반환
    // 파일 crc64 가져오기
     NSString * crc64 = [[outputObject __originHTTPURLResponse__].allHeaderFields valueForKey:@"x-cos-hash-crc64ecma"];
}];

[[QCloudCOSXMLService defaultCOSXML] HeadObject:headerRequest];
```

>?전체 예시는 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Objc/Examples/cases/HeadObject.m)를 참고하십시오.

**Swift**

[//]: # (.cssg-snippet-head-object) 
```swift
let headObject = QCloudHeadObjectRequest.init();

// BucketName-Appid로 구성된 버킷 이름. COS 콘솔에서 확인 가능합니다. https://console.cloud.tencent.com/cos5/bucket
headObject.bucket = "examplebucket-1250000000";

// versionId 버전 제어 활성화 시, 조회할 버전 ID를 지정하며 지정하지 않을 경우 객체의 최신 버전을 조회합니다.
headObject.versionID = "versionID";

// 객체 키. 객체의 COS 상의 전체 경로로, 디렉터리가 있을 경우 형식은 "video/xxx/movie.mp4"입니다.
headObject.object  = "exampleobject";
headObject.finishBlock =  {(result,error) in
    if let result = result {
        // 파일 crc64 가져오기
        let crc64 = result?.__originHTTPURLResponse__.allHeaderFields["x-cos-hash-crc64ecma"];
       
    } else {
        print(error!);
    }
}
QCloudCOSXMLService.defaultCOSXML().headObject(headObject);
```

>?전체 예시는 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Swift/Examples/cases/HeadObject.swift)를 참고하십시오.

