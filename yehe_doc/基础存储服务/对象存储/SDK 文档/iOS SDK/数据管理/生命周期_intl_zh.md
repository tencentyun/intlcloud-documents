## 简介
本文档提供关于生命周期的 API 概览以及 SDK 示例代码。

| API                                                          | 操作名       | 操作描述                       |
| ------------------------------------------------------------ | ------------ | ------------------------------ |
| [PUT Bucket lifecycle](https://intl.cloud.tencent.com/document/product/436/8280) | 设置生命周期 | 设置存储桶的生命周期管理的配置 |
| [GET Bucket lifecycle](https://intl.cloud.tencent.com/document/product/436/8278) | 查询生命周期 | 查询存储桶生命周期管理的配置   |
| [DELETE Bucket lifecycle](https://intl.cloud.tencent.com/document/product/436/8284) | 删除生命周期 | 删除存储桶生命周期管理的配置   |

## SDK API 参考

SDK 所有接口的具体参数与方法说明，请参考 [SDK API](https://cos-ios-sdk-doc-1253960454.file.myqcloud.com/)。

## 设置生命周期

#### 功能说明

设置指定存储桶的生命周期配置信息。

#### 示例代码
**Objective-C**

[//]: # (.cssg-snippet-put-bucket-lifecycle)
```objective-c
QCloudPutBucketLifecycleRequest* request = [QCloudPutBucketLifecycleRequest new];

// 存储桶名称，由BucketName-Appid 组成，可以在COS控制台查看 https://console.cloud.tencent.com/cos5/bucket
request.bucket = @"examplebucket-1250000000";
__block QCloudLifecycleConfiguration* lifecycleConfiguration =
[[QCloudLifecycleConfiguration alloc] init];

// 规则描述
QCloudLifecycleRule* rule = [[QCloudLifecycleRule alloc] init];

// 用于唯一地标识规则
rule.identifier = @"identifier";

// 指明规则是否启用，枚举值：Enabled，Disabled
rule.status = QCloudLifecycleStatueEnabled;

// Filter 用于描述规则影响的 Object 集合
QCloudLifecycleRuleFilter* filter = [[QCloudLifecycleRuleFilter alloc] init];

// 指定规则所适用的前缀。匹配前缀的对象受该规则影响，Prefix 最多只能有一个
filter.prefix = @"prefix1";

// Filter 用于描述规则影响的 Object 集合
rule.filter = filter;

// 规则转换属性，对象何时转换为 Standard_IA 或 Archive
QCloudLifecycleTransition* transition = [[QCloudLifecycleTransition alloc] init];

// 指明规则对应的动作在对象最后的修改日期过后多少天操作：
transition.days = 100;

// 指定 Object 转储到的目标存储类型，枚举值： STANDARD_IA，ARCHIVE
transition.storageClass = QCloudCOSStorageStandardIA;
rule.transition = transition;
request.lifeCycle = lifecycleConfiguration;

// 生命周期配置
request.lifeCycle.rules = @[rule];
[request setFinishBlock:^(id outputObject, NSError* error) {
    // outputObject 包含所有的响应 http 头部
    NSDictionary* info = (NSDictionary *) outputObject;
}];

[[QCloudCOSXMLService defaultCOSXML] PutBucketLifecycle:request];
```

>?更多完整示例，请前往 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Objc/Examples/cases/BucketLifecycle.m) 查看。


**Swift**

[//]: # (.cssg-snippet-put-bucket-lifecycle)
```swift
let putBucketLifecycleReq = QCloudPutBucketLifecycleRequest.init();

// 存储桶名称，由BucketName-Appid 组成，可以在COS控制台查看 https://console.cloud.tencent.com/cos5/bucket
putBucketLifecycleReq.bucket = "examplebucket-1250000000";

let config = QCloudLifecycleConfiguration.init();

// 规则描述
let rule = QCloudLifecycleRule.init();

// 用于唯一地标识规则
rule.identifier = "swift";

// 指明规则是否启用，枚举值：Enabled，Disabled
rule.status = .enabled;

// Filter 用于描述规则影响的 Object 集合
let fileter = QCloudLifecycleRuleFilter.init();

// 指定规则所适用的前缀。匹配前缀的对象受该规则影响，Prefix 最多只能有一个
fileter.prefix = "0";

// Filter 用于描述规则影响的 Object 集合
rule.filter = fileter;

// 规则转换属性，对象何时转换为 Standard_IA 或 Archive
let transition = QCloudLifecycleTransition.init();

// 指明规则对应的动作在对象最后的修改日期过后多少天操作：
transition.days = 100;

// 指定 Object 转储到的目标存储类型，枚举值： STANDARD_IA，ARCHIVE
transition.storageClass = .standardIA;

rule.transition = transition;

putBucketLifecycleReq.lifeCycle = config;

// 生命周期配置
putBucketLifecycleReq.lifeCycle.rules = [rule];

putBucketLifecycleReq.finishBlock = {(result,error) in
    if let result = result {
        // result 包含响应的 header 信息
    } else {
        print(error!);
    }
}
QCloudCOSXMLService.defaultCOSXML().putBucketLifecycle(putBucketLifecycleReq);
```

>?更多完整示例，请前往 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Swift/Examples/cases/BucketLifecycle.swift) 查看。


## 查询生命周期

#### 功能说明

查询存储桶的生命周期管理配置。

#### 示例代码
**Objective-C**

[//]: # (.cssg-snippet-get-bucket-lifecycle)
```objective-c
QCloudGetBucketLifecycleRequest* request = [QCloudGetBucketLifecycleRequest new];

// 存储桶名称，由BucketName-Appid 组成，可以在COS控制台查看 https://console.cloud.tencent.com/cos5/bucket
request.bucket = @"examplebucket-1250000000";
[request setFinishBlock:^(QCloudLifecycleConfiguration* result,NSError* error) {
    // 可以从 result 中获取返回信息
    // result.rules 规则描述集合的数组
 
}];
[[QCloudCOSXMLService defaultCOSXML] GetBucketLifecycle:request];
```

>?更多完整示例，请前往 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Objc/Examples/cases/BucketLifecycle.m) 查看。

**Swift**

[//]: # (.cssg-snippet-get-bucket-lifecycle)
```swift
let getBucketLifeCycle = QCloudGetBucketLifecycleRequest.init();
getBucketLifeCycle.bucket = "examplebucket-1250000000";
getBucketLifeCycle.setFinish { (config, error) in
    if let config = config {
        // 生命周期规则
        let rules = config.rules
    } else {
        print(error!);
    }
 
};
QCloudCOSXMLService.defaultCOSXML().getBucketLifecycle(getBucketLifeCycle);
```

>?更多完整示例，请前往 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Swift/Examples/cases/BucketLifecycle.swift) 查看。

## 删除生命周期

#### 功能说明

删除存储桶生命周期管理的配置。

#### 示例代码
**Objective-C**

[//]: # (.cssg-snippet-delete-bucket-lifecycle)
```objective-c
QCloudDeleteBucketLifeCycleRequest* request =
[[QCloudDeleteBucketLifeCycleRequest alloc ] init];

// 存储桶名称，由BucketName-Appid 组成，可以在COS控制台查看 https://console.cloud.tencent.com/cos5/bucket
request.bucket = @"examplebucket-1250000000";

[request setFinishBlock:^(QCloudLifecycleConfiguration* deleteResult, NSError* error) {
    // 返回删除结果
}];
[[QCloudCOSXMLService defaultCOSXML] DeleteBucketLifeCycle:request];
```

>?更多完整示例，请前往 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Objc/Examples/cases/BucketLifecycle.m) 查看。

**Swift**

[//]: # (.cssg-snippet-delete-bucket-lifecycle)
```swift
let deleteBucketLifeCycle = QCloudDeleteBucketLifeCycleRequest.init();
deleteBucketLifeCycle.bucket = "examplebucket-1250000000";
deleteBucketLifeCycle.finishBlock = { (result, error) in
    if let result = result {
        // result 包含响应的 header 信息
    } else {
        print(error!);
    }
};
QCloudCOSXMLService.defaultCOSXML().deleteBucketLifeCycle(deleteBucketLifeCycle);
```

>?更多完整示例，请前往 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Swift/Examples/cases/BucketLifecycle.swift) 查看。

