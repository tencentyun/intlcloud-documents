## 简介

本文档提供关于清单的 API 概览以及 SDK 示例代码。

| API                                                          | 操作名       | 操作描述             |
| ------------------------------------------------------------ | ------------ | -------------------- |
| [PUT Bucket inventory](https://intl.cloud.tencent.com/document/product/436/30625) | 设置清单任务 | 设置存储桶的清单任务 |
| [GET Bucket inventory](https://intl.cloud.tencent.com/document/product/436/30623) | 查询清单任务 | 查询存储桶的清单任务 |
| [DELETE Bucket inventory](https://intl.cloud.tencent.com/document/product/436/30626) | 删除清单任务 | 删除存储桶的清单任务 |

## SDK API 参考

SDK 所有接口的具体参数与方法说明，请参考 [SDK API 参考](https://cos-ios-sdk-doc-1253960454.file.myqcloud.com/)。

## 设置清单任务

#### 功能说明

PUT Bucket inventory 用于在存储桶中创建清单任务。

#### 示例代码
**Objective-C**

[//]: # (.cssg-snippet-put-bucket-inventory)
```objective-c
QCloudPutBucketInventoryRequest *putReq = [QCloudPutBucketInventoryRequest new];

// 存储桶名称，由BucketName-Appid 组成，可以在COS控制台查看 https://console.cloud.tencent.com/cos5/bucket
putReq.bucket= @"examplebucket-1250000000";

// 清单任务的名称
putReq.inventoryID = @"list1";

// 用户在请求体中使用 XML 语言设置清单任务的具体配置信息。配置信息包括清单任务分析的对象，
// 分析的频次，分析的维度，分析结果的格式及存储的位置等信息。
QCloudInventoryConfiguration *config = [QCloudInventoryConfiguration new];

// 清单的名称，与请求参数中的 id 对应
config.identifier = @"list1";

// 清单是否启用的标识：
// 如果设置为 true，清单功能将生效
// 如果设置为 false，将不生成任何清单
config.isEnabled = @"True";

// 描述存放清单结果的信息
QCloudInventoryDestination *des = [QCloudInventoryDestination new];

QCloudInventoryBucketDestination *btDes =[QCloudInventoryBucketDestination new];

// 清单分析结果的文件形式，可选项为 CSV 格式
btDes.cs = @"CSV";

// 存储桶的所有者 ID
btDes.account = @"1278687956";

// 存储桶名称，由BucketName-Appid 组成，可以在COS控制台查看 https://console.cloud.tencent.com/cos5/bucket
btDes.bucket  = @"qcs::cos:ap-guangzhou::examplebucket-1250000000";

// 清单分析结果的前缀
btDes.prefix = @"list1";

// COS 托管密钥的加密方式
QCloudInventoryEncryption *enc = [QCloudInventoryEncryption new];
enc.ssecos = @"";

// 为清单结果提供服务端加密的选项
btDes.encryption = enc;

// 清单结果导出后存放的存储桶信息
des.bucketDestination = btDes;

// 描述存放清单结果的信息
config.destination = des;

// 配置清单任务周期
QCloudInventorySchedule *sc = [QCloudInventorySchedule new];

// 清单任务周期，可选项为按日或者按周，枚举值：Daily、Weekly
sc.frequency = @"Daily";
config.schedule = sc;
QCloudInventoryFilter *fileter = [QCloudInventoryFilter new];
fileter.prefix = @"myPrefix";
config.filter = fileter;
config.includedObjectVersions = QCloudCOSIncludedObjectVersionsAll;
QCloudInventoryOptionalFields *fields = [QCloudInventoryOptionalFields new];

fields.field = @[ @"Size",
                  @"LastModifiedDate",
                  @"ETag",
                  @"StorageClass",
                  @"IsMultipartUploaded",
                  @"ReplicationStatus"];

// 设置清单结果中应包含的分析项目
config.optionalFields = fields;
putReq.inventoryConfiguration = config;
[putReq setFinishBlock:^(id outputObject, NSError *error) {
    // 可以从 outputObject 中获取 response 中 etag 或者自定义头部等信息
    NSDictionary * result = (NSDictionary *)outputObject;

}];
[[QCloudCOSXMLService defaultCOSXML] PutBucketInventory:putReq];
```

>?更多完整示例，请前往 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Objc/Examples/cases/BucketInventory.m) 查看。


**Swift**

[//]: # (.cssg-snippet-put-bucket-inventory)
```swift
let putReq = QCloudPutBucketInventoryRequest.init();

// 存储桶名称，由BucketName-Appid 组成，可以在COS控制台查看 https://console.cloud.tencent.com/cos5/bucket
putReq.bucket = "examplebucket-1250000000";

// 清单任务的名称
putReq.inventoryID = "list1";

// 用户在请求体中使用 XML 语言设置清单任务的具体配置信息。配置信息包括清单任务分析的对象，
// 分析的频次，分析的维度，分析结果的格式及存储的位置等信息。
let config = QCloudInventoryConfiguration.init();

// 清单的名称，与请求参数中的 id 对应
config.identifier = "list1";

// 清单是否启用的标识：
// 如果设置为 true，清单功能将生效
// 如果设置为 false，将不生成任何清单
config.isEnabled = "True";

// 描述存放清单结果的信息
let des = QCloudInventoryDestination.init();
let btDes = QCloudInventoryBucketDestination.init();

// 清单分析结果的文件形式，可选项为 CSV 格式
btDes.cs = "CSV";

// 存储桶的所有者 ID
btDes.account = "1278687956";

// 清单分析结果的存储桶名
btDes.bucket  = "qcs::cos:ap-guangzhou::examplebucket-1250000000";

// 清单分析结果的前缀
btDes.prefix = "list1";

// COS 托管密钥的加密方式
let enc = QCloudInventoryEncryption.init();
enc.ssecos = "";

// 为清单结果提供服务端加密的选项
btDes.encryption = enc;

// 清单结果导出后存放的存储桶信息
des.bucketDestination = btDes;

// 描述存放清单结果的信息
config.destination = des;

// 配置清单任务周期
let sc = QCloudInventorySchedule.init();

// 清单任务周期，可选项为按日或者按周，枚举值：Daily、Weekly
sc.frequency = "Daily";
config.schedule = sc;
let fileter = QCloudInventoryFilter.init();
fileter.prefix = "myPrefix";
config.filter = fileter;
config.includedObjectVersions = .all;
let fields = QCloudInventoryOptionalFields.init();
fields.field = [ "Size",
                 "LastModifiedDate",
                 "ETag",
                 "StorageClass",
                 "IsMultipartUploaded",
                 "ReplicationStatus"];
// 设置清单结果中应包含的分析项目
config.optionalFields = fields;
putReq.inventoryConfiguration = config;

putReq.finishBlock = {(result,error) in
    if let result = result {
        // result 包含响应的 header 信息
    } else {
        print(error!);
    }
}

QCloudCOSXMLService.defaultCOSXML().putBucketInventory(putReq);
```

>?更多完整示例，请前往 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Swift/Examples/cases/BucketInventory.swift) 查看。


#### 错误码说明

该请求可能会发生的一些常见的特殊错误如下：

| 错误码                | 描述                                         | 状态码               |
| --------------------- | -------------------------------------------- | -------------------- |
| InvalidArgument       | 不合法的参数值                               | HTTP 400 Bad Request |
| TooManyConfigurations | 清单数量已经达到1000条的上限                 | HTTP 400 Bad Request |
| AccessDenied          | 未授权的访问。您可能不具备访问该存储桶的权限 | HTTP 403 Forbidden   |

## 查询清单任务

#### 功能说明

GET Bucket inventory 用于查询存储桶中用户的清单任务信息。

#### 示例代码
**Objective-C**

[//]: # (.cssg-snippet-get-bucket-inventory)
```objective-c
QCloudGetBucketInventoryRequest *getReq = [QCloudGetBucketInventoryRequest new];

// 存储桶名称，由BucketName-Appid 组成，可以在COS控制台查看 https://console.cloud.tencent.com/cos5/bucket
getReq.bucket = @"examplebucket-1250000000";

// 清单任务的名称
getReq.inventoryID = @"list1";
[getReq setFinishBlock:^(QCloudInventoryConfiguration * _Nonnull result,
                         NSError * _Nonnull error) {
    // result 包含清单的信息
}];
[[QCloudCOSXMLService defaultCOSXML] GetBucketInventory:getReq];
```

>?更多完整示例，请前往 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Objc/Examples/cases/BucketCORS.m) 查看。

**Swift**

[//]: # (.cssg-snippet-get-bucket-inventory)
```swift
let req = QCloudGetBucketInventoryRequest.init();

// 存储桶名称，由BucketName-Appid 组成，可以在COS控制台查看 https://console.cloud.tencent.com/cos5/bucket
req.bucket = "examplebucket-1250000000";
// 清单任务的名称
req.inventoryID = "list1";
req.setFinish {(result,error) in
    if let result = result {
        // 任务信息
        let enabled = result.isEnabled
    } else {
        print(error!);
    }
}
QCloudCOSXMLService.defaultCOSXML().getBucketInventory(req);
```

>?更多完整示例，请前往 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Swift/Examples/cases/BucketCORS.swift) 查看。

## 删除清单任务

#### 功能说明

DELETE Bucket inventory 用于删除存储桶中指定的清单任务。

#### 示例代码
**Objective-C**

[//]: # (.cssg-snippet-delete-bucket-inventory)
```objective-c
QCloudDeleteBucketInventoryRequest *delReq = [QCloudDeleteBucketInventoryRequest new];

// 存储桶名称，由BucketName-Appid 组成，可以在COS控制台查看 https://console.cloud.tencent.com/cos5/bucket
delReq.bucket = @"examplebucket-1250000000";

// 清单任务的名称
delReq.inventoryID = @"list1";
[delReq setFinishBlock:^(id outputObject, NSError *error) {
    // 可以从 outputObject 中获取 response 中 etag 或者自定义头部等信息
    NSDictionary * result = (NSDictionary *)outputObject;
    
}];
[[QCloudCOSXMLService defaultCOSXML] DeleteBucketInventory:delReq];
```

>?更多完整示例，请前往 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Objc/Examples/cases/BucketCORS.m) 查看。

**Swift**

[//]: # (.cssg-snippet-delete-bucket-inventory)
```swift
let delReq = QCloudDeleteBucketInventoryRequest.init();

// 存储桶名称，由BucketName-Appid 组成，可以在COS控制台查看 https://console.cloud.tencent.com/cos5/bucket
delReq.bucket = "examplebucket-1250000000";

// 清单任务的名称
delReq.inventoryID = "list1";
delReq.finishBlock = {(result,error) in
    if let result = result {
        // result 包含响应的 header 信息
    } else {
        print(error!);
    }
}

QCloudCOSXMLService.defaultCOSXML().deleteBucketInventory(delReq);
```

>?更多完整示例，请前往 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Swift/Examples/cases/BucketCORS.swift) 查看。

