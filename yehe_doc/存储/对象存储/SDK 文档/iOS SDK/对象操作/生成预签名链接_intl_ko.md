## 소개

본 문서는 객체 사전 서명된 링크 생성에 대한 예시 코드를 제공합니다.

## SDK API 참조

SDK 모든 인터페이스의 구체적인 매개변수와 방법 설명은 [SDK API](https://cos-ios-sdk-doc-1253960454.file.myqcloud.com/)를 참조하십시오.

## 객체 사전 서명된 링크 생성

#### 예시 코드1: 사전 서명된 업로드 링크 생성
**Objective-C**

[//]: # (.cssg-snippet-get-presign-upload-url)
```objective-c
QCloudGetPresignedURLRequest* getPresignedURLRequest = [[QCloudGetPresignedURLRequest alloc] init];

// BucketName-APPID 포맷의 버킷 이름
getPresignedURLRequest.bucket = @"examplebucket-1250000000";

// 사전 서명된 URL로 요청하는 HTTP 방법. 유효 값(대소문자 구분): @'GET', @'PUT', @'POST', @'DELETE'
getPresignedURLRequest.HTTPMethod = @"PUT";

// 객체 키는 객체의 COS 상의 전체 경로로, 디렉터리가 있을 경우 포맷은 'video/xxx/movie.mp4'입니다.
getPresignedURLRequest.object = @"exampleobject";

[getPresignedURLRequest setFinishBlock:^(QCloudGetPresignedURLResult * _Nonnull result,
                                         NSError * _Nonnull error) {
    // 사전 서명된 URL
    NSString* presignedURL = result.presienedURL;
    
}];

[[QCloudCOSXMLService defaultCOSXML] getPresignedURL:getPresignedURLRequest];
```

>?전체 예시는 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Objc/Examples/cases/ObjectPresignUrl.m)를 참조하십시오.

**Swift**

[//]: # (.cssg-snippet-get-presign-upload-url)
```swift
let getPresign  = QCloudGetPresignedURLRequest.init();

// BucketName-APPID 포맷의 버킷 이름
getPresign.bucket = "examplebucket-1250000000" ;

// // 사전 서명된 URL로 요청하는 HTTP 방법. 유효 값(대소문자 구분):
// @'GET', @'PUT', @'POST', @'DELETE'
getPresign.httpMethod = "PUT";

// 객체 키는 객체의 COS 상의 전체 경로로, 디렉터리가 있을 경우 포맷은 'video/xxx/movie.mp4'입니다.
getPresign.object = "exampleobject";
getPresign.setFinish { (result, error) in
    if let result = result {
        let url = result.presienedURL
    } else {
        print(error!);
    }
}
QCloudCOSXMLService.defaultCOSXML().getPresignedURL(getPresign);
```

>?전체 예시는 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Swift/Examples/cases/ObjectPresignUrl.swift)를 참조하십시오.

#### 예시 코드2: 사전 서명된 다운로드 링크 생성
**Objective-C**

[//]: # (.cssg-snippet-get-presign-download-url)
```objective-c
QCloudGetPresignedURLRequest* getPresignedURLRequest = [[QCloudGetPresignedURLRequest alloc] init];

// BucketName-APPID 포맷의 버킷 이름
getPresignedURLRequest.bucket = @"examplebucket-1250000000";

// 사전 서명된 URL로 요청하는 HTTP 방법. 유효 값(대소문자 구분): @'GET', @'PUT', @'POST', @'DELETE'
getPresignedURLRequest.HTTPMethod = @"GET";

// 객체 키는 객체의 COS 상의 전체 경로로, 디렉터리가 있을 경우 포맷은 'video/xxx/movie.mp4'입니다.
getPresignedURLRequest.object = @"exampleobject";

[getPresignedURLRequest setFinishBlock:^(QCloudGetPresignedURLResult * _Nonnull result,
                                         NSError * _Nonnull error) {
    // 사전 서명된 URL
    NSString* presignedURL = result.presienedURL;
   
}];

[[QCloudCOSXMLService defaultCOSXML] getPresignedURL:getPresignedURLRequest];
```

>?전체 예시는 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Objc/Examples/cases/ObjectPresignUrl.m)를 참조하십시오.

**Swift**

[//]: # (.cssg-snippet-get-presign-download-url)
```swift
let getPresign  = QCloudGetPresignedURLRequest.init();

// BucketName-APPID 포맷의 버킷 이름
getPresign.bucket = "examplebucket-1250000000" ;

// // 사전 서명된 URL로 요청하는 HTTP 방법. 유효 값(대소문자 구분):
// @'GET', @'PUT', @'POST', @'DELETE'
getPresign.httpMethod = "GET";

// 객체 키는 객체의 COS 상의 전체 경로로, 디렉터리가 있을 경우 포맷은 'video/xxx/movie.mp4'입니다.
getPresign.object = "exampleobject";
getPresign.setFinish { (result, error) in
    if let result = result {
        let url = result.presienedURL
    } else {
        print(error!);
    }
}
QCloudCOSXMLService.defaultCOSXML().getPresignedURL(getPresign);
```

>?전체 예시는 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Swift/Examples/cases/ObjectPresignUrl.swift)를 참조하십시오.

