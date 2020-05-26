

## Overview

This document provides an overview of APIs and SDK code samples related to log management.

| API | Operation Name | Operation Description |
| ------------------------------------------------------------ | ------------ | -------------------------- |
| [PUT Bucket logging](https://intl.cloud.tencent.com/document/product/436/17054) | Setting log management | Enables logging for the source bucket |
| [GET Bucket logging](https://intl.cloud.tencent.com/document/product/436/17053) | Querying log management | Queries the logging configuration information of the source bucket |

## Setting Log Management

#### Feature description

This API (PUT Bucket logging) is used to enable logging for the source bucket and store its access logs in a specified destination bucket.

#### Method prototype

When you start to use COS, you need to create a bucket under a specified account for object use and management and specify the region where the bucket resides. The user who creates a bucket is considered the owner of the bucket by default. If you do not specify the access permission when creating a bucket, the bucket has private read/write ("private") permission. The steps are as follows:    

1. Instantiate `QCloudPutBucketLoggingRequest`
2. Call the `PutBucketLogging` method in the `QCloudCOSXMLService` object to initiate a request.
3. Get the specific content from the `outputObject` in the `finishBlock` of the callback.

#### Sample request

[//]: # (.cssg-snippet-objc-put-bucket-logging)
```
QCloudPutBucketLoggingRequest *request = [QCloudPutBucketLoggingRequest new];
QCloudBucketLoggingStatus *status = [QCloudBucketLoggingStatus new];
QCloudLoggingEnabled *loggingEnabled = [QCloudLoggingEnabled new];
loggingEnabled.targetBucket = @"examplebucket-1250000000";
loggingEnabled.targetPrefix = @"mylogs";
status.loggingEnabled = loggingEnabled;
request.bucketLoggingStatus = status;
request.bucket = @"examplebucket-1250000000";
[request setFinishBlock:^(id outputObject, NSError *error) {

}];
[[QCloudCOSXMLService defaultCOSXML] PutBucketLogging:request];
```

Swift sample code:

[//]: # (.cssg-snippet-swift-put-bucket-logging)
```
let req = QCloudPutBucketLoggingRequest.init();

let status = QCloudBucketLoggingStatus.init();

let loggingEnabled = QCloudLoggingEnabled.init();

loggingEnabled.targetBucket = "examplebucket-1250000000";

loggingEnabled.targetPrefix = "";
status.loggingEnabled = loggingEnabled;
req.bucketLoggingStatus = status;
req.bucket = "examplebucket-1250000000";
req.finishBlock = {(result,error) in

    if error != nil{
        print(error!);
    }else{
        print( result!);
    }
}

QCloudCOSXMLService.defaultCOSXML().putBucketLogging(req);

```

#### Parameter description

#### `QCloudPutBucketLoggingRequest` request parameter description

| Parameter Name | Description | Type | Required |
| ------------------- | ------------------------------------------------------------ | --------------------------- | -------- |
| bucket            | Source bucket for which to enable the logging feature in the format of `BucketName-APPID`. For more information, please see [Naming Convention](https://intl.cloud.tencent.com/document/product/436/13312) | NSString *                  | Yes       |
| bucketLoggingStatus | Indicates the status of the logging configuration                                       | QCloudBucketLoggingStatus * | Yes       |

#### `QCloudBucketLoggingStatus` parameter description

| Parameter Name | Description | Type | Required |
| -------------- | ----------------------------------------------- | ---------------------- | -------- |
| loggingEnabled | Specific information of the bucket logging setting, which is mainly the destination bucket | QCloudLoggingEnabled * | Yes       |

#### `QCloudLoggingEnabled` parameter description

| Parameter Name | Description | Type | Required |
| ------------ | ------------------------------ | ----------- | -------- |
| targetBucket | Destination bucket for storing logs           | NSString  * | Yes       |
| targetPrefix | Specified path in the destination bucket for storing logs | NSString  * | Yes       |



## Querying Log Management

#### Feature description

This API (GET Bucket logging) is used to query the log configuration information of a specified bucket.

#### Method prototype

When you start to use COS, you need to create a bucket under a specified account for object use and management and specify the region where the bucket resides. The user who creates a bucket is considered the owner of the bucket by default. If you do not specify the access permission when creating a bucket, the bucket has private read/write ("private") permission. The steps are as follows:    

1. Instantiate `QCloudGetBucketLoggingRequest`
2. Call the `GetBucketLogging` method in the `QCloudCOSXMLService` object to initiate a request.
3. Get the specific content from the `outputObject` in the `finishBlock` of the callback.



#### Sample request

[//]: # (.cssg-snippet-objc-get-bucket-logging)
```
QCloudGetBucketLoggingRequest *getReq = [QCloudGetBucketLoggingRequest new];
getReq.bucket = @"examplebucket-1250000000";
[getReq setFinishBlock:^(QCloudBucketLoggingStatus * _Nonnull result, NSError * _Nonnull error) {
	NSLog(@"getReq result = %@",result.loggingEnabled.targetBucket);

}];
[[QCloudCOSXMLService defaultCOSXML]GetBucketLogging:getReq];
```

Swift sample code:

[//]: # (.cssg-snippet-swift-get-bucket-logging)
```
let req = QCloudGetBucketLoggingRequest.init();
req.bucket = "examplebucket-1250000000";
req.setFinish { (result, error) in

    if error != nil{
        print(error!);
    }else{
        print( result!);
    }
};
QCloudCOSXMLService.defaultCOSXML().getBucketLogging(req);

```

#### Parameter description

#### `QCloudGetBucketLoggingRequest` request parameter description

| Parameter Name | Description | Type | Required |
| -------- | ------------------------------------------------------------ | ---------- | -------- |
| bucket   | Destination bucket where to store logs in the format of `BucketName-APPID`. For more information, please see [Naming Convention](https://intl.cloud.tencent.com/document/product/436/13312) | NSString * | Yes |

#### Returned result description

#### `QCloudBucketLoggingStatus` parameter description

| Parameter Name | Description | Type |
| -------------- | ----------------------------------------------- | ---------------------- |
| loggingEnabled | Specific information of the bucket logging setting, which is mainly the destination bucket | QCloudLoggingEnabled * |

#### Returned error code description

When an SDK request fails, the returned error will not be empty and will include error code, error message, and other information required for troubleshooting to help developers fix the problem quickly.

There are mainly two types of returned error codes (encapsulated in the returned error): error codes returned by the device for network reasons and error codes returned by COS.

- All the error codes returned by the device for network reasons are 4-digit negative numbers such as -1001, which are defined by Apple. For more information, please see the definitions in the `NSURLError.h` header of the `Foundation` framework or [Apple's official documentation](https://developer.apple.com/documentation/foundation/1508628-url_loading_system_error_codes).
- Error codes returned by COS are based on HTTP status codes such as 404 and 503. For solutions to this type of error codes, please see [API Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).
- All the error codes customized by the SDK are 5-digit positive numbers such as 10000 and 20000. For solutions to this type of error codes, please see [SDK Error Codes](https://intl.cloud.tencent.com/document/product/436/30610).
