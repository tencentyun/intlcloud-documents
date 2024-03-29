## 简介

本文档提供关于存储桶策略的 API 概览以及 SDK 示例代码。

| API                                                          | 操作名       | 操作描述                       |
| ------------------------------------------------------------ | ------------ | ------------------------------ |
| [PUT Bucket policy](https://intl.cloud.tencent.com/document/product/436/8282) | 设置存储桶策略 | 设置指定存储桶的权限策略     |
| [GET Bucket policy](https://intl.cloud.tencent.com/document/product/436/8276) | 查询存储桶策略 | 查询指定存储桶的权限策略 |
| [DELETE Bucket policy](https://intl.cloud.tencent.com/document/product/436/8285) | 删除存储桶策略 | 删除指定存储桶的权限策略 |

## SDK API 参考

SDK 所有接口的具体参数与方法说明，请参考 [SDK API 参考](https://cos-ios-sdk-doc-1253960454.file.myqcloud.com/)。

## 设置存储桶策略

#### 功能说明

设置指定存储桶的权限策略（PUT Bucket policy）。

>! COS iOS SDK 版本需要大于等于 v6.1.8。
>

#### 示例代码

[//]: # ".cssg-snippet-put-bucket-policy"
```java
QCloudPutBucketPolicyRequest * request = [QCloudPutBucketPolicyRequest new];
// 存储桶名称，由bucketname-appid 组成，appid必须填入，可以在COS控制台查看存储桶名称。 https://console.cloud.tencent.com/cos5/bucket
request.bucket = @"0-1250000000";
request.regionName = @"ap-chengdu";
// 权限策略，详情请参见 访问管理策略语法 https://www.tencentcloud.com/document/product/436/12469
request.policyInfo = @{
    @"Statement": @[
        @{
        @"Principal": @{
            @"qcs": @[
            @"qcs::cam::uin/100000000001:uin/100000000001"
            ]
        },
        @"Effect": @"allow",
        @"Action": @[
            @"name/cos:GetBucket"
        ],
        @"Resource": @[
            @"qcs::cos:ap-guangzhou:uid/1250000000:examplebucket-1250000000/*"
        ]
        }
    ],
    @"version": @"2.0"
    };
[request setFinishBlock:^(id  _Nullable outputObject, NSError * _Nullable error) {
    
}];
[[QCloudCOSXMLService defaultCOSXML] PutBucketPolicy:request];
```

>? 更多完整示例，请前往 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Objc/Examples/cases/BucketPolicyOperation.m) 查看。

## 查询存储桶策略

#### 功能说明

查询指定存储桶的权限策略（GET Bucket policy）。

>! COS Android SDK 版本需要大于等于 v6.1.8。
>

#### 示例代码

[//]: # ".cssg-snippet-get-bucket-policy"
```java

QCloudGetBucketPolicyRequest * request = [QCloudGetBucketPolicyRequest new];
// 存储桶名称，由bucketname-appid 组成，appid必须填入，可以在COS控制台查看存储桶名称。 https://console.cloud.tencent.com/cos5/bucket
request.bucket = @"bucketname-appid";
request.regionName = @"ap-chengdu";
[request setFinishBlock:^(QCloudBucketPolicyResult * _Nullable outputObject, NSError * _Nullable error) {
    // QCloudBucketPolicyResult 详细字段请查看api文档或者SDK源码
}];
[[QCloudCOSXMLService defaultCOSXML] GetBucketPolicy:request];
```

>? 更多完整示例，请前往 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Objc/Examples/cases/BucketPolicyOperation.m) 查看。

## 删除存储桶策略

#### 功能说明

删除指定存储桶的权限策略（DELETE Bucket policy）。

>! COS Android SDK 版本需要大于等于 v6.1.8。
>

#### 示例代码

[//]: # ".cssg-snippet-delete-bucket-policy"
```java
// 存储桶名称，由bucketname-appid 组成，appid必须填入，可以在COS控制台查看存储桶名称。 https://console.cloud.tencent.com/cos5/bucket
QCloudDeleteBucketPolicyRequest * request = [QCloudDeleteBucketPolicyRequest new];
request.bucket = @"0-1253960454";
request.regionName = @"ap-chengdu";
[request setFinishBlock:^(id  _Nullable outputObject, NSError * _Nullable error) {
    /// error 为空则表示成功
}];
[[QCloudCOSXMLService defaultCOSXML] DeleteBucketPolicy:request];
```

>? 更多完整示例，请前往 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Objc/Examples/cases/BucketPolicyOperation.m) 查看。


