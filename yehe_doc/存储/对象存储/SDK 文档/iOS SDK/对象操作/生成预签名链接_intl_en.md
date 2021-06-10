## Overview
This document provides an overview of SDK code samples related to generating pre-signed object links.

## SDK API Reference

For the parameters and method descriptions of all the APIs in the SDK, please see [SDK API Reference](https://cos-ios-sdk-doc-1253960454.file.myqcloud.com/).

## Generating a Pre-signed Object Link

#### Sample 1. Generating a pre-signed upload link
**Objective-C**

[//]: # (.cssg-snippet-get-presign-upload-url)
```objective-c
QCloudGetPresignedURLRequest* getPresignedURLRequest = [[QCloudGetPresignedURLRequest alloc] init];

// Bucket name in the format: `BucketName-APPID`
getPresignedURLRequest.bucket = @"examplebucket-1250000000";

// HTTP method of the request using a pre-signed URL. Valid values (case-sensitive): @"GET", @"PUT", @"POST", @"DELETE"
getPresignedURLRequest.HTTPMethod = @"PUT";

// Object key, i.e. the full path of a COS object. If the object is in a directory, the path should be "video/xxx/movie.mp4"
getPresignedURLRequest.object = @"exampleobject";

[getPresignedURLRequest setFinishBlock:^(QCloudGetPresignedURLResult * _Nonnull result,
                                         NSError * _Nonnull error) {
    
    // Pre-signed URL
    NSString* presignedURL = result.presienedURL;
    
}];

[[QCloudCOSXMLService defaultCOSXML] getPresignedURL:getPresignedURLRequest];
```

>?For more samples, please visit [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Objc/Examples/cases/ObjectPresignUrl.m).

**Swift**

[//]: # (.cssg-snippet-get-presign-upload-url)
```swift
let getPresign  = QCloudGetPresignedURLRequest.init();

// Bucket name in the format: `BucketName-APPID`
getPresign.bucket = "examplebucket-1250000000" ;

// HTTP method of the request using a pre-signed URL. Valid values (case-sensitive):
// @"GET", @"PUT", @"POST", @"DELETE"
getPresign.httpMethod = "PUT";

// Object key, i.e. the full path of a COS object. If the object is in a directory, the path should be "video/xxx/movie.mp4"
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

>?For more samples, please visit [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Swift/Examples/cases/ObjectPresignUrl.swift).

#### Sample 2. Generating a pre-signed download link
**Objective-C**

[//]: # (.cssg-snippet-get-presign-download-url)
```objective-c
QCloudGetPresignedURLRequest* getPresignedURLRequest = [[QCloudGetPresignedURLRequest alloc] init];

// Bucket name in the format: `BucketName-APPID`
getPresignedURLRequest.bucket = @"examplebucket-1250000000";

// HTTP method of the request using a pre-signed URL. Valid values (case-sensitive): @"GET", @"PUT", @"POST", @"DELETE"
getPresignedURLRequest.HTTPMethod = @"GET";

// Object key, i.e. the full path of a COS object. If the object is in a directory, the path should be "video/xxx/movie.mp4"
getPresignedURLRequest.object = @"exampleobject";

[getPresignedURLRequest setFinishBlock:^(QCloudGetPresignedURLResult * _Nonnull result,
                                         NSError * _Nonnull error) {
    // Pre-signed URL
    NSString* presignedURL = result.presienedURL;
   
}];

[[QCloudCOSXMLService defaultCOSXML] getPresignedURL:getPresignedURLRequest];
```

>?For more samples, please visit [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Objc/Examples/cases/ObjectPresignUrl.m).

**Swift**

[//]: # (.cssg-snippet-get-presign-download-url)
```swift
let getPresign  = QCloudGetPresignedURLRequest.init();

// Bucket name in the format: `BucketName-APPID`
getPresign.bucket = "examplebucket-1250000000" ;

// HTTP method of the request using a pre-signed URL. Valid values (case-sensitive):
// @"GET", @"PUT", @"POST", @"DELETE"
getPresign.httpMethod = "GET";

// Object key, i.e. the full path of a COS object. If the object is in a directory, the path should be "video/xxx/movie.mp4"
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

>?For more samples, please visit [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Swift/Examples/cases/ObjectPresignUrl.swift).

