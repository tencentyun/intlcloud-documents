## Overview

This document provides an overview of APIs and SDK sample codes related to cross-origin access.

| API | Operation | Description |
| ------------------------------------------------------------ | ------------ | ------------------------------ |
| [PUT Bucket cors](https://intl.cloud.tencent.com/document/product/436/8279) | Setting a cross-origin access configuration | Sets the cross-origin access permissions for a bucket |
| [GET Bucket cors](https://intl.cloud.tencent.com/document/product/436/8274) | Querying a cross-origin access configuration | Queries the cross-origin access configuration of a bucket |
| [DELETE Bucket cors](https://intl.cloud.tencent.com/document/product/436/8283) | Deleting a cross-origin access configuration | Deletes the cross-origin access configuration of a bucket |

## SDK API References

For the parameters and method descriptions of all the APIs in the SDK, see [SDK API References](https://cos-ios-sdk-doc-1253960454.file.myqcloud.com/).

## Setting a Cross-Origin Access Configuration

#### API description 

This API is used to set the cross-origin access configuration of a bucket.

#### Sample code
**Objective-C**

[//]: # (.cssg-snippet-put-bucket-cors)
```objective-c
QCloudPutBucketCORSRequest* putCORS = [QCloudPutBucketCORSRequest new];
QCloudCORSConfiguration* cors = [QCloudCORSConfiguration new];

QCloudCORSRule* rule = [QCloudCORSRule new];

// Set the rule ID
rule.identifier = @"sdk";

// Notify the server which custom HTTP request headers are allowed for subsequent requests when an OPTIONS request is sent. Wildcard "*" is supported
rule.allowedHeader = @[@"origin",@"host",@"accept",
                       @"content-type",@"authorization"];
rule.exposeHeader = @"ETag";

// Allowed HTTP methods. Enumerated values: GET, PUT, HEAD, POST, DELETE
rule.allowedMethod = @[@"GET",@"PUT",@"POST", @"DELETE", @"HEAD"];

// Set the validity period of the OPTIONS request result
rule.maxAgeSeconds = 3600;

// Allowed access source; wildcard "*" is supported. Format: protocol://domain name[:port]
rule.allowedOrigin = @"http://cloud.tencent.com";
cors.rules = @[rule];
putCORS.corsConfiguration = cors;

// Bucket name in the format: BucketName-APPID
putCORS.bucket = @"examplebucket-1250000000";

[putCORS setFinishBlock:^(id outputObject, NSError *error) {
    // You can get the headers returned by the server from outputObject
    NSDictionary * result = (NSDictionary *)outputObject;
}];

[[QCloudCOSXMLService defaultCOSXML] PutBucketCORS:putCORS];
```

>?For more samples, go to [GitHub](https://github.com/tencentyun/qcloud-sdk-ios-samples/tree/master/COSAPIDemo/Objc/Examples/cases/BucketCORS.m).

**Swift**

[//]: # (.cssg-snippet-put-bucket-cors)
```swift
let putBucketCorsReq = QCloudPutBucketCORSRequest.init();

let corsConfig = QCloudCORSConfiguration.init();

let rule = QCloudCORSRule.init();

// Set the rule ID
rule.identifier = "rule1";

// Notify the server which custom HTTP request headers are allowed for subsequent requests when an OPTIONS request is sent. Wildcard "*" is supported
rule.allowedHeader = ["origin","host","accept","content-type","authorization"];
rule.exposeHeader = "Etag";

// Allowed HTTP methods. Enumerated values: GET, PUT, HEAD, POST, DELETE
rule.allowedMethod = ["GET","PUT","POST", "DELETE", "HEAD"];

// Set the validity period of the OPTIONS request result
rule.maxAgeSeconds = 3600;

// Allowed access source; wildcard "*" is supported. Format: protocol://domain name[:port]
rule.allowedOrigin = "*";

corsConfig.rules = [rule];

putBucketCorsReq.corsConfiguration = corsConfig;

// Bucket name in the format: BucketName-APPID
putBucketCorsReq.bucket = "examplebucket-1250000000";
putBucketCorsReq.finishBlock = {(result,error) in
    // result returns the response headers
    if error != nil{
        print(error!);
    }else{
        print(result!);
    }
}
QCloudCOSXMLService.defaultCOSXML().putBucketCORS(putBucketCorsReq);
```

>?For more samples, go to [GitHub](https://github.com/tencentyun/qcloud-sdk-ios-samples/tree/master/COSAPIDemo/Swift/Examples/cases/BucketCORS.swift).

## Querying a Cross-Origin Configuration

#### API description

This API is used to query the cross-origin access configuration of a bucket.

#### Sample code
**Objective-C**

[//]: # (.cssg-snippet-get-bucket-cors)
```objective-c
QCloudGetBucketCORSRequest* corsRequest = [QCloudGetBucketCORSRequest new];

// Bucket name in the format: BucketName-APPID
corsRequest.bucket = @"examplebucket-1250000000";

[corsRequest setFinishBlock:^(QCloudCORSConfiguration * _Nonnull result,
                              NSError * _Nonnull error) {
    // List cross-origin rules
    NSArray<QCloudCORSRule*> *rules = result.rules;
    
}];

[[QCloudCOSXMLService defaultCOSXML] GetBucketCORS:corsRequest];
```

>?For more samples, go to [GitHub](https://github.com/tencentyun/qcloud-sdk-ios-samples/tree/master/COSAPIDemo/Objc/Examples/cases/BucketCORS.m).

**Swift**

[//]: # (.cssg-snippet-get-bucket-cors)
```swift
let  getBucketCorsRes = QCloudGetBucketCORSRequest.init();

// Bucket name in the format: BucketName-APPID
getBucketCorsRes.bucket = "examplebucket-1250000000";
getBucketCorsRes.setFinish { (corsConfig, error) in
    // corsConfig contains the CORS settings
    if error != nil{
        print(error!);
    }else{
        print(corsConfig!);
    }
}
QCloudCOSXMLService.defaultCOSXML().getBucketCORS(getBucketCorsRes);
```

>?For more samples, go to [GitHub](https://github.com/tencentyun/qcloud-sdk-ios-samples/tree/master/COSAPIDemo/Swift/Examples/cases/BucketCORS.swift).

## Deleting a Cross-Origin Configuration

#### API description

This API is used to delete the cross-origin access configuration of a bucket.

#### Sample code
**Objective-C**

[//]: # (.cssg-snippet-delete-bucket-cors)
```objective-c
QCloudDeleteBucketCORSRequest* deleteCORS = [QCloudDeleteBucketCORSRequest new];

// Bucket name in the format: BucketName-APPID
deleteCORS.bucket = @"examplebucket-1250000000";

[deleteCORS setFinishBlock:^(id outputObject, NSError *error) {
    // You can get the headers returned by the server from outputObject
   NSDictionary* info = (NSDictionary *) outputObject;
}];
[[QCloudCOSXMLService defaultCOSXML] DeleteBucketCORS:deleteCORS];
```

>?For more samples, go to [GitHub](https://github.com/tencentyun/qcloud-sdk-ios-samples/tree/master/COSAPIDemo/Objc/Examples/cases/BucketCORS.m).


**Swift**

[//]: # (.cssg-snippet-delete-bucket-cors)
```swift
let deleteBucketCorsRequest = QCloudDeleteBucketCORSRequest.init();

// Bucket name in the format: BucketName-APPID
deleteBucketCorsRequest.bucket = "examplebucket-1250000000";

deleteBucketCorsRequest.finishBlock = {(result,error) in
    // result returns the response headers
    if error != nil{
        print(error!);
    }else{
        print(result!);
    }
}
QCloudCOSXMLService.defaultCOSXML().deleteBucketCORS(deleteBucketCorsRequest);
```

>?For more samples, go to [GitHub](https://github.com/tencentyun/qcloud-sdk-ios-samples/tree/master/COSAPIDemo/Swift/Examples/cases/BucketCORS.swift).


