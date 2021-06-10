## Overview

This document provides an overview of APIs and SDK code samples related to bucket and object access control lists (ACL).

**Bucket ACLs**

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | --------------------------------------- |
| [PUT Bucket acl](https://intl.cloud.tencent.com/document/product/436/7737) | Setting a bucket ACL | Sets the ACL for a specified bucket |
| [GET Bucket acl](https://intl.cloud.tencent.com/document/product/436/7733) | Querying a bucket ACL | Queries the ACL of specified bucket |

**Object ACLs**

| API | Operation | Description |
| ------------------------------------------------------------ | ------------ | --------------------------------------------- |
| [PUT Object acl](https://intl.cloud.tencent.com/document/product/436/7748) | Setting an object ACL | Sets an ACL for a specified object in a bucket |
| [GET Object acl](https://intl.cloud.tencent.com/document/product/436/7744) | Querying an object ACL | Queries the ACL of an object |

## SDK API Reference

For the parameters and method descriptions of all the APIs in the SDK, please see [SDK API Reference](https://cos-ios-sdk-doc-1253960454.file.myqcloud.com/).


## Bucket ACLs

### Setting a bucket ACL

#### API description 

This API is used to set the access control list (ACL) on a specified bucket.

#### Sample code
**Objective-C**

[//]: # (.cssg-snippet-put-bucket-acl)
```objective-c
QCloudPutBucketACLRequest* putACL = [QCloudPutBucketACLRequest new];

// ID of the authorized account
NSString* uin = @"100000000001";
NSString *ownerIdentifier = [NSString stringWithFormat:@"qcs::cam::uin/%@:uin/%@"
                             , uin,uin];
NSString *grantString = [NSString stringWithFormat:@"id=\"%@\"",ownerIdentifier];

// Grant read and write permission
putACL.grantFullControl = grantString;

// Grant read permission
putACL.grantRead = grantString;

// Grant write permission
putACL.grantWrite = grantString;

// Bucket name in the format: `BucketName-APPID`
putACL.bucket = @"examplebucket-1250000000";

[putACL setFinishBlock:^(id outputObject, NSError *error) {
    // “outputObject” contains headers returned by the server
    NSDictionary * result = (NSDictionary *)outputObject;

}];
// Set an ACL
[[QCloudCOSXMLService defaultCOSXML] PutBucketACL:putACL];
```

>?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Objc/Examples/cases/BucketACL.m).

**Swift**

[//]: # (.cssg-snippet-put-bucket-acl)
```swift
let putBucketACLReq = QCloudPutBucketACLRequest.init();

// Bucket name in the format: `BucketName-APPID`
putBucketACLReq.bucket = "examplebucket-1250000000";

// ID of the authorized account
let appTD = "100000000001";
let ownerIdentifier = "qcs::cam::uin/\(appTD):uin/\(appTD)";
let grantString = "id=\"\(ownerIdentifier)\"";
// Grants write permission
putBucketACLReq.grantWrite = grantString;

// Grant read permission
putBucketACLReq.grantRead = grantString;

// Grant full control (both read and write permission)
putBucketACLReq.grantFullControl = grantString;

putBucketACLReq.finishBlock = {(result,error) in
    if let result = result {
        // “result” contains headers returned by the server
    } else {
        print(error!)
    }
}
QCloudCOSXMLService.defaultCOSXML().putBucketACL(putBucketACLReq);
```

>?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Swift/Examples/cases/BucketACL.swift).

### Querying a bucket ACL

#### API description 

This API is used to query the access control list (ACL) of a specified bucket.

#### Sample code
**Objective-C**

[//]: # (.cssg-snippet-get-bucket-acl)
```objective-c
QCloudGetBucketACLRequest* getBucketACl = [QCloudGetBucketACLRequest new];

// Bucket name in the format: BucketName-APPID
getBucketACl.bucket = @"examplebucket-1250000000";

[getBucketACl setFinishBlock:^(QCloudACLPolicy * _Nonnull result,
                                       NSError * _Nonnull error) {
    // Grant information, including grantee and permission
    QCloudAccessControlList *acl = result.accessControlList;
}];

[[QCloudCOSXMLService defaultCOSXML] GetBucketACL:getBucketACl];
```

>?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Objc/Examples/cases/BucketACL.m).

**Swift**

[//]: # (.cssg-snippet-get-bucket-acl)
```swift
let getBucketACLReq = QCloudGetBucketACLRequest.init();

// Bucket name in the format: `BucketName-APPID`
getBucketACLReq.bucket = "examplebucket-1250000000";

getBucketACLReq.setFinish { (result, error) in
    if let result = result {
        // ACL grant information
        let acl = result.accessControlList;
    } else {
        print(error!)
    }
}
QCloudCOSXMLService.defaultCOSXML().getBucketACL(getBucketACLReq)
```

>?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Swift/Examples/cases/BucketACL.swift).

## Object ACLs

### Setting an object ACL

#### API description 

This API is used to set the access control list (ACL) on an object in a bucket.

#### Sample code
**Objective-C**

[//]: # (.cssg-snippet-put-object-acl)
```objective-c
QCloudPutObjectACLRequest* request = [QCloudPutObjectACLRequest new];

// Object key, i.e. the full path of a COS object. If the object is in a directory, the path should be "video/xxx/movie.mp4"
request.object = @"exampleobject";

// Bucket name in the format: BucketName-APPID
request.bucket = @"examplebucket-1250000000";

NSString *grantString = [NSString stringWithFormat:@"id=\"%@\"",@"100000000001"];

// grantFullControl grants both read and write permission
// Grant read and write permission
request.grantFullControl = grantString;
// Grant read permission
request.grantRead = grantString;
// Grants write permission
request.grantWrite = grantString;

[request setFinishBlock:^(id outputObject, NSError *error) {
    // “outputObject” returns information such as the Etag or custom headers
    NSDictionary* info = (NSDictionary *) outputObject;
}];

[[QCloudCOSXMLService defaultCOSXML] PutObjectACL:request];
```

>?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Objc/Examples/cases/ObjectACL.m).

**Swift**

[//]: # (.cssg-snippet-put-object-acl)
```swift
let putObjectACl = QCloudPutObjectACLRequest.init();

// Bucket name in the format: `BucketName-APPID`
putObjectACl.bucket = "examplebucket-1250000000";

// Object key, i.e. the full path of a COS object. If the object is in a directory, the format should be: "video/xxx/movie.mp4"
putObjectACl.object = "exampleobject";
let grantString = "id=\"100000000001\"";

// grantFullControl grants both read and write permission
putObjectACl.grantFullControl = grantString;
// Grant read permission
putObjectACl.grantRead = grantString;


putObjectACl.finishBlock = {(result,error)in
    if let result = result {
        // “result” contains response headers
    } else {
        print(error!);
    }
}
QCloudCOSXMLService.defaultCOSXML().putObjectACL(putObjectACl);
```

>?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Swift/Examples/cases/ObjectACL.swift).

### Querying an object ACL

#### API description 

This API is used to query the ACL of an object.

#### Sample code
**Objective-C**

[//]: # (.cssg-snippet-get-object-acl)
```objective-c
QCloudGetObjectACLRequest *request = [QCloudGetObjectACLRequest new];

// Object key, i.e. the full path of a COS object. If the object is in a directory, the path should be "video/xxx/movie.mp4"
request.object = @"exampleobject";

// Bucket name in the format: BucketName-APPID
request.bucket = @"examplebucket-1250000000";

__block QCloudACLPolicy* policy;
[request setFinishBlock:^(QCloudACLPolicy * _Nonnull result,
                          NSError * _Nonnull error) {
    
    policy = result;
    // “result.accessControlList” contains information on the grantee and granted permission
    // “result.owner” is the object owner
}];

[[QCloudCOSXMLService defaultCOSXML] GetObjectACL:request];
```
>?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Objc/Examples/cases/ObjectACL.m).



**Swift**

[//]: # (.cssg-snippet-get-object-acl)
```swift
let getObjectACL = QCloudGetObjectACLRequest.init();

// Bucket name in the format: `BucketName-APPID`
getObjectACL.bucket = "examplebucket-1250000000";

// Object key, i.e. the full path of a COS object. If the object is in a directory, the path should be "video/xxx/movie.mp4"
getObjectACL.object = "exampleobject";
getObjectACL.setFinish { (result, error) in
    if let result = result {
        // ACL grant information
        let acl = result.accessControlList
    } else {
        print(error!);
    }
}
QCloudCOSXMLService.defaultCOSXML().getObjectACL(getObjectACL);
```
>?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Swift/Examples/cases/ObjectACL.swift).



