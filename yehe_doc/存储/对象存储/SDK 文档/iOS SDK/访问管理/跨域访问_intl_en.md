## Overview

This document provides an overview of APIs and SDK sample codes for cross-origin resource sharing (CORS).

| API | Operation | Description |
| ------------------------------------------------------------ | ------------ | ------------------------------ |
| [PUT Bucket cors](https://intl.cloud.tencent.com/document/product/436/8279) | Setting CORS configuration | Sets the CORS permissions of bucket |
| [GET Bucket cors](https://intl.cloud.tencent.com/document/product/436/8274) | Querying CORS configuration | Queries the CORS configuration of a bucket |
| [DELETE Bucket cors](https://intl.cloud.tencent.com/document/product/436/8283) | Deleting CORS configuration | Deletes the CORS configuration of a bucket |

## SDK API References

For parameters and method description of all APIs in the SDK, see [SDK API Reference](https://cos-ios-sdk-doc-1253960454.file.myqcloud.com/).

## Setting CORS Configuration

#### Feature description

This API is used to set the CORS configuration of a specified bucket.

#### Sample code
**Objective-C**

[//]: # (.cssg-snippet-put-bucket-cors)
```objective-c
QCloudPutBucketCORSRequest* putCORS = [QCloudPutBucketCORSRequest new];
QCloudCORSConfiguration* cors = [QCloudCORSConfiguration new];

QCloudCORSRule* rule = [QCloudCORSRule new];

// Set rule ID
rule.identifier = @"sdk";

// Allowed HTTP request headers. The wildcard "*" is supported.
rule.allowedHeader = @[@"origin",@"host",@"accept",
                       @"content-type",@"authorization"];
rule.exposeHeader = @"ETag";

// Allowed HTTP method values (such as GET, PUT, HEAD, POST and DELETE)
rule.allowedMethod = @[@"GET",@"PUT",@"POST", @"DELETE", @"HEAD"];

// Validity period of results
rule.maxAgeSeconds = 3600;

// Allowed origin in the format of `protocol://domain name[:port number]`. The wildcard * is supported.
rule.allowedOrigin = @"http://cloud.tencent.com";

cors.rules = @[rule];
putCORS.corsConfiguration = cors;

// Bucket name in the format of BucketName-APPID, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
putCORS.bucket = @"examplebucket-1250000000";

[putCORS setFinishBlock:^(id outputObject, NSError *error) {
    // You can get the header information returned by the server from outputObject
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

// Set rule ID
rule.identifier = "rule1";

// Allowed HTTP request headers. The wildcard "*" is supported.
rule.allowedHeader = ["origin","host","accept","content-type","authorization"];
rule.exposeHeader = "Etag";

// Allowed HTTP method values (such as GET, PUT, HEAD, POST and DELETE)
rule.allowedMethod = ["GET","PUT","POST", "DELETE", "HEAD"];

// Validity period of results
rule.maxAgeSeconds = 3600;

// Allowed origin in the format of `protocol://domain name[:port number]`. The wildcard * is supported.
rule.allowedOrigin = "*";

corsConfig.rules = [rule];
putBucketCorsReq.corsConfiguration = corsConfig;

// Bucket name in the format of BucketName-APPID, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
putBucketCorsReq.bucket = "examplebucket-1250000000";
putBucketCorsReq.finishBlock = {(result,error) in
    if let result = result {
        // You can get the header information returned by the server from result
    } else {
        print(error!)
    }
}
QCloudCOSXMLService.defaultCOSXML().putBucketCORS(putBucketCorsReq);
```

>?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Swift/Examples/cases/BucketCORS.swift).

## Querying CORS Configuration

#### Feature description

This API is used to query the CORS configuration of a bucket.

#### Sample code
**Objective-C**

[//]: # (.cssg-snippet-get-bucket-cors)
```objective-c
QCloudGetBucketCORSRequest* corsRequest = [QCloudGetBucketCORSRequest new];

// Bucket name in the format of BucketName-APPID, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
corsRequest.bucket = @"examplebucket-1250000000";

[corsRequest setFinishBlock:^(QCloudCORSConfiguration * _Nonnull result,
                              NSError * _Nonnull error) {
    // List of CORS rules
    NSArray<QCloudCORSRule*> *rules = result.rules;
    
}];

[[QCloudCOSXMLService defaultCOSXML] GetBucketCORS:corsRequest];
```

>?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Objc/Examples/cases/BucketCORS.m).

**Swift**

[//]: # (.cssg-snippet-get-bucket-cors)
```swift
let  getBucketCorsRes = QCloudGetBucketCORSRequest.init();

// Bucket name in the format of BucketName-APPID, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
getBucketCorsRes.bucket = "examplebucket-1250000000";
getBucketCorsRes.setFinish { (corsConfig, error) in
    if let corsConfig = corsConfig {
        // List of CORS rules
        let rules = corsConfig.rules
    } else {
        print(error!)
    }
}
QCloudCOSXMLService.defaultCOSXML().getBucketCORS(getBucketCorsRes);
```

>?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Swift/Examples/cases/BucketCORS.swift).

## Deleting CORS Configuration

#### Feature description

This API is used to delete the CORS configuration of a bucket.

#### Sample code
**Objective-C**

[//]: # (.cssg-snippet-delete-bucket-cors)
```objective-c
QCloudDeleteBucketCORSRequest* deleteCORS = [QCloudDeleteBucketCORSRequest new];

// Bucket name in the format of BucketName-APPID, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
deleteCORS.bucket = @"examplebucket-1250000000";

[deleteCORS setFinishBlock:^(id outputObject, NSError *error) {
    // You can get the header information returned by the server from outputObject
   NSDictionary* info = (NSDictionary *) outputObject;
}];
[[QCloudCOSXMLService defaultCOSXML] DeleteBucketCORS:deleteCORS];
```

>?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Objc/Examples/cases/BucketCORS.m).


**Swift**

[//]: # (.cssg-snippet-delete-bucket-cors)
```swift
let deleteBucketCorsRequest = QCloudDeleteBucketCORSRequest.init();

// Bucket name in the format of BucketName-APPID, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
deleteBucketCorsRequest.bucket = "examplebucket-1250000000";

deleteBucketCorsRequest.finishBlock = {(result,error) in
    if let result = result {
        // You can get the header information returned by the server from result
    } else {
        print(error!)
    }
}
QCloudCOSXMLService.defaultCOSXML().deleteBucketCORS(deleteBucketCorsRequest);
```

>?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Swift/Examples/cases/BucketCORS.swift).


