<!--
 * @Author: your name
 * @Date: 2020-12-07 10:53:33
 * @LastEditTime: 2021-06-08 09:27:54
 * @LastEditors: your name
 * @Description: In User Settings Edit
 * @FilePath: /qcloud-documents/product/스토리지와 CDN/COS 4.0/SDK 문서/iOS SDK/객체 작업/CORS 프리플라이트 요청 구성.md
-->
## 소개

본 문서는 CORS 프리플라이트 요청 구성 작업에 대한 API 개요 및 SDK 예시 코드를 제공합니다.

| API                                                          | 작업명         | 작업 설명                                  |
| ------------------------------------------------------------ | -------------- | ----------------------------------------- |
| [Options Object](https://intl.cloud.tencent.com/document/product/436/8288) | CORS 프리플라이트 요청 구성 | 사전 요청을 통해 실제 CORS 요청의 발송 가능 여부 확인  |

## SDK API 참고

SDK 모든 인터페이스의 구체적인 매개변수와 방법 설명은 [SDK API](https://cos-ios-sdk-doc-1253960454.file.myqcloud.com/)를 참고하십시오.

## CORS 프리플라이트 요청 구성

#### 기능 설명
CORS 프리플라이트 요청 구성을 획득합니다(Options Object).

#### 예시 코드
**Objective-C**

[//]: # (.cssg-snippet-option-object)
```objective-c
QCloudOptionsObjectRequest* request = [[QCloudOptionsObjectRequest alloc] init];

// BucketName-APPID 포맷의 버킷 이름
request.bucket =@"examplebucket-1250000000";

// CORS 프리플라이트 요청에 대한 원본 도메인, 요청 method 및 host를 설정합니다.
request.origin = @"http://cloud.tencent.com";
request.accessControlRequestMethod = @"GET";
request.accessControlRequestHeaders = @"host";

// 객체 키. 객체의 COS 상의 전체 경로로, 디렉터리가 있을 경우 형식은 "video/xxx/movie.mp4"입니다.
request.object = @"exampleobject";

[request setFinishBlock:^(id outputObject, NSError* error) {
    // outputObject에서 response의 etag 또는 사용자 정의 헤더 등 정보 획득 가능
    NSDictionary* info = (NSDictionary *) outputObject;
    
}];

[[QCloudCOSXMLService defaultCOSXML] OptionsObject:request];
```

>?전체 예시는 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Objc/Examples/cases/BucketCORS.m)를 참고하십시오.

**Swift**

[//]: # (.cssg-snippet-option-object)
```swift
let optionsObject = QCloudOptionsObjectRequest.init();

// 객체 키. 객체의 COS 상의 전체 경로로, 디렉터리가 있을 경우 형식은 "video/xxx/movie.mp4"입니다.
optionsObject.object = "exampleobject";

// CORS 프리플라이트 요청에 대한 원본 도메인, 요청 method 및 요청 헤더를 설정합니다.
optionsObject.origin = "http://www.qcloud.com";
optionsObject.accessControlRequestMethod = "GET";
optionsObject.accessControlRequestHeaders = "origin";

// BucketName-Appid로 구성된 버킷의 이름. COS 콘솔에서 확인 가능 https://console.cloud.tencent.com/cos5/bucket
optionsObject.bucket = "examplebucket-1250000000";

optionsObject.finishBlock = {(result,error) in
    if let result = result {
        // `result`에서 서버가 반환한 header 정보를 얻을 수 있습니다.
    }
}
QCloudCOSXMLService.defaultCOSXML().optionsObject(optionsObject);
```

>?전체 예시는 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Swift/Examples/cases/BucketCORS.swift)를 참고하십시오.

