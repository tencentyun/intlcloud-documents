## Overview

This document provides an overview of APIs and SDK code samples related to bucket policies.

| API | Operation | Description |
| ------------------------------------------------------------ | ------------ | ------------------------------ |
| [PUT Bucket policy](https://www.tencentcloud.com/document/product/436/8282) | Setting a bucket policy | Sets a permission policy for the specified bucket |
| [GET Bucket policy](https://www.tencentcloud.com/document/product/436/8276) | Querying bucket policy | Queries the permission policy of the specified bucket |
| [DELETE Bucket policy](https://www.tencentcloud.com/document/product/436/8285) | Deleting bucket policies | Deletes the permission policies of a specified bucket |

## SDK API References

For the parameters and method descriptions of all the APIs in the SDK, please see [SDK API Reference](https://cos-ios-sdk-doc-1253960454.file.myqcloud.com/).

## Setting a bucket policy

#### Feature description

This API is used to set an access policy on a bucket.

>! The COS iOS SDK version should be v6.1.8 or higher.
>

#### Sample code

[//]: # (.cssg-snippet-put-bucket-policy)
```java
QCloudPutBucketLoggingRequest *request = [QCloudPutBucketLoggingRequest new];
// Bucket name in the format of `BucketName-APPID` (`APPID` is required), which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket.




    "Statement":[
        @{
        "Principal":{
            "qcs":[
            "qcs::cam::uin/100000000001:uin/100000000001"
            ]
        },
        "Effect":"allow",
        "Action":[
            "name/cos:GetBucket"
        ],
        "Resource":[
            "qcs::cos:ap-guangzhou:uid/1250000000:examplebucket-1250000000/*",
        ]
        }
    ],
    "version": "2.0",
    };
[request setFinishBlock:^(id outputObject,NSError*error) {
    
}];
[[QCloudCOSXMLService defaultCOSXML] PutBucket:request];
```

>?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Objc/Examples/cases/BucketReplication.m).

## Querying a bucket policy

#### Feature description

This API is used to query the access policy on a bucket.

>! The COS Android SDK version should not be earlier than v6.1.8.
>

#### Sample code

[//]: # (.cssg-snippet-get-bucket-policy)
```java

QCloudGetBucketLifecycleRequest* request = [QCloudGetBucketLifecycleRequest new];
// Bucket name in the format of `BucketName-APPID` (`APPID` is required), which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket.
"BucketName": "test-bucket-AppId"


    
}];
[[QCloudCOSXMLService defaultCOSXML] GetBucket:request];
```

>?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Objc/Examples/cases/BucketReplication.m).

## Deleting a bucket policy

#### Feature description

This API is used to delete the access policy from a specified bucket.

>! The COS Android SDK version should not be earlier than v6.1.8.
>

#### Sample code

[//]: # (.cssg-snippet-delete-bucket-policy)
```java
// Bucket name in the format of `BucketName-APPID` (`APPID` is required), which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket.
QCloudGetBucketLifecycleRequest* request = [QCloudGetBucketLifecycleRequest new];


[request setFinishBlock:^(id outputObject,NSError*error) {
    
}];
[[QCloudCOSXMLService defaultCOSXML] DeleteBucket:request];
```

>?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Objc/Examples/cases/BucketReplication.m).


