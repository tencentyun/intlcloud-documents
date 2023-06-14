## Overview

This document provides an overview of code samples for generating a pre-signed object URL.

For details about how to use a pre-signed URL for uploads, see [Upload via Pre-Signed URL](https://intl.cloud.tencent.com/document/product/436/14114). For details about how to use a pre-signed URL for downloads, see [Download via Pre-Signed URL](https://intl.cloud.tencent.com/document/product/436/14116).

>?
> - We recommend you use a temporary key to generate a pre-signed URL for the security of your requests such as uploads and downloads. When you apply for a temporary key, follow the [principle of least privilege](https://intl.cloud.tencent.com/document/product/436/32972) to avoid leaking resources besides your buckets and objects.
> - If you need to use a permanent key to generate a pre-signed URL, we recommend you limit the permission of the permanent key to uploads and downloads only to avoid risks.
> 


## SDK API References

For the parameters and method description of all the APIs in the SDK, see the [API documentation](https://cos-ios-sdk-doc-1253960454.file.myqcloud.com/).

## Generating Pre-Signed Object URL

#### Sample 1. Generating pre-signed upload URL
**Objective-C**

[//]: # (.cssg-snippet-get-presign-upload-url)
```objective-c
QCloudGetPresignedURLRequest* getPresignedURLRequest = [[QCloudGetPresignedURLRequest alloc] init];

// Bucket name in the format of BucketName-Appid, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
getPresignedURLRequest.bucket = @"examplebucket-1250000000";

// HTTP method of the request using a pre-signed URL. Valid values (case-sensitive): @"GET", @"PUT", @"POST", @"DELETE"
getPresignedURLRequest.HTTPMethod = @"PUT";

// Get the pre-signed URL function. By default, it is signed to the `host` header. You can also choose not to include the `host` header in the signature, but the request may fail or vulnerabilities may occur.
getPresignedURLRequest.signHost = YES;

// HTTP request parameters, which should be the same as those passed to the actual request. This can prevent users from tampering with the HTTP request parameters.
getPresignedURLRequest.requestParameters = @{@"param1":@"value1",@"param1":@"value1"};

// HTTP request headers, which should be included in the actual request. This can prevent users from tampering with the HTTP request headers that are signed here.
getPresignedURLRequest.requestHeaders = @{@"param1":@"value1",@"param1":@"value1"};

// Object key, i.e., the full path of a COS object. If the object is in a directory, the path should be "video/xxx/movie.mp4"
getPresignedURLRequest.object = @"exampleobject";

[getPresignedURLRequest setFinishBlock:^(QCloudGetPresignedURLResult * _Nonnull result,
                                         NSError * _Nonnull error) {
    // Pre-signed URL
    NSString* presignedURL = result.presienedURL;
    // Upload a file through the pre-signed URL
    NSMutableURLRequest *request = [[NSMutableURLRequest alloc] initWithURL:[NSURL URLWithString:result.presienedURL]];
    // Specify `HTTPMethod` as `PUT`
    request.HTTPMethod = @"PUT";
    // `fromData` is the file to be uploaded
    [[[NSURLSession sharedSession]
        uploadTaskWithRequest:request fromData:[@"testtest" dataUsingEncoding:NSUTF8StringEncoding] completionHandler:^(NSData * _Nullable data, NSURLResponse * _Nullable response, NSError * _Nullable error) {
        // View the result in the response
    }]resume];

}];

[[QCloudCOSXMLService defaultCOSXML] getPresignedURL:getPresignedURLRequest];
```

>? For more complete samples, visit [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Objc/Examples/cases/ObjectPresignUrl.m).
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

// Get the pre-signed URL function. By default, it is signed to the `host` header. You can also choose not to include the `host` header in the signature, but the request may fail or vulnerabilities may occur.
getPresign.signHost = YES;

// HTTP request parameters, which should be the same as those passed to the actual request. This can prevent users from tampering with the HTTP request parameters.
getPresign.requestParameters = {"param1":"value1","param1":"value1"};

// HTTP request headers, which should be included in the actual request. This can prevent users from tampering with the HTTP request headers that are signed here.
getPresign.requestHeaders = {"param1":"value1","param1":"value1"};

// Object key, i.e., the full path of a COS object. If the object is in a directory, the path should be "video/xxx/movie.mp4"
getPresign.object = "exampleobject";
getPresign.setFinish { (result, error) in
    if let result = result {
        let url = result.presienedURL
        // Upload a file through the pre-signed URL
        let request = NSMutableURLRequest.init(url: NSURL.init(string:url) as! URL);
        // Specify `HTTPMethod` as `PUT`
        request.httpMethod = "PUT";
        // `fromData` is the file to be uploaded
        URLSession.shared.uploadTask(with: request, from:  "testtest".data(using: String.Encoding.utf8)) { data, res, err in
            // View the result in the response
        }.resume()
    } else {
        print(error!);
    }
}
QCloudCOSXMLService.defaultCOSXML().getPresignedURL(getPresign);
```

>? For more complete samples, visit [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Swift/Examples/cases/ObjectPresignUrl.swift).
>

#### Sample 2. Generating pre-signed download URL
**Objective-C**

[//]: # (.cssg-snippet-get-presign-download-url)
```objective-c
QCloudGetPresignedURLRequest* getPresignedURLRequest = [[QCloudGetPresignedURLRequest alloc] init];

// Bucket name in the format of BucketName-Appid, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
getPresignedURLRequest.bucket = @"examplebucket-1250000000";

// HTTP method of the request using a pre-signed URL. Valid values (case-sensitive): @"GET", @"PUT", @"POST", @"DELETE"
getPresignedURLRequest.HTTPMethod = @"GET";

// Get the pre-signed URL function. By default, it is signed to the `host` header. You can also choose not to include the `host` header in the signature, but the request may fail or vulnerabilities may occur.
getPresignedURLRequest.signHost = YES;

// HTTP request parameters, which should be the same as those passed to the actual request. This can prevent users from tampering with the HTTP request parameters.
getPresignedURLRequest.requestParameters = @{@"param1":@"value1",@"param1":@"value1"};

// HTTP request headers, which should be included in the actual request. This can prevent users from tampering with the HTTP request headers that are signed here.
getPresignedURLRequest.requestHeaders = @{@"param1":@"value1",@"param1":@"value1"};

// Object key, i.e., the full path of a COS object. If the object is in a directory, the path should be "video/xxx/movie.mp4"
getPresignedURLRequest.object = @"exampleobject";

[getPresignedURLRequest setFinishBlock:^(QCloudGetPresignedURLResult * _Nonnull result,
                                         NSError * _Nonnull error) {
    // Pre-signed URL
    NSString* presignedURL = result.presienedURL;
    // Download a file through the pre-signed URL
    NSMutableURLRequest *request = [[NSMutableURLRequest alloc] initWithURL:[NSURL URLWithString:presignedURL]];
    // Specify `HTTPMethod` as `GET`
    request.HTTPMethod = @"GET";
    [[[NSURLSession sharedSession]
        downloadTaskWithRequest:request
                completionHandler:^(NSURL *_Nullable location, NSURLResponse *_Nullable response, NSError *_Nullable error) {
                // `location` is the local file path after successful download
                }] resume];
}];

[[QCloudCOSXMLService defaultCOSXML] getPresignedURL:getPresignedURLRequest];
```

>? For more complete samples, visit [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Objc/Examples/cases/ObjectPresignUrl.m).
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

// Get the pre-signed URL function. By default, it is signed to the `host` header. You can also choose not to include the `host` header in the signature, but the request may fail or vulnerabilities may occur.
getPresignedURLRequest.signHost = YES;

// HTTP request parameters, which should be the same as those passed to the actual request. This can prevent users from tampering with the HTTP request parameters.
getPresignedURLRequest.requestParameters = {"param1":"value1","param1":"value1"};

// HTTP request headers, which should be included in the actual request. This can prevent users from tampering with the HTTP request headers that are signed here.
getPresignedURLRequest.requestHeaders = {"param1":"value1","param1":"value1"};

// Object key, i.e., the full path of a COS object. If the object is in a directory, the path should be "video/xxx/movie.mp4"
getPresign.object = "exampleobject";
getPresign.setFinish { (result, error) in
    if let result = result {
        let url = result.presienedURL
        // Download a file through the pre-signed URL
        let request = NSMutableURLRequest.init(url: NSURL.init(string: url) as! URL);
           // Specify `HTTPMethod` as `GET`
        request.httpMethod = "GET";
        URLSession.shared.downloadTask(with: request) { location, response, error in
            // `location` is the local file path after successful download
        }.resume();
    } else {
        print(error!);
    }
}
QCloudCOSXMLService.defaultCOSXML().getPresignedURL(getPresign);
```

>? For more complete samples, visit [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Swift/Examples/cases/ObjectPresignUrl.swift).
>

