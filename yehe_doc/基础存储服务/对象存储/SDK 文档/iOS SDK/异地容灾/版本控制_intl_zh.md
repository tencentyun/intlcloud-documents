## 简介

本文档提供关于版本控制的 API 概览以及 SDK 示例代码。

| API                                                          | 操作名       | 操作描述                 |
| ------------------------------------------------------------ | ------------ | ------------------------ |
| [PUT Bucket versioning](https://intl.cloud.tencent.com/document/product/436/19889) | 设置版本控制 | 设置存储桶的版本控制功能 |
| [GET Bucket versioning](https://intl.cloud.tencent.com/document/product/436/19888) | 查询版本控制 | 查询存储桶的版本控制信息 |

## SDK API 参考

SDK 所有接口的具体参数与方法说明，请参考 [SDK API](https://cos-ios-sdk-doc-1253960454.file.myqcloud.com/)。

## 设置版本控制

#### 功能说明

设置指定存储桶的版本控制功能。开启版本控制功能后，只能暂停，不能关闭。

#### 示例代码
**Objective-C**

[//]: # ".cssg-snippet-put-bucket-versioning"
```objective-c
// 开启版本控制
QCloudPutBucketVersioningRequest* request = [[QCloudPutBucketVersioningRequest alloc] init];

// 存储桶名称，由BucketName-Appid 组成，可以在COS控制台查看 https://console.cloud.tencent.com/cos5/bucket
request.bucket =@"examplebucket-1250000000";

// 说明版本控制的具体信息
QCloudBucketVersioningConfiguration* versioningConfiguration =
    [[QCloudBucketVersioningConfiguration alloc] init];

request.configuration = versioningConfiguration;

// 说明版本是否开启，枚举值：QCloudCOSBucketVersioningStatusEnabled、
// QCloudCOSBucketVersioningStatusSuspended
versioningConfiguration.status = QCloudCOSBucketVersioningStatusEnabled;

[request setFinishBlock:^(id outputObject, NSError* error) {
    // outputObject 包含所有的响应 http 头部
    NSDictionary* info = (NSDictionary *) outputObject;
}];
[[QCloudCOSXMLService defaultCOSXML] PutBucketVersioning:request];
```

>?更多完整示例，请前往 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Objc/Examples/cases/BucketVersioning.m) 查看。

**Swift**

[//]: # ".cssg-snippet-put-bucket-versioning"
```swift
// 开启版本控制
let putBucketVersioning = QCloudPutBucketVersioningRequest.init();

// 存储桶名称，由BucketName-Appid 组成，可以在COS控制台查看 https://console.cloud.tencent.com/cos5/bucket
putBucketVersioning.bucket = "examplebucket-1250000000";

// 说明版本控制的具体信息
let config = QCloudBucketVersioningConfiguration.init();

// 说明版本是否开启，枚举值：Suspended、Enabled
config.status = .enabled;

putBucketVersioning.configuration = config;

putBucketVersioning.finishBlock = {(result,error) in
    if let result = result {
        // result 包含响应的 header 信息
    } else {
        print(error!);
    }
}
QCloudCOSXMLService.defaultCOSXML().putBucketVersioning(putBucketVersioning);
```

>?更多完整示例，请前往 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Swift/Examples/cases/BucketVersioning.swift) 查看。

## 查询版本控制

#### 功能说明

查询指定存储桶的版本控制信息。

- 获取存储桶版本控制的状态，需要有该存储桶的读权限。
- 有三种版本控制状态：未启用版本控制、启用版本控制和暂停版本控制。

#### 示例代码
**Objective-C**

[//]: # ".cssg-snippet-get-bucket-versioning"
```objective-c
QCloudGetBucketVersioningRequest* request =
                            [[QCloudGetBucketVersioningRequest alloc] init];

// 存储桶名称，由BucketName-Appid 组成，可以在COS控制台查看 https://console.cloud.tencent.com/cos5/bucket
request.bucket = @"examplebucket-1250000000";

[request setFinishBlock:^(QCloudBucketVersioningConfiguration* result,
                          NSError* error) {
    // 获取多版本状态
    QCloudCOSBucketVersioningStatus * status = result.status;
}];

[[QCloudCOSXMLService defaultCOSXML] GetBucketVersioning:request];
```

>?更多完整示例，请前往 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Objc/Examples/cases/BucketVersioning.m) 查看。

**Swift**

[//]: # ".cssg-snippet-get-bucket-versioning"
```swift
let getBucketVersioning = QCloudGetBucketVersioningRequest.init();

// 存储桶名称，由BucketName-Appid 组成，可以在COS控制台查看 https://console.cloud.tencent.com/cos5/bucket
getBucketVersioning.bucket = "examplebucket-1250000000";

getBucketVersioning.setFinish { (config, error) in
    if let config = config {
        // 多版本状态
        let status = config.status
    } else {
        print(error!);
    }
       
}
QCloudCOSXMLService.defaultCOSXML().getBucketVersioning(getBucketVersioning);
```

>?更多完整示例，请前往 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Swift/Examples/cases/BucketVersioning.swift) 查看。

