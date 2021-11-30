## Overview

This document provides an overview of SDK code samples related to generating pre-signed object URLs.

>?
> - You are advised to use a temporary key to generate pre-signed URLs for the security of your requests such as uploads and downloads. When you apply for a temporary key, follow the [Principle of Least Privilege](https://intl.cloud.tencent.com/document/product/436/32972) to avoid leaking resources besides your buckets and objects.
> - If you need to use a permanent key to generate a pre-signed URL, you are advised to limit the permission of the permanent key to uploads and downloads only to avoid risks.
> 


## SDK API References

For parameters and method description of all APIs in the SDK, please see [SDK API Reference](https://cos-ios-sdk-doc-1253960454.file.myqcloud.com/).

## Generating a Pre-Signed Object URL

#### Sample code 1. Generating a pre-signed upload URL
**Objective-C**

[//]: # (.cssg-snippet-get-presign-upload-url)
```objective-c
QCloudGetPresignedURLRequest* getPresignedURLRequest = [[QCloudGetPresignedURLRequest alloc] init];

// Bucket name in the format of BucketName-Appid, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
getPresignedURLRequest.bucket = @"examplebucket-1250000000";

// HTTP method of the request using a pre-signed URL. Valid values (case-sensitive): @"GET", @"PUT", @"POST", @"DELETE"
getPresignedURLRequest.HTTPMethod = @"PUT";

// Obtain the pre-signed URL function. By default, it is signed to the Host header. You can also choose not to sign it to Host (the request might fail or vulnerabilities might occur).
getPresignedURLRequest.signHost = YES;

// HTTP request parameters, which should be the same as those passed to the actual request. This can prevent users from tampering with the HTTP request parameters.
getPresignedURLRequest.requestParameters = @{@"param1":@"value1",@"param1":@"value1"};

// HTTP request headers, which should be included in the actual request. This can prevent users from tampering with the HTTP request headers that are signed here.
getPresignedURLRequest.requestHeaders = @{@"param1":@"value1",@"param1":@"value1"};

// Object key, i.e., the full path of a COS object. If the object is in a directory, the format should be "video/xxx/movie.mp4"
getPresignedURLRequest.object = @"exampleobject";

[getPresignedURLRequest setFinishBlock:^(QCloudGetPresignedURLResult * _Nonnull result,
                                         NSError * _Nonnull error) {
    // Pre-Signed URL
    NSString* presignedURL = result.presienedURL;
    
}];

[[QCloudCOSXMLService defaultCOSXML] getPresignedURL:getPresignedURLRequest];
```

>? For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Objc/Examples/cases/ObjectPresignUrl.m).
>

**Swift**

[//]: # (.cssg-snippet-get-presign-upload-url)
```swift
let getPresign  = QCloudGetPresignedURLRequest.init();

// Bucket name in the format of BucketName-Appid, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
getPresign.bucket = "examplebucket-1250000000" ;

// HTTP method of the request using a pre-signed URL. Valid values (case-sensitive):
// @"GET", @"PUT", @"POST", @"DELETE"
getPresign.httpMethod = "PUT";

// Obtain the pre-signed URL function. By default, it is signed to the Host header. You can also choose not to sign it to Host (the request might fail or vulnerabilities might occur).
getPresignedURLRequest.signHost = YES;

// HTTP request parameters, which should be the same as those passed to the actual request. This can prevent users from tampering with the HTTP request parameters.
getPresignedURLRequest.requestParameters = {"param1":"value1","param1":"value1"};

// HTTP request headers, which should be included in the actual request. This can prevent users from tampering with the HTTP request headers that are signed here.
getPresignedURLRequest.requestHeaders = {"param1":"value1","param1":"value1"};

// Object key, i.e., the full path of a COS object. If the object is in a directory, the format should be "video/xxx/movie.mp4"
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

>? For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Swift/Examples/cases/ObjectPresignUrl.swift).
>

#### Sample code 2. Generating a pre-signed download URL
**Objective-C**

[//]: # (.cssg-snippet-get-presign-download-url)
```objective-c
QCloudGetPresignedURLRequest* getPresignedURLRequest = [[QCloudGetPresignedURLRequest alloc] init];

// Bucket name in the format of BucketName-Appid, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
getPresignedURLRequest.bucket = @"examplebucket-1250000000";

// HTTP method of the request using a pre-signed URL. Valid values (case-sensitive): @"GET", @"PUT", @"POST", @"DELETE"
getPresignedURLRequest.HTTPMethod = @"GET";

// Obtain the pre-signed URL function. By default, it is signed to the Host header. You can also choose not to sign it to Host (the request might fail or vulnerabilities might occur).
getPresignedURLRequest.signHost = YES;

// HTTP request parameters, which should be the same as those passed to the actual request. This can prevent users from tampering with the HTTP request parameters.
getPresignedURLRequest.requestParameters = @{@"param1":@"value1",@"param1":@"value1"};

// HTTP request headers, which should be included in the actual request. This can prevent users from tampering with the HTTP request headers that are signed here.
getPresignedURLRequest.requestHeaders = @{@"param1":@"value1",@"param1":@"value1"};

// Object key, i.e., the full path of a COS object. If the object is in a directory, the format should be "video/xxx/movie.mp4"
getPresignedURLRequest.object = @"exampleobject";

[getPresignedURLRequest setFinishBlock:^(QCloudGetPresignedURLResult * _Nonnull result,
                                         NSError * _Nonnull error) {
    // Pre-Signed URL
    NSString* presignedURL = result.presienedURL;
   
}];

[[QCloudCOSXMLService defaultCOSXML] getPresignedURL:getPresignedURLRequest];
```

>? For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Objc/Examples/cases/ObjectPresignUrl.m).
>

**Swift**

[//]: # (.cssg-snippet-get-presign-download-url)
```swift
let getPresign  = QCloudGetPresignedURLRequest.init();

// Bucket name in the format of BucketName-Appid, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
getPresign.bucket = "examplebucket-1250000000" ;

// HTTP method of the request using a pre-signed URL. Valid values (case-sensitive):
// @"GET", @"PUT", @"POST", @"DELETE"
getPresign.httpMethod = "GET";

// Obtain the pre-signed URL function. By default, it is signed to the Host header. You can also choose not to sign it to Host (the request might fail or vulnerabilities might occur).
getPresignedURLRequest.signHost = YES;

// HTTP request parameters, which should be the same as those passed to the actual request. This can prevent users from tampering with the HTTP request parameters.
getPresignedURLRequest.requestParameters = {"param1":"value1","param1":"value1"};

// HTTP request headers, which should be included in the actual request. This can prevent users from tampering with the HTTP request headers that are signed here.
getPresignedURLRequest.requestHeaders = {"param1":"value1","param1":"value1"};

// Object key, i.e., the full path of a COS object. If the object is in a directory, the format should be "video/xxx/movie.mp4"
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

>? For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Swift/Examples/cases/ObjectPresignUrl.swift).
>

