## 简介

本文档提供关于存储桶、对象的访问控制列表（ACL）的相关 API 概览以及 SDK 示例代码。

**存储桶 ACL**

| API                                                          | 操作名         | 操作描述                                |
| ------------------------------------------------------------ | -------------- | --------------------------------------- |
| [PUT Bucket acl](https://intl.cloud.tencent.com/document/product/436/7737) | 设置存储桶 ACL | 设置指定存储桶的访问权限控制列表（ACL） |
| [GET Bucket acl](https://intl.cloud.tencent.com/document/product/436/7733) | 查询存储桶 ACL | 查询指定存储桶的访问权限控制列表（ACL） |

**对象 ACL**

| API                                                          | 操作名       | 操作描述                                      |
| ------------------------------------------------------------ | ------------ | --------------------------------------------- |
| [PUT Object acl](https://intl.cloud.tencent.com/document/product/436/7748) | 设置对象 ACL | 设置存储桶中某个对象的访问控制列表 |
| [GET Object acl](https://intl.cloud.tencent.com/document/product/436/7744) | 查询对象 ACL | 查询对象的访问控制列表                |

## SDK API 参考

SDK 所有接口的具体参数与方法说明，请参考 [SDK API](https://cos-ios-sdk-doc-1253960454.file.myqcloud.com/)。


## 存储桶 ACL

### 设置存储桶 ACL

#### 功能说明

设置指定存储桶的访问权限控制列表（ACL）。

#### 示例代码
**Objective-C**

[//]: # (.cssg-snippet-put-bucket-acl)
```objective-c
QCloudPutBucketACLRequest* putACL = [QCloudPutBucketACLRequest new];

// 授予权限的账号 ID
NSString* uin = @"100000000001";
NSString *ownerIdentifier = [NSString stringWithFormat:@"qcs::cam::uin/%@:uin/%@"
                             , uin,uin];
NSString *grantString = [NSString stringWithFormat:@"id=\"%@\"",ownerIdentifier];

// 赋予被授权者读写权限
putACL.grantFullControl = grantString;

// 赋予被授权者读权限
putACL.grantRead = grantString;

// 存储桶名称，由BucketName-Appid 组成，可以在COS控制台查看 https://console.cloud.tencent.com/cos5/bucket
putACL.bucket = @"examplebucket-1250000000";

[putACL setFinishBlock:^(id outputObject, NSError *error) {
    // 可以从 outputObject 中获取服务器返回的 header 信息
    NSDictionary * result = (NSDictionary *)outputObject;

}];
// 设置acl
[[QCloudCOSXMLService defaultCOSXML] PutBucketACL:putACL];
```

>?更多完整示例，请前往 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Objc/Examples/cases/BucketACL.m) 查看。

**Swift**

[//]: # (.cssg-snippet-put-bucket-acl)
```swift
let putBucketACLReq = QCloudPutBucketACLRequest.init();

// 存储桶名称，由BucketName-Appid 组成，可以在COS控制台查看 https://console.cloud.tencent.com/cos5/bucket
putBucketACLReq.bucket = "examplebucket-1250000000";

// 授予权限的账号 ID
let appTD = "100000000001";
let ownerIdentifier = "qcs::cam::uin/\(appTD):uin/\(appTD)";
let grantString = "id=\"\(ownerIdentifier)\"";
// 赋予被授权者写权限
putBucketACLReq.grantWrite = grantString;

// 赋予被授权者读权限
putBucketACLReq.grantRead = grantString;

// 赋予被授权者读写权限 grantFullControl == grantRead + grantWrite
putBucketACLReq.grantFullControl = grantString;

putBucketACLReq.finishBlock = {(result,error) in
    if let result = result {
        // 可以从 result 中获取服务器返回的 header 信息
    } else {
        print(error!)
    }
}
QCloudCOSXMLService.defaultCOSXML().putBucketACL(putBucketACLReq);
```

>?更多完整示例，请前往 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Swift/Examples/cases/BucketACL.swift) 查看。

### 查询存储桶 ACL

#### 功能说明

查询指定存储桶的访问权限控制列表（ACL）。

#### 示例代码
**Objective-C**

[//]: # (.cssg-snippet-get-bucket-acl)
```objective-c
QCloudGetBucketACLRequest* getBucketACl = [QCloudGetBucketACLRequest new];

// 存储桶名称，格式：BucketName-APPID
getBucketACl.bucket = @"examplebucket-1250000000";

[getBucketACl setFinishBlock:^(QCloudACLPolicy * _Nonnull result,
                                       NSError * _Nonnull error) {
    // 被授权者与权限的信息
    QCloudAccessControlList *acl = result.accessControlList;
}];

[[QCloudCOSXMLService defaultCOSXML] GetBucketACL:getBucketACl];
```

>?更多完整示例，请前往 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Objc/Examples/cases/BucketACL.m) 查看。

**Swift**

[//]: # (.cssg-snippet-get-bucket-acl)
```swift
let getBucketACLReq = QCloudGetBucketACLRequest.init();

// 存储桶名称，由BucketName-Appid 组成，可以在COS控制台查看 https://console.cloud.tencent.com/cos5/bucket
getBucketACLReq.bucket = "examplebucket-1250000000";

getBucketACLReq.setFinish { (result, error) in
    if let result = result {
        // ACL 授权信息
        let acl = result.accessControlList;
    } else {
        print(error!)
    }
}
QCloudCOSXMLService.defaultCOSXML().getBucketACL(getBucketACLReq)
```

>?更多完整示例，请前往 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Swift/Examples/cases/BucketACL.swift) 查看。

## 对象 ACL

### 设置对象 ACL

#### 功能说明

设置存储桶中某个对象的访问控制列表（ACL）。

#### 示例代码
**Objective-C**

[//]: # (.cssg-snippet-put-object-acl)
```objective-c
QCloudPutObjectACLRequest* request = [QCloudPutObjectACLRequest new];

// 对象键，是对象在 COS 上的完整路径，如果带目录的话，格式为 "video/xxx/movie.mp4"
request.object = @"exampleobject";

// 存储桶名称，由BucketName-Appid 组成，可以在COS控制台查看 https://console.cloud.tencent.com/cos5/bucket
request.bucket = @"examplebucket-1250000000";

NSString *grantString = [NSString stringWithFormat:@"id=\"%@\"",@"100000000001"];

// grantFullControl 等价于 grantRead + grantWrite
// 赋予被授权者读写权限。
request.grantFullControl = grantString;
// 赋予被授权者读权限。
request.grantRead = grantString;

[request setFinishBlock:^(id outputObject, NSError *error) {
    // 可以从 outputObject 中获取 response 中 etag 或者自定义头部等信息
    NSDictionary* info = (NSDictionary *) outputObject;
}];

[[QCloudCOSXMLService defaultCOSXML] PutObjectACL:request];
```

>?更多完整示例，请前往 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Objc/Examples/cases/ObjectACL.m) 查看。

**Swift**

[//]: # (.cssg-snippet-put-object-acl)
```swift
let putObjectACl = QCloudPutObjectACLRequest.init();

// 存储桶名称，由BucketName-Appid 组成，可以在COS控制台查看 https://console.cloud.tencent.com/cos5/bucket
putObjectACl.bucket = "examplebucket-1250000000";

// 对象键，是对象在 COS 上的完整路径，如果带目录的话，格式为 "video/xxx/movie.mp4"
putObjectACl.object = "exampleobject";
let grantString = "id=\"100000000001\"";

// grantFullControl 等价于 grantRead + grantWrite
putObjectACl.grantFullControl = grantString;
// 赋予被授权者读权限。
putObjectACl.grantRead = grantString;


putObjectACl.finishBlock = {(result,error)in
    if let result = result {
        // result 包含响应的 header 信息
    } else {
        print(error!);
    }
}
QCloudCOSXMLService.defaultCOSXML().putObjectACL(putObjectACl);
```

>?更多完整示例，请前往 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Swift/Examples/cases/ObjectACL.swift) 查看。

### 查询对象 ACL

#### 功能说明

查询对象的访问控制列表。

#### 示例代码
**Objective-C**

[//]: # (.cssg-snippet-get-object-acl)
```objective-c
QCloudGetObjectACLRequest *request = [QCloudGetObjectACLRequest new];

// 对象键，是对象在 COS 上的完整路径，如果带目录的话，格式为 "video/xxx/movie.mp4"
request.object = @"exampleobject";

// 存储桶名称，由BucketName-Appid 组成，可以在COS控制台查看 https://console.cloud.tencent.com/cos5/bucket
request.bucket = @"examplebucket-1250000000";

__block QCloudACLPolicy* policy;
[request setFinishBlock:^(QCloudACLPolicy * _Nonnull result,
                          NSError * _Nonnull error) {
    
    policy = result;
    // result.accessControlList; 被授权者与权限的信息
    // result.owner; 持有者的信息
}];

[[QCloudCOSXMLService defaultCOSXML] GetObjectACL:request];
```
>?更多完整示例，请前往 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Objc/Examples/cases/ObjectACL.m) 查看。



**Swift**

[//]: # (.cssg-snippet-get-object-acl)
```swift
let getObjectACL = QCloudGetObjectACLRequest.init();

// 存储桶名称，由BucketName-Appid 组成，可以在COS控制台查看 https://console.cloud.tencent.com/cos5/bucket
getObjectACL.bucket = "examplebucket-1250000000";

// 对象键，是对象在 COS 上的完整路径，如果带目录的话，格式为 "video/xxx/movie.mp4"
getObjectACL.object = "exampleobject";
getObjectACL.setFinish { (result, error) in
    if let result = result {
        // 对象授权信息
        let acl = result.accessControlList
    } else {
        print(error!);
    }
}
QCloudCOSXMLService.defaultCOSXML().getObjectACL(getObjectACL);
```
>?更多完整示例，请前往 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Swift/Examples/cases/ObjectACL.swift) 查看。



