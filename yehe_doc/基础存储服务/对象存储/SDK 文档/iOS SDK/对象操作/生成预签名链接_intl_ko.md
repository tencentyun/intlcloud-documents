## 소개

본 문서는 객체의 사전 서명된 링크 생성에 대한 예시 코드를 제공합니다.

>?
> - 사용자는 임시 키를 사용하여 사전 서명을 생성하고, 임시 승인을 통해 사전 서명 업로드 및 다운로드 요청의 보안성을 강화할 것을 권장합니다. 임시 키 신청 시, [최소 권한의 원칙 관련 가이드](https://intl.cloud.tencent.com/document/product/436/32972)를 준수하여 타깃 버킷이나 객체 이외의 리소스가 유출되지 않도록 하시기 바랍니다.
> - 사전 서명 생성을 위해 영구 키를 사용해야 하는 경우, 리스크 방지를 위해 영구 키 권한을 업로드 또는 다운로드 작업으로 제한할 것을 권장합니다.
> 


## SDK API 참고

SDK 모든 인터페이스의 구체적인 매개변수와 방법 설명은 [SDK API](https://cos-ios-sdk-doc-1253960454.file.myqcloud.com/)를 참고하십시오.

## 객체 사전 서명된 링크 생성

#### 예시 코드1: 사전 서명된 업로드 링크 생성
**Objective-C**

[//]: # (.cssg-snippet-get-presign-upload-url)
```objective-c
QCloudGetPresignedURLRequest* getPresignedURLRequest = [[QCloudGetPresignedURLRequest alloc] init];

// BucketName-Appid로 구성된 버킷의 이름. COS 콘솔에서 확인 가능 https://console.cloud.tencent.com/cos5/bucket
getPresignedURLRequest.bucket = @"examplebucket-1250000000";

// 사전 서명된 URL로 요청하는 HTTP 방법. 유효 값(대소문자 구분): @'GET', @'PUT', @'POST', @'DELETE'
getPresignedURLRequest.HTTPMethod = @"PUT";

// 사전 서명된 URL 함수를 가져옵니다. 기본적으로 Header Host에 서명됩니다. Header Host에 서명되지 않도록 선택할 수도 있으나, 요청 실패 또는 취약성이 발생할 수 있습니다.
getPresignedURLRequest.signHost = YES;

// http 요청 매개변수. 실제 요청에 전달된 것과 동일해야 사용자가 HTTP 요청 매개변수를 변경하는 것을 방지할 수 있습니다.
getPresignedURLRequest.requestParameters = @{@"param1":@"value1",@"param1":@"value1"};

// 실제 요청에 포함되어야 하는 http 요청 헤더. 이를 통해 사용자가 HTTP 요청 매개변수를 변경하는 것을 방지할 수 있습니다.
getPresignedURLRequest.requestHeaders = @{@"param1":@"value1",@"param1":@"value1"};

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

[//]: # (.cssg-snippet-get-presign-upload-url)
```swift
let getPresign  = QCloudGetPresignedURLRequest.init();

// BucketName-Appid로 구성된 버킷의 이름. COS 콘솔에서 확인 가능 https://console.cloud.tencent.com/cos5/bucket
getPresign.bucket = "examplebucket-1250000000" ;

// 사전 서명된 URL로 요청하는 HTTP 방법. 유효 값(대소문자 구분):
// @"GET"、@"PUT"、@"POST"、@"DELETE"
getPresign.httpMethod = "PUT";

// 사전 서명된 URL 함수를 가져옵니다. 기본적으로 Header Host에 서명됩니다. Header Host에 서명되지 않도록 선택할 수도 있으나, 요청 실패 또는 취약성이 발생할 수 있습니다.
getPresignedURLRequest.signHost = YES;

// http 요청 매개변수. 실제 요청에 전달된 것과 동일해야 사용자가 HTTP 요청 매개변수를 변경하는 것을 방지할 수 있습니다.
getPresignedURLRequest.requestParameters = {"param1":"value1","param1":"value1"};

// 실제 요청에 포함되어야 하는 http 요청 헤더. 이를 통해 사용자가 HTTP 요청 매개변수를 변경하는 것을 방지할 수 있습니다.
getPresignedURLRequest.requestHeaders = {"param1":"value1","param1":"value1"};

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

#### 예시 코드2: 사전 서명된 다운로드 링크 생성
**Objective-C**

[//]: # (.cssg-snippet-get-presign-download-url)
```objective-c
QCloudGetPresignedURLRequest* getPresignedURLRequest = [[QCloudGetPresignedURLRequest alloc] init];

// BucketName-Appid로 구성된 버킷의 이름. COS 콘솔에서 확인 가능 https://console.cloud.tencent.com/cos5/bucket
getPresignedURLRequest.bucket = @"examplebucket-1250000000";

// 사전 서명된 URL로 요청하는 HTTP 방법. 유효 값(대소문자 구분): @'GET', @'PUT', @'POST', @'DELETE'
getPresignedURLRequest.HTTPMethod = @"GET";

// 사전 서명된 URL 함수를 가져옵니다. 기본적으로 Header Host에 서명됩니다. Header Host에 서명되지 않도록 선택할 수도 있으나, 요청 실패 또는 취약성이 발생할 수 있습니다.
getPresignedURLRequest.signHost = YES;

// http 요청 매개변수. 실제 요청에 전달된 것과 동일해야 사용자가 HTTP 요청 매개변수를 변경하는 것을 방지할 수 있습니다.
getPresignedURLRequest.requestParameters = @{@"param1":@"value1",@"param1":@"value1"};

// 실제 요청에 포함되어야 하는 http 요청 헤더. 이를 통해 사용자가 HTTP 요청 매개변수를 변경하는 것을 방지할 수 있습니다.
getPresignedURLRequest.requestHeaders = @{@"param1":@"value1",@"param1":@"value1"};

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

// BucketName-Appid로 구성된 버킷의 이름. COS 콘솔에서 확인 가능 https://console.cloud.tencent.com/cos5/bucket
getPresign.bucket = "examplebucket-1250000000" ;

// 사전 서명된 URL로 요청하는 HTTP 방법. 유효 값(대소문자 구분):
// @"GET"、@"PUT"、@"POST"、@"DELETE"
getPresign.httpMethod = "GET";

// 사전 서명된 URL 함수를 가져옵니다. 기본적으로 Header Host에 서명됩니다. Header Host에 서명되지 않도록 선택할 수도 있으나, 요청 실패 또는 취약성이 발생할 수 있습니다.
getPresignedURLRequest.signHost = YES;

// http 요청 매개변수. 실제 요청에 전달된 것과 동일해야 사용자가 HTTP 요청 매개변수를 변경하는 것을 방지할 수 있습니다.
getPresignedURLRequest.requestParameters = {"param1":"value1","param1":"value1"};

// 실제 요청에 포함되어야 하는 http 요청 헤더. 이를 통해 사용자가 HTTP 요청 매개변수를 변경하는 것을 방지할 수 있습니다.
getPresignedURLRequest.requestHeaders = {"param1":"value1","param1":"value1"};

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

