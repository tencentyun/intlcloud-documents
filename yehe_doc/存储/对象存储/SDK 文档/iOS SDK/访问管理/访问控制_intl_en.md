## Overview

This document provides an overview of APIs and SDK code samples related to bucket and object access control lists (ACL).

**Bucket ACL**

| API          | Operation                   | Description                                       |
| ------------------------------------------------------------ | -------------- | --------------------------------------- |
| [PUT Bucket acl](https://intl.cloud.tencent.com/document/product/436/7737) | Setting a bucket ACL | Sets the ACL for a specified bucket |
| [GET Bucket acl](https://intl.cloud.tencent.com/document/product/436/7733) | Querying bucket ACL | Queries the ACL of a specified bucket |

**Object ACL**

| API | Operation Name | Description |
| ------------------------------------------------------------ | ------------ | --------------------------------------------- |
| [PUT Object acl](https://intl.cloud.tencent.com/document/product/436/7748) | Setting an object ACL | Sets the ACL for a specified object in a bucket |
| [GET Object acl](https://intl.cloud.tencent.com/document/product/436/7744) | Querying an object ACL | Queries the ACL of an object |

## SDK API References

For parameters and method descriptions of all SDK APIs, see [SDK API References](https://cos-ios-sdk-doc-1253960454.file.myqcloud.com/).


## Bucket ACL

### Setting a bucket ACL

#### API description

This API (PUT Bucket acl) is used to set the access control list (ACL) for a specified bucket.

#### Sample code
**Objective-C**

[//]: # (.cssg-snippet-put-bucket-acl)
```objective-c
QCloudPutBucketACLRequest* putACL = [QCloudPutBucketACLRequest new];

// ID of the grantee account
NSString* uin = @"100000000001";
NSString *ownerIdentifier = [NSString stringWithFormat:@"qcs::cam::uin/%@:uin/%@"
                             , uin,uin];
NSString *grantString = [NSString stringWithFormat:@"id=\"%@\"",ownerIdentifier];

// Grant read and write permissions to the grantee
putACL.grantFullControl = grantString;

// Grant read permissions to the grantee
putACL.grantRead = grantString;

// Grant write permissions to the grantee
putACL.grantWrite = grantString;

// Bucket name in the format of BucketName-APPID
putACL.bucket = @"examplebucket-1250000000";

[putACL setFinishBlock:^(id outputObject, NSError *error) {
    // You can get the headers returned by the server from outputObject
    NSDictionary * result = (NSDictionary *)outputObject;

}];
// Set an ACL
[[QCloudCOSXMLService defaultCOSXML] PutBucketACL:putACL];
```

>?For more samples, go to [GitHub](https://github.com/tencentyun/qcloud-sdk-ios-samples/tree/master/COSAPIDemo/Objc/Examples/cases/BucketACL.m).

**Swift**

[//]: # (.cssg-snippet-put-bucket-acl)
```swift
let putBucketACLReq = QCloudPutBucketACLRequest.init();

// Bucket name in the format of BucketName-APPID
putBucketACLReq.bucket = "examplebucket-1250000000";

// ID of the grantee account
let appTD = "100000000001";
let ownerIdentifier = "qcs::cam::uin/\(appTD):uin/\(appTD)";
let grantString = "id=\"\(ownerIdentifier)\"";
// Grant write permissions to the grantee
putBucketACLReq.grantWrite = grantString;

// Grant read permissions to the grantee
putBucketACLReq.grantRead = grantString;

// Grant full control (read and write permissions) to the grantee grantFullControl == grantRead + grantWrite
putBucketACLReq.grantFullControl = grantString;

putBucketACLReq.finishBlock = {(result,error) in
    // QCloudACLPolicy contains bucket ACL information
    if error != nil{
        print(error!);
    }else{
        print(result!);
    }
}
QCloudCOSXMLService.defaultCOSXML().putBucketACL(putBucketACLReq);
```

>?For more samples, go to [GitHub](https://github.com/tencentyun/qcloud-sdk-ios-samples/tree/master/COSAPIDemo/Swift/Examples/cases/BucketACL.swift).

### Querying bucket ACL

#### API description

This API (GET Bucket acl) is used to query the access control list (ACL) of a specified bucket.

#### Sample code
**Objective-C**

[//]: # (.cssg-snippet-get-bucket-acl)
```objective-c
QCloudGetBucketACLRequest* getBucketACl = [QCloudGetBucketACLRequest new];

// Bucket name in the format of BucketName-APPID
getBucketACl.bucket = @"examplebucket-1250000000";

[getBucketACl setFinishBlock:^(QCloudACLPolicy * _Nonnull result,
                                       NSError * _Nonnull error) {
    // The grantee and permissions
    QCloudAccessControlList *acl = result.accessControlList;
}];

[[QCloudCOSXMLService defaultCOSXML] GetBucketACL:getBucketACl];
```

>?For more samples, go to [GitHub](https://github.com/tencentyun/qcloud-sdk-ios-samples/tree/master/COSAPIDemo/Objc/Examples/cases/BucketACL.m).

**Swift**

[//]: # (.cssg-snippet-get-bucket-acl)
```swift
let getBucketACLReq = QCloudGetBucketACLRequest.init();

// Bucket name in the format of BucketName-APPID
getBucketACLReq.bucket = "examplebucket-1250000000";

getBucketACLReq.setFinish { (result, error) in
    if error != nil{
        print(error!);
    }else{
        print(result!);
        result?.accessControlList; // The grantee and permissions
    }
}
QCloudCOSXMLService.defaultCOSXML().getBucketACL(getBucketACLReq)
```

>?For more samples, go to [GitHub](https://github.com/tencentyun/qcloud-sdk-ios-samples/tree/master/COSAPIDemo/Swift/Examples/cases/BucketACL.swift).

## Object ACL

### Setting an object ACL

#### API description

This API (PUT Object acl) is used to set an access control list (ACL) for an object in a bucket.

#### Sample code
**Objective-C**

[//]: # (.cssg-snippet-put-object-acl)
```objective-c
QCloudPutObjectACLRequest* request = [QCloudPutObjectACLRequest new];

// Object key, which is the full path of a COS object. If the object is in a directory, the format should be like "dir1/object1"
request.object = @"exampleobject";

// Bucket name in the format of BucketName-APPID
request.bucket = @"examplebucket-1250000000";

NSString *grantString = [NSString stringWithFormat:@"id=\"%@\"",@"100000000001"];

// grantFullControl grants both read and write permissions
// Grant read and write permissions to the grantee
request.grantFullControl = grantString;
// Grant read permissions to the grantee
request.grantRead = grantString;
// Grants write permissions to the grantee
request.grantWrite = grantString;

[request setFinishBlock:^(id outputObject, NSError *error) {
    // outputObject returns the etag or custom headers
    NSDictionary* info = (NSDictionary *) outputObject;
}];

[[QCloudCOSXMLService defaultCOSXML] PutObjectACL:request];
```

>?For more samples, go to [GitHub](https://github.com/tencentyun/qcloud-sdk-ios-samples/tree/master/COSAPIDemo/Objc/Examples/cases/ObjectACL.m).

**Swift**

[//]: # (.cssg-snippet-put-object-acl)
```swift
let putObjectACl = QCloudPutObjectACLRequest.init();

// Bucket name in the format of BucketName-APPID
putObjectACl.bucket = "examplebucket-1250000000";

// Object key, which is the full path of a COS object. If the object is in a directory, the format should be like "dir1/object1"
putObjectACl.object = "exampleobject";
let grantString = "id=\"100000000001\"";

// grantFullControl grants both read and write permissions
putObjectACl.grantFullControl = grantString;
// Grant read permissions to the grantee
putObjectACl.grantRead = grantString;
// Grants write permissions to the grantee
putObjectACl.grantWrite = grantString;

putObjectACl.finishBlock = {(result,error)in
    if error != nil{
        print(error!)
    }else{
        // outputObject returns the etag or custom headers
        print(result!);
    }
}
QCloudCOSXMLService.defaultCOSXML().putObjectACL(putObjectACl);
```

>?For more samples, go to [GitHub](https://github.com/tencentyun/qcloud-sdk-ios-samples/tree/master/COSAPIDemo/Swift/Examples/cases/ObjectACL.swift).

### Querying an object ACL

#### API description

This API (GET Object acl) is used to query the ACL of an object.

#### Sample code
**Objective-C**

[//]: # (.cssg-snippet-get-object-acl)
```objective-c
QCloudGetObjectACLRequest *request = [QCloudGetObjectACLRequest new];

// Object key, which is the full path of a COS object. If the object is in a directory, the format should be like "dir1/object1"
request.object = @"exampleobject";

// Bucket name in the format of BucketName-APPID
request.bucket = @"examplebucket-1250000000";

__block QCloudACLPolicy* policy;
[request setFinishBlock:^(QCloudACLPolicy * _Nonnull result,
                          NSError * _Nonnull error) {
    
    policy = result;
    // result.accessControlList; the grantee and permissions
    // result.owner; the object owner
}];

[[QCloudCOSXMLService defaultCOSXML] GetObjectACL:request];
```
>?For more samples, go to [GitHub](https://github.com/tencentyun/qcloud-sdk-ios-samples/tree/master/COSAPIDemo/Objc/Examples/cases/ObjectACL.m).



**Swift**

[//]: # (.cssg-snippet-get-object-acl)
```swift
let getObjectACL = QCloudGetObjectACLRequest.init();

// Bucket name in the format of BucketName-APPID
getObjectACL.bucket = "examplebucket-1250000000";

// Object key, which is the full path of a COS object. If the object is in a directory, the format should be like "dir1/object1"
getObjectACL.object = "exampleobject";
getObjectACL.setFinish { (result, error) in
    // result.accessControlList; the grantee and permissions
    // result.owner; the object owner
    if error != nil{
        print(error!)
    }else{
        // You can get the object ACL from the accessControlList field in the result
        print(result!.accessControlList);
    }
}
QCloudCOSXMLService.defaultCOSXML().getObjectACL(getObjectACL);
```
>?For more samples, go to [GitHub](https://github.com/tencentyun/qcloud-sdk-ios-samples/tree/master/COSAPIDemo/Swift/Examples/cases/ObjectACL.swift).



