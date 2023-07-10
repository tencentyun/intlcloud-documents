## 소개

본 문서는 객체 액세스 URL을 획득하는 코드 예시를 제공합니다.

>?
> - 객체 액세스 URL을 조회합니다. 해당 인터페이스는 객체의 실제 존재 여부를 판단하지 않습니다.
> - 파일에 개인 읽기 권한이 있는 경우 이 인터페이스에서 생성된 URL을 사용하여 리소스에 직접 액세스할 수 없으며 [사전 서명 링크 생성](https://intl.cloud.tencent.com/document/product/436/37690) 문서를 통해 URL을 생성할 수 있습니다.

## SDK API 참고

SDK 모든 인터페이스의 구체적인 매개변수와 방법 설명은 [SDK API](https://cos-ios-sdk-doc-1253960454.file.myqcloud.com/)를 참고하십시오.

## 객체 액세스 URL 가져오기

#### 예시 코드1: 객체 액세스 URL 가져오기
**Objective-C**

[//]: # (.cssg-snippet-get-presign-download-url)
```objective-c
QCloudGetPresignedURLRequest* getPresignedURLRequest = [[QCloudGetPresignedURLRequest alloc] init];

// 생성된 링크에는 서명이 없습니다.
getPresignedURLRequest.isUseSignature = false:

// BucketName-Appid로 구성된 버킷의 이름. COS 콘솔에서 볼 수 있습니다. https://console.cloud.tencent.com/cos5/bucket
getPresignedURLRequest.bucket = @"examplebucket-1250000000";

// 객체 키. 객체의 COS 상의 전체 경로로, 디렉터리가 있을 경우 형식은 "video/xxx/movie.mp4"입니다.
getPresignedURLRequest.object = @"exampleobject";

[getPresignedURLRequest setFinishBlock:^(QCloudGetPresignedURLResult * _Nonnull result,
                                         NSError * _Nonnull error) {
    // 사전 서명된 URL
    NSString* presignedURL = result.presienedURL;
   
}];

[[QCloudCOSXMLService defaultCOSXML] getPresignedURL:getPresignedURLRequest];
```

>? 전체 예시는 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Objc/Examples/cases/ObjectPresignUrl.m)를 참고하십시오.
>

**Swift**

[//]: # (.cssg-snippet-get-presign-download-url)
```swift
let getPresign  = QCloudGetPresignedURLRequest.init();

// 생성된 링크에는 서명이 없습니다.
getPresign.isUseSignature = false;
// BucketName-Appid로 구성된 버킷의 이름. COS 콘솔에서 볼 수 있습니다. https://console.cloud.tencent.com/cos5/bucket
getPresign.bucket = "examplebucket-1250000000" ;

// 객체 키. 객체의 COS 상의 전체 경로로, 디렉터리가 있을 경우 형식은 "video/xxx/movie.mp4"입니다.
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

>? 전체 예시는 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Swift/Examples/cases/ObjectPresignUrl.swift)를 참고하십시오.
>

