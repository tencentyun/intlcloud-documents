## 简介

本文档提供关于对象的删除操作相关的 API 概览以及 SDK 示例代码。

| API                                                          | 操作名         | 操作描述                                  |
| ------------------------------------------------------------ | -------------- | ----------------------------------------- |
| [DELETE Object](https://intl.cloud.tencent.com/document/product/436/7743) | 删除单个对象   | 在存储桶中删除指定对象 |
| [DELETE Multiple Objects](https://intl.cloud.tencent.com/document/product/436/8289)	 | 删除多个对象	|在存储桶中批量删除对象  |

## SDK API 参考

SDK 所有接口的具体参数与方法说明，请参考 [SDK API](https://cos-ios-sdk-doc-1253960454.file.myqcloud.com/)。

## 删除对象

#### 功能说明

删除指定的对象（DELETE Object）。

#### 示例代码一：删除单个对象
**Objective-C**

[//]: # (.cssg-snippet-delete-object)
```objective-c
QCloudDeleteObjectRequest* deleteObjectRequest = [QCloudDeleteObjectRequest new];

// 存储桶名称，由BucketName-Appid 组成，可以在COS控制台查看 https://console.cloud.tencent.com/cos5/bucket
deleteObjectRequest.bucket = @"examplebucket-1250000000";


// 对象键，是对象在 COS 上的完整路径，如果带目录的话，格式为 "video/xxx/movie.mp4"
deleteObjectRequest.object = @"exampleobject";

[deleteObjectRequest setFinishBlock:^(id outputObject, NSError *error) {
    // outputObject 包含所有的响应 http 头部
    NSDictionary* info = (NSDictionary *) outputObject;
}];

[[QCloudCOSXMLService defaultCOSXML] DeleteObject:deleteObjectRequest];
```

>?更多完整示例，请前往 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Objc/Examples/cases/DeleteObject.m) 查看。

**Swift**

[//]: # (.cssg-snippet-delete-object)
```swift
let deleteObject = QCloudDeleteObjectRequest.init();

// 存储桶名称，由BucketName-Appid 组成，可以在COS控制台查看 https://console.cloud.tencent.com/cos5/bucket
deleteObject.bucket = "examplebucket-1250000000";


// 对象键，是对象在 COS 上的完整路径，如果带目录的话，格式为 "video/xxx/movie.mp4"
deleteObject.object = "exampleobject";

deleteObject.finishBlock = {(result,error)in
    if let result = result {
        // result 包含响应的 header 信息
    } else {
        print(error!);
    }
}
QCloudCOSXMLService.defaultCOSXML().deleteObject(deleteObject);
```

>?更多完整示例，请前往 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Swift/Examples/cases/DeleteObject.swift) 查看。


#### 示例代码二：删除目录
**Objective-C**

[//]: # (.cssg-snippet-delete-dir)
```objective-c
QCloudGetBucketRequest* request = [QCloudGetBucketRequest new];
// 存储桶名称，由BucketName-Appid 组成，可以在COS控制台查看 https://console.cloud.tencent.com/cos5/bucket
request.bucket = @"examplebucket-1250000000";
// 单次返回的最大条目数量，默认1000
request.maxKeys = 100;

//要删除的目录名称：带'/'
request.prefix = @"prefix";

[request setFinishBlock:^(QCloudListBucketResult * result, NSError* error) {
    if(!error){
        NSMutableArray *deleteInfosArr = [NSMutableArray array];
        for (QCloudBucketContents *content in result.contents) {
            QCloudDeleteMultipleObjectRequest *delteRequest = [QCloudDeleteMultipleObjectRequest new];
            delteRequest.bucket = request.bucket;

            QCloudDeleteObjectInfo *object = [QCloudDeleteObjectInfo new];
            object.key = content.key;
            [deleteInfosArr addObject:object];
        }
            
        QCloudDeleteInfo *deleteInfos = [QCloudDeleteInfo new];
        deleteInfos.objects = [deleteInfosArr copy];
          
        QCloudDeleteMultipleObjectRequest *delteRequest = [QCloudDeleteMultipleObjectRequest new];
        delteRequest.bucket = @"examplebucket-1250000000";
        delteRequest.deleteObjects = deleteInfos;
        [delteRequest setFinishBlock:^(QCloudDeleteResult *outputObject, NSError *error) {
            NSLog(@"outputObject = %@",outputObject);
        }];

        [[QCloudCOSXMLService defaultCOSXML] DeleteMultipleObject:delteRequest];
            
    }
}];

[[QCloudCOSXMLService defaultCOSXML] GetBucket:request];
```

>?更多完整示例，请前往 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Objc/Examples/cases/DeleteObject.m) 查看。

**Swift**

[//]: # (.cssg-snippet-delete-dir)
```swift
let getBucketReq = QCloudGetBucketRequest.init();
        
// 存储桶名称，由BucketName-Appid 组成，可以在COS控制台查看 https://console.cloud.tencent.com/cos5/bucket
getBucketReq.bucket = "examplebucket-1250000000";
        
// 单次返回的最大条目数量，默认1000
getBucketReq.maxKeys = 100;
        
//要删除的目录名称：带'/'
getBucketReq.prefix = "dir/";
        
getBucketReq.setFinish { (result, error) in
    if let result = result {
        let contents = result.contents;
        let infos = NSMutableArray.init();
        for content in contents {
            let info = QCloudDeleteObjectInfo.init();
            info.key = content.key;
            infos.add(info);
        }
        let mutipleDel = QCloudDeleteMultipleObjectRequest.init();
        // 要删除的文件集合
        let deleteInfos = QCloudDeleteInfo.init();
        // 存储桶名称，由BucketName-Appid 组成，可以在COS控制台查看 https://console.cloud.tencent.com/cos5/bucket
        mutipleDel.bucket = "examplebucket-1250000000";
                
        deleteInfos.objects = infos as! [QCloudDeleteObjectInfo];
                
        // 布尔值，这个值决定了是否启动 Quiet 模式：
        // true：启动 Quiet 模式
        // false：启动 Verbose 模式
        // 默认值为 False
        deleteInfos.quiet = false;
                
        // 封装了需要批量删除的多个对象的信息
        mutipleDel.deleteObjects = deleteInfos;
                
        mutipleDel.setFinish { (result, error) in
            if let result = result {
                let deleted = result.deletedObjects
                let failed = result.deletedFailedObjects
            } else {
                print(error!);
            }
        }
        QCloudCOSXMLService.defaultCOSXML().deleteMultipleObject(mutipleDel);
    } else {
        print(error!);
    }
}
QCloudCOSXMLService.defaultCOSXML().getBucket(getBucketReq);
```

>?更多完整示例，请前往 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Swift/Examples/cases/DeleteObject.swift) 查看。

## 删除多个对象

#### 功能说明

批量删除多个对象（DELETE Multiple Objects）。

#### 示例代码一：批量删除对象

**Objective-C**

[//]: # (.cssg-snippet-delete-multi-object)
```objective-c
QCloudDeleteMultipleObjectRequest* delteRequest = [QCloudDeleteMultipleObjectRequest new];
delteRequest.bucket = @"examplebucket-1250000000";

// 要删除的单个文件
QCloudDeleteObjectInfo* deletedObject0 = [QCloudDeleteObjectInfo new];

// 对象键，是对象在 COS 上的完整路径，如果带目录的话，格式为 "video/xxx/movie.mp4"
deletedObject0.key = @"exampleobject";

// 要删除的文件集合
QCloudDeleteInfo* deleteInfo = [QCloudDeleteInfo new];

// 布尔值，这个值决定了是否启动 Quiet 模式：
// true：启动 Quiet 模式
// false：启动 Verbose 模式
// 默认值为 False
deleteInfo.quiet = NO;

// 存放需要删除对象信息的数组
deleteInfo.objects = @[deletedObject0];

// 封装了需要批量删除的多个对象的信息
delteRequest.deleteObjects = deleteInfo;

[delteRequest setFinishBlock:^(QCloudDeleteResult* outputObject,
                               NSError *error) {
    // 可以从 outputObject 中获取 response 中 etag 或者自定义头部等信息
    
}];

[[QCloudCOSXMLService defaultCOSXML] DeleteMultipleObject:delteRequest];
```

>?更多完整示例，请前往 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Objc/Examples/cases/DeleteObject.m) 查看。

**Swift**

[//]: # (.cssg-snippet-delete-multi-object)
```swift
let mutipleDel = QCloudDeleteMultipleObjectRequest.init();

// 存储桶名称，由BucketName-Appid 组成，可以在COS控制台查看 https://console.cloud.tencent.com/cos5/bucket
mutipleDel.bucket = "examplebucket-1250000000";

// 要删除的单个文件
let info1 = QCloudDeleteObjectInfo.init();

// 对象键，是对象在 COS 上的完整路径，如果带目录的话，格式为 "video/xxx/movie.mp4"
info1.key = "exampleobject";

let info2 = QCloudDeleteObjectInfo.init();

// 要删除的文件集合
let deleteInfos = QCloudDeleteInfo.init();

// 存放需要删除对象信息的数组
deleteInfos.objects = [info1,info2];

// 布尔值，这个值决定了是否启动 Quiet 模式：
// true：启动 Quiet 模式
// false：启动 Verbose 模式
// 默认值为 False
deleteInfos.quiet = false;

// 封装了需要批量删除的多个对象的信息
mutipleDel.deleteObjects = deleteInfos;

mutipleDel.setFinish { (result, error) in
    if let result = result {
        let deleted = result.deletedObjects
        let failed = result.deletedFailedObjects
    } else {
        print(error!);
    }
}
QCloudCOSXMLService.defaultCOSXML().deleteMultipleObject(mutipleDel);
```

>?更多完整示例，请前往 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Swift/Examples/cases/DeleteObject.swift) 查看。

#### 示例代码二：删除带指定前缀的对象
**Objective-C**

[//]: # (.cssg-snippet-delete-dir)
```objective-c
QCloudGetBucketRequest* request = [QCloudGetBucketRequest new];
// 存储桶名称，由BucketName-Appid 组成，可以在COS控制台查看 https://console.cloud.tencent.com/cos5/bucket
request.bucket = @"examplebucket-1250000000";
// 单次返回的最大条目数量，默认1000
request.maxKeys = 100;

//如果要删除指定前缀的文件:prefix为文件名前缀
request.prefix = @"prefix";

[request setFinishBlock:^(QCloudListBucketResult * result, NSError* error) {
    if(!error){
        NSMutableArray *deleteInfosArr = [NSMutableArray array];
        for (QCloudBucketContents *content in result.contents) {
            QCloudDeleteMultipleObjectRequest *delteRequest = [QCloudDeleteMultipleObjectRequest new];
            delteRequest.bucket = request.bucket;

            QCloudDeleteObjectInfo *object = [QCloudDeleteObjectInfo new];
            object.key = content.key;
            [deleteInfosArr addObject:object];
        }
            
        QCloudDeleteInfo *deleteInfos = [QCloudDeleteInfo new];
        deleteInfos.objects = [deleteInfosArr copy];
          
        QCloudDeleteMultipleObjectRequest *delteRequest = [QCloudDeleteMultipleObjectRequest new];
        delteRequest.bucket = @"examplebucket-1250000000";
        delteRequest.deleteObjects = deleteInfos;
        [delteRequest setFinishBlock:^(QCloudDeleteResult *outputObject, NSError *error) {
            NSLog(@"outputObject = %@",outputObject);
        }];

        [[QCloudCOSXMLService defaultCOSXML] DeleteMultipleObject:delteRequest];
            
    }
}];

[[QCloudCOSXMLService defaultCOSXML] GetBucket:request];
```

>?更多完整示例，请前往 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Objc/Examples/cases/DeleteObject.m) 查看。

**Swift**

[//]: # (.cssg-snippet-delete-dir)
```swift
let getBucketReq = QCloudGetBucketRequest.init();
        
// 存储桶名称，由BucketName-Appid 组成，可以在COS控制台查看 https://console.cloud.tencent.com/cos5/bucket
getBucketReq.bucket = "examplebucket-1250000000";
        
// 单次返回的最大条目数量，默认1000
getBucketReq.maxKeys = 100;
        
//如果要删除指定前缀的文件:prefix为文件名前缀
getBucketReq.prefix = "dir/";

        
getBucketReq.setFinish { (result, error) in
    if let result = result {
        let contents = result.contents;
        let infos = NSMutableArray.init();
        for content in contents {
            let info = QCloudDeleteObjectInfo.init();
            info.key = content.key;
            infos.add(info);
        }
        let mutipleDel = QCloudDeleteMultipleObjectRequest.init();
        // 要删除的文件集合
        let deleteInfos = QCloudDeleteInfo.init();
        // 存储桶名称，由BucketName-Appid 组成，可以在COS控制台查看 https://console.cloud.tencent.com/cos5/bucket
        mutipleDel.bucket = "examplebucket-1250000000";
                
        deleteInfos.objects = infos as! [QCloudDeleteObjectInfo];
                
        // 布尔值，这个值决定了是否启动 Quiet 模式：
        // true：启动 Quiet 模式
        // false：启动 Verbose 模式
        // 默认值为 False
        deleteInfos.quiet = false;
                
        // 封装了需要批量删除的多个对象的信息
        mutipleDel.deleteObjects = deleteInfos;
                
        mutipleDel.setFinish { (result, error) in
            if let result = result {
                let deleted = result.deletedObjects
                let failed = result.deletedFailedObjects
            } else {
                print(error!);
            }
        }
        QCloudCOSXMLService.defaultCOSXML().deleteMultipleObject(mutipleDel);
    } else {
        print(error!);
    }
}
QCloudCOSXMLService.defaultCOSXML().getBucket(getBucketReq);
```

>?更多完整示例，请前往 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Swift/Examples/cases/DeleteObject.swift) 查看。

