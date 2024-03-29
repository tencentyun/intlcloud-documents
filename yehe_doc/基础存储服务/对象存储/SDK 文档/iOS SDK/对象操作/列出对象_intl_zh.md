## 简介

本文档提供关于列出对象操作相关的 API 概览以及 SDK 示例代码。

| API                                                          | 操作名         | 操作描述                                  |
| ------------------------------------------------------------ | -------------- | ----------------------------------------- |
| [GET Bucket（List Objects）](https://intl.cloud.tencent.com/document/product/436/30614) | 查询对象列表   | 查询存储桶下的部分或者全部对象     |
| [GET Bucket Object Versions](https://intl.cloud.tencent.com/document/product/436/31551) | 查询对象及其历史版本列表 |   查询存储桶下的部分或者全部对象及其历史版本信息|

## SDK API 参考

SDK 所有接口的具体参数与方法说明，请参考 [SDK API](https://cos-ios-sdk-doc-1253960454.file.myqcloud.com/)。

## 查询对象列表

#### 功能说明

查询存储桶下的部分或者全部对象。

#### 示例代码一: 获取第一页数据
**Objective-C**

[//]: # (.cssg-snippet-get-bucket)
```objective-c
QCloudGetBucketRequest* request = [QCloudGetBucketRequest new];

// 存储桶名称，由BucketName-Appid 组成，可以在COS控制台查看 https://console.cloud.tencent.com/cos5/bucket
request.bucket = @"examplebucket-1250000000";

// 单次返回的最大条目数量，默认1000
request.maxKeys = 100;

// 前缀匹配，用来规定返回的文件前缀地址
request.prefix = @"dir1/";

[request setFinishBlock:^(QCloudListBucketResult * result, NSError* error) {
    // result 返回具体信息
    // QCloudListBucketResult.contents 桶内文件数组
    // QCloudListBucketResult.commonPrefixes 桶内文件夹数组
    if (result.isTruncated) {
        // 表示数据被截断，需要拉取下一页数据
        self->prevPageResult = result;
    }
}];

[[QCloudCOSXMLService defaultCOSXML] GetBucket:request];
```

>?更多完整示例，请前往 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Objc/Examples/cases/ListObjects.m) 查看。

**Swift**

[//]: # (.cssg-snippet-get-bucket)
```swift
let getBucketReq = QCloudGetBucketRequest.init();

// 存储桶名称，由BucketName-Appid 组成，可以在COS控制台查看 https://console.cloud.tencent.com/cos5/bucket
getBucketReq.bucket = "examplebucket-1250000000";

// 单次返回的最大条目数量，默认1000
getBucketReq.maxKeys = 100;

// 前缀匹配
getBucketReq.prefix = "dir/";

getBucketReq.setFinish { (result, error) in
    if let result = result {
        // 文件列表
        let contents = result.contents
        
        if (result.isTruncated) {
            // 数据被截断，需要请求下一页数据
            self.prevPageResult = result;
        }
    } else {
        print(error!);
    }
}
QCloudCOSXMLService.defaultCOSXML().getBucket(getBucketReq);
```

>?更多完整示例，请前往 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Swift/Examples/cases/ListObjects.swift) 查看。

#### 示例代码二：请求下一页数据
**Objective-C**

[//]: # (.cssg-snippet-get-bucket-next-page)
```objective-c
QCloudGetBucketRequest* request = [QCloudGetBucketRequest new];

// 存储桶名称，由BucketName-Appid 组成，可以在COS控制台查看 https://console.cloud.tencent.com/cos5/bucket
request.bucket = @"examplebucket-1250000000";

// prevPageResult 是上一页的返回结果
// 分页参数 默认以UTF-8二进制顺序列出条目，所有列出条目从marker开始
request.marker = prevPageResult.nextMarker;

// 单次返回的最大条目数量，默认1000
request.maxKeys = 100;

[request setFinishBlock:^(QCloudListBucketResult * result, NSError* error) {
    // result 返回具体信息
    // QCloudListBucketResult.contents 桶内文件数组
    // QCloudListBucketResult.commonPrefixes 桶内文件夹数组
    if (result.isTruncated) {
        // 表示数据被截断，需要拉取下一页数据
        self->prevPageResult = result;
    }
}];

[[QCloudCOSXMLService defaultCOSXML] GetBucket:request];
```

>?更多完整示例，请前往 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Objc/Examples/cases/ListObjects.m) 查看。

**Swift**

[//]: # (.cssg-snippet-get-bucket-next-page)
```swift
let getBucketReq = QCloudGetBucketRequest.init();

// 存储桶名称，由BucketName-Appid 组成，可以在COS控制台查看 https://console.cloud.tencent.com/cos5/bucket
getBucketReq.bucket = "examplebucket-1250000000";

// 分页参数 默认以UTF-8二进制顺序列出条目，所有列出条目从marker开始
if let result = self.prevPageResult {
    getBucketReq.marker = result.marker
}

// 单次返回的最大条目数量，默认1000
getBucketReq.maxKeys = 100;
// 前缀匹配
getBucketReq.prefix = "dir/";

getBucketReq.setFinish { (result, error) in
    if let result = result {
        // 文件列表
        let contents = result.contents
        
        if (result.isTruncated) {
            // 数据被截断，需要请求下一页数据
            self.prevPageResult = result;
        }
    } else {
        print(error!);
    }
}
QCloudCOSXMLService.defaultCOSXML().getBucket(getBucketReq);
```

>?更多完整示例，请前往 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Swift/Examples/cases/ListObjects.swift) 查看。

#### 示例代码三：获取对象列表与子目录
**Objective-C**

[//]: # (.cssg-snippet-get-bucket-with-delimiter)
```objective-c
QCloudGetBucketRequest* request = [QCloudGetBucketRequest new];

// 存储桶名称，由BucketName-Appid 组成，可以在COS控制台查看 https://console.cloud.tencent.com/cos5/bucket
request.bucket = @"examplebucket-1250000000";

// 单次返回的最大条目数量，默认1000
request.maxKeys = 100;

// 前缀匹配，用来规定返回的文件前缀地址
request.prefix = @"dir1/";

// 定界符为一个符号，如果有 Prefix，则将 Prefix 到 delimiter 之间的相同路径归为一类，
// 定义为 Common Prefix，然后列出所有 Common Prefix。如果没有 Prefix，则从路径起点开始
// delimiter:路径分隔符 固定为 /
request.delimiter = @"/";

// prevPageResult 是上一页的返回结果
// 分页参数 默认以UTF-8二进制顺序列出条目，所有列出条目从marker开始
request.marker = prevPageResult.nextMarker;

[request setFinishBlock:^(QCloudListBucketResult * result, NSError* error) {
    // result 返回具体信息
    // QCloudListBucketResult.contents 桶内文件数组
    // QCloudListBucketResult.commonPrefixes 桶内文件夹数组
    if (result.isTruncated) {
        // 表示数据被截断，需要拉取下一页数据
        self->prevPageResult = result;
    }
}];

[[QCloudCOSXMLService defaultCOSXML] GetBucket:request];
```

>?更多完整示例，请前往 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Objc/Examples/cases/ListObjects.m) 查看。

**Swift**

[//]: # (.cssg-snippet-get-bucket-with-delimiter)
```swift
let getBucketReq = QCloudGetBucketRequest.init();

// 存储桶名称，由BucketName-Appid 组成，可以在COS控制台查看 https://console.cloud.tencent.com/cos5/bucket
getBucketReq.bucket = "examplebucket-1250000000";

// 单次返回的最大条目数量，默认1000
getBucketReq.maxKeys = 100;

// 前缀匹配，用来规定返回的文件前缀地址
getBucketReq.prefix = "dir/";

// 定界符为一个符号，如果有 Prefix，则将 Prefix 到 delimiter 之间的相同路径归为一类，
// 定义为 Common Prefix，然后列出所有 Common Prefix。如果没有 Prefix，则从路径起点开始
// delimiter:路径分隔符 固定为 /
getBucketReq.delimiter = "/";

// 分页参数 默认以UTF-8二进制顺序列出条目，所有列出条目从marker开始
if let result = self.prevPageResult {
    getBucketReq.marker = result.marker
}

getBucketReq.setFinish { (result, error) in
    if let result = result {
        // 文件列表
        let contents = result.contents
        
        if (result.isTruncated) {
            // 数据被截断，需要请求下一页数据
            self.prevPageResult = result;
        }
    } else {
        print(error!);
    }
}
QCloudCOSXMLService.defaultCOSXML().getBucket(getBucketReq);
```

>?更多完整示例，请前往 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Swift/Examples/cases/ListObjects.swift) 查看。

## 查询对象历史版本列表

#### 功能说明

查询开启版本控制的存储桶下的部分或者全部对象。

#### 示例代码：获取对象历史版本列表第一页数据

[//]: # (.cssg-snippet-list-objects-versioning)
```objective-c
QCloudListObjectVersionsRequest* listObjectVersionsRequest = [[QCloudListObjectVersionsRequest alloc] init];

// 存储桶名称
listObjectVersionsRequest.bucket = @"bucketname";

// 一页请求数据条目数，默认 1000
listObjectVersionsRequest.maxKeys = 100;

//从当前key列出剩余的条目
listObjectVersionsRequest.keyMarker = prevPageResult.nextKeyMarker;
//从当前key的某个版本列出剩余的条目
listObjectVersionsRequest.versionIdMarker = prevPageResult.nextVersionIDMarkder;
[listObjectVersionsRequest setFinishBlock:^(QCloudListVersionsResult * _Nonnull result,
                                            NSError * _Nonnull error) {
    
    // 已删除的文件
    NSArray<QCloudDeleteMarker*> *deleteMarker = result.deleteMarker;
    
    // 对象版本条目
    NSArray<QCloudVersionContent*> *versionContent = result.versionContent;
    
    if (result.isTruncated) {
        // 表示数据被截断，需要拉取下一页数据
        self->prevPageResult = result;
    }

    
}];

[[QCloudCOSXMLService defaultCOSXML] ListObjectVersions:listObjectVersionsRequest];
```

>?更多完整示例，请前往 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Objc/Examples/cases/ListObjectsVersioning.m) 查看。

