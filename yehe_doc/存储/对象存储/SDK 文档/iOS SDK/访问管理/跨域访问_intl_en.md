## Overview

This document provides an overview of APIs and SDK sample codes related to cross-origin access (or cross-origin resource sharing, CORS).

| API | Operation | Description |
| ------------------------------------------------------------ | ------------ | ------------------------------ |
| [PUT Bucket cors](https://intl.cloud.tencent.com/document/product/436/8279) | Setting cross-origin access configuration | Sets cross-origin access permissions for a bucket |
| [GET Bucket cors](https://intl.cloud.tencent.com/document/product/436/8274) | Querying cross-origin access configuration | Queries the cross-origin access configuration of a bucket |
| [DELETE Bucket cors](https://intl.cloud.tencent.com/document/product/436/8283) | Deleting cross-origin access configuration | Deletes the cross-origin access configuration from a bucket |

## SDK API Reference

For the parameters and method descriptions of all the APIs in the SDK, please see [SDK API Reference](https://cos-ios-sdk-doc-1253960454.file.myqcloud.com/).

## Setting Cross-Origin Access Configuration

#### API description 

This API is used to set a cross-origin access (CORS) configuration on a specified bucket.

#### Sample code
**Objective-C**

[//]: # (.cssg-snippet-put-bucket-cors)
```objective-c
QCloudPutBucketCORSRequest* putCORS = [QCloudPutBucketCORSRequest new];
QCloudCORSConfiguration* cors = [QCloudCORSConfiguration new];

QCloudCORSRule* rule = [QCloudCORSRule new];

// Set the rule ID
rule.identifier = @"sdk";

// Custom HTTP request headers allowed in the request. The wildcard "*" is supported.
rule.allowedHeader = @[@"origin",@"host",@"accept",
                       @"content-type",@"authorization"];
rule.exposeHeader = @"ETag";

// Allowed HTTP methods. Enumerated values: GET, PUT, HEAD, POST, DELETE
rule.allowedMethod = @[@"GET",@"PUT",@"POST", @"DELETE", @"HEAD"];

// Set the validity duration of the request result
rule.maxAgeSeconds = 3600;

// Allowed origin; wildcard "*" is supported. Format: protocol://domain name[:port]
rule.allowedOrigin = @"http://cloud.tencent.com";

cors.rules = @[rule];
putCORS.corsConfiguration = cors;

// Bucket name in the format: BucketName-APPID
putCORS.bucket = @"examplebucket-1250000000";

[putCORS setFinishBlock:^(id outputObject, NSError *error) {
    // “outputObject” contains headers returned by the server
    NSDictionary * result = (NSDictionary *)outputObject;
}];

[[QCloudCOSXMLService defaultCOSXML] PutBucketCORS:putCORS];
```

>?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Objc/Examples/cases/BucketCORS.m).

**Swift**

[//]: # (.cssg-snippet-put-bucket-cors)
```swift
let putBucketCorsReq = QCloudPutBucketCORSRequest.init();

let corsConfig = QCloudCORSConfiguration.init();

let rule = QCloudCORSRule.init();

// Set the rule ID
rule.identifier = "rule1";

// Custom HTTP request headers allowed in the request. The wildcard "*" is supported.
rule.allowedHeader = ["origin","host","accept","content-type","authorization"];
rule.exposeHeader = "Etag";

// Allowed HTTP methods. Enumerated values: GET, PUT, HEAD, POST, DELETE
rule.allowedMethod = ["GET","PUT","POST", "DELETE", "HEAD"];

// Set the validity duration of the request result
rule.maxAgeSeconds = 3600;

// Allowed origin; wildcard "*" is supported. Format: protocol://domain name[:port]
rule.allowedOrigin = "*";

corsConfig.rules = [rule];
putBucketCorsReq.corsConfiguration = corsConfig;

// Bucket name in the format: BucketName-APPID
putBucketCorsReq.bucket = "examplebucket-1250000000";
putBucketCorsReq.finishBlock = {(result,error) in
    if let result = result {
        // “result” contains headers returned by the server
    } else {
        print(error!)
    }
}
QCloudCOSXMLService.defaultCOSXML().putBucketCORS(putBucketCorsReq);
```

>?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Swift/Examples/cases/BucketCORS.swift).

## Querying Cross-Origin Access Configuration

#### API description

This API is used to query the cross-origin access (CORS) configuration of a bucket.

#### Sample code
**Objective-C**

[//]: # (.cssg-snippet-get-bucket-cors)
```objective-c
QCloudGetBucketCORSRequest* corsReqeust = [QCloudGetBucketCORSRequest new];

// Bucket name in the format: BucketName-APPID
corsRequest.bucket = @"examplebucket-1250000000";

[corsRequest setFinishBlock:^(QCloudCORSConfiguration * _Nonnull result,
                              NSError * _Nonnull error) {
    // List cross-origin rules
    NSArray<QCloudCORSRule*> *rules = result.rules;
    
}];

[[QCloudCOSXMLService defaultCOSXML] GetBucketCORS:corsReqeust];
```

>?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Objc/Examples/cases/BucketCORS.m).

**Swift**

[//]: # (.cssg-snippet-get-bucket-cors)
```swift
let  getBucketCorsRes = QCloudGetBucketCORSRequest.init();

// Bucket name in the format: BucketName-APPID
getBucketCorsRes.bucket = "examplebucket-1250000000";
getBucketCorsRes.setFinish { (corsConfig, error) in
    if let corsConfig = corsConfig {
        // List cross-origin rules
        let rules = corsConfig.rules
    } else {
        print(error!)
    }
}
QCloudCOSXMLService.defaultCOSXML().getBucketCORS(getBucketCorsRes);
```

>?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Swift/Examples/cases/BucketCORS.swift).

## Deleting Cross-Origin Access Configuration

#### API description

This API is used to delete the cross-origin access (CORS) configuration from a bucket.

#### Sample code
**Objective-C**

[//]: # (.cssg-snippet-delete-bucket-cors)
```objective-c
QCloudDeleteBucketCORSRequest* deleteCORS = [QCloudDeleteBucketCORSRequest new];

// Bucket name in the format: BucketName-APPID
deleteCORS.bucket = @"examplebucket-1250000000";

[deleteCORS setFinishBlock:^(id outputObject, NSError *error) {
    // “outputObject” contains headers returned by the server
   NSDictionary* info = (NSDictionary *) outputObject;
}];
[[QCloudCOSXMLService defaultCOSXML] DeleteBucketCORS:deleteCORS];
```

>?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Objc/Examples/cases/BucketCORS.m).


**Swift**

[//]: # (.cssg-snippet-delete-bucket-cors)
```swift
let deleteBucketCorsRequest = QCloudDeleteBucketCORSRequest.init();

// Bucket name in the format: BucketName-APPID
deleteBucketCorsRequest.bucket = "examplebucket-1250000000";

deleteBucketCorsRequest.finishBlock = {(result,error) in
    if let result = result {
        // “result” contains headers returned by the server
    } else {
        print(error!)
    }
}
QCloudCOSXMLService.defaultCOSXML().deleteBucketCORS(deleteBucketCorsRequest);
```

>?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Swift/Examples/cases/BucketCORS.swift).


