## 简介

本文档提供关于对象标签的 API 概览以及 SDK 示例代码。

| API                                                          | 操作名       | 操作描述                     |
| :----------------------------------------------------------- | :----------- | :--------------------------- |
| [PUT Object tagging](https://intl.cloud.tencent.com/document/product/436/35709) | 设置对象标签 | 为已上传的对象设置标签       |
| [GET Object tagging](https://intl.cloud.tencent.com/document/product/436/35710) | 查询对象标签 | 查询指定对象下已有的对象标签 |
| [DELETE Object tagging](https://intl.cloud.tencent.com/document/product/436/35711) | 删除对象标签 | 删除指定对象下已有的对象标签 |


## SDK API 参考

SDK 所有接口的具体参数与方法说明，请参考 [SDK API](https://cos-ios-sdk-doc-1253960454.file.myqcloud.com/)。

## 设置对象标签
#### 功能说明

COS 支持为已存在的对象设置标签。通过为对象添加键值对作为对象标签，可以协助您分组管理已有的对象资源。

#### 示例代码

**Objective-C**
```objective-c

    QCloudPutObjectTaggingRequest *putReq = [QCloudPutObjectTaggingRequest new];

    // 存储桶名称，由BucketName-Appid 组成，可以在COS控制台查看 https://console.cloud.tencent.com/cos5/bucket
    putReq.bucket = @"examplebucket-1250000000";

    // 标签集合
    QCloudTagging *taggings = [QCloudTagging new];

    QCloudTag *tag1 = [QCloudTag new];

    // 标签的 Key，长度不超过128字节, 支持英文字母、数字、空格、加号、减号、下划线、等号、点号、
    // 冒号、斜线
    tag1.key = @"age";

    // 标签的 Value，长度不超过256字节, 支持英文字母、数字、空格、加号、减号、下划线、等号、点号
    // 、冒号、斜线
    tag1.value = @"20";
    QCloudTag *tag2 = [QCloudTag new];
    tag2.key = @"name";
    tag2.value = @"karis";

    // 标签集合，最多支持10个标签
    QCloudTagSet *tagSet = [QCloudTagSet new];
    tagSet.tag = @[tag1,tag2];
    taggings.tagSet = tagSet;

    // 标签集合
    putReq.taggings = taggings;

    [putReq setFinishBlock:^(id outputObject, NSError *error) {
        // outputObject 包含所有的响应 http 头部
        NSDictionary* info = (NSDictionary *) outputObject;
    }];
    [[QCloudCOSXMLService defaultCOSXML] PutObjectTagging:putReq];
```

**Swift**
```swift
    let putReq = QCloudPutObjectTaggingRequest()

    // 存储桶名称，由BucketName-Appid 组成，可以在COS控制台查看 https://console.cloud.tencent.com/cos5/bucket
    putReq.bucket = "examplebucket-1250000000";

    // 标签集合
    let taggings = QCloudTagging();

    let tag1 = QCloudTag();

    // 标签的 Key，长度不超过128字节, 支持英文字母、数字、空格、加号、减号、下划线、等号、点号、
    // 冒号、斜线
    tag1.key = "age";

    // 标签的 Value，长度不超过256字节, 支持英文字母、数字、空格、加号、减号、下划线、等号、点号
    // 、冒号、斜线
    tag1.value = "20";
    let tag2 = QCloudTag();
    tag2.key = "name";
    tag2.value = "karis";

    // 标签集合，最多支持10个标签
    let tagSet = QCloudTagSet();
    tagSet.tag = [tag1,tag2];
    taggings.tagSet = tagSet;

    // 标签集合
    putReq.taggings = taggings;

    req.finishBlock = {(result,error) in
        if let result = result {
            // result 包含响应的 header 信息
        } else {
            print(error!);
        }
    }
    QCloudCOSXMLService.defaultCOSXML().putObjectTagging(putReq);
```

## 查询对象标签

#### 功能说明

查询指定对象下已有的对象标签。

#### 示例代码

**Objective-C**
```objective-c
    QCloudGetObjectTaggingRequest *getReq = [QCloudGetObjectTaggingRequest new];

    // 存储桶名称，由BucketName-Appid 组成，可以在COS控制台查看 https://console.cloud.tencent.com/cos5/bucket
    getReq.bucket = @"examplebucket-1250000000";

    [getReq setFinishBlock:^(QCloudTagging * result, NSError * error) {

        // tag的集合
        QCloudTagSet * tagSet = result.tagSet;
    }];
    [[QCloudCOSXMLService defaultCOSXML] GetObjectTagging:getReq];
```

**Swift**
```swift
    let getReq = QCloudGetObjectTaggingRequest();

    // 存储桶名称，由BucketName-Appid 组成，可以在COS控制台查看 https://console.cloud.tencent.com/cos5/bucket
    getReq.bucket = "examplebucket-1250000000";

    req.finishBlock = {(result,error) in
        if let result = result {
            // tag的集合
            let tagSet = result.tagSet;
        } else {
            print(error!);
        }
    }

    QCloudCOSXMLService.defaultCOSXML().getObjectTagging(getReq);
```

## 删除对象标签

>! COS iOS SDK 版本需要大于等于 v5.9.9。

#### 功能说明

删除指定对象下已有的对象标签。

#### 请求示例

**Objective-C**
```objective-c
    QCloudDeleteObjectTaggingRequest *request = [QCloudDeleteObjectTaggingRequest new];

    // 文件名
    request.object = @"test.png";
    // 存储桶名称，由BucketName-Appid 组成，可以在COS控制台查看 https://console.cloud.tencent.com/cos5/bucket
    request.bucket = @"examplebucket-1250000000";
    request.versionId = @"versionId";

    [request setFinishBlock:^(id * result, NSError * error) {

        if(!error){
            // 删除成功
        }else{
            // 删除失败
        }
    }];
    [[QCloudCOSXMLService defaultCOSXML] DeleteObjectTagging:request];
```

**Swift**
```swift
    let request = QCloudDeleteObjectTaggingRequest();

    // 文件名
    request.object = "test.png";

    // 存储桶名称，由BucketName-Appid 组成，可以在COS控制台查看 https://console.cloud.tencent.com/cos5/bucket
    request.bucket = "examplebucket-1250000000";

    request.versionId = "versionId";

    req.finishBlock = {(result,error) in
        if(!error){
            // 删除成功
        }else{
            // 删除失败
        }
    }

    QCloudCOSXMLService.defaultCOSXML().deleteObjectTagging(request); 
```
