## 简介

本文档提供关于静态网站的 API 概览以及 SDK 示例代码。

| API                                                          | 操作名           | 操作描述                 |
| ------------------------------------------------------------ | ---------------- | ------------------------ |
| [PUT Bucket website](https://intl.cloud.tencent.com/document/product/436/30617) | 设置静态网站     | 设置存储桶的静态网站配置 |
| [GET Bucket website](https://intl.cloud.tencent.com/document/product/436/30616) | 查询静态网站配置 | 查询存储桶的静态网站配置 |
| [DELETE Bucket website](https://intl.cloud.tencent.com/document/product/436/30629) | 删除静态网站配置 | 删除存储桶的静态网站配置 |

## SDK API 参考

SDK 所有接口的具体参数与方法说明，请参考 [SDK API](https://cos-ios-sdk-doc-1253960454.file.myqcloud.com/)。

## 设置静态网站

#### 功能说明

PUT Bucket website 用于为存储桶配置静态网站。

#### 示例代码
**Objective-C**

[//]: # (.cssg-snippet-put-bucket-website)
```objective-c
// 存储桶名称，由BucketName-Appid 组成，可以在COS控制台查看 https://console.cloud.tencent.com/cos5/bucket
NSString *bucket = @"examplebucket-1250000000";

NSString *indexDocumentSuffix = @"index.html";
NSString *errorDocKey = @"error.html";
NSString *derPro = @"https";
int errorCode = 451;
NSString * replaceKeyPrefixWith = @"404.html";
QCloudPutBucketWebsiteRequest *putReq = [QCloudPutBucketWebsiteRequest new];
putReq.bucket = bucket;

QCloudWebsiteConfiguration *config = [QCloudWebsiteConfiguration new];

QCloudWebsiteIndexDocument *indexDocument = [QCloudWebsiteIndexDocument new];

// 指定索引文档的对象键后缀。例如指定为index.html，那么当访问到存储桶的根目录时，会自动返回
// index.html 的内容，或者当访问到article/目录时，会自动返回 article/index.html的内容
indexDocument.suffix = indexDocumentSuffix;
// 索引文档配置
config.indexDocument = indexDocument;

// 错误文档配置
QCloudWebisteErrorDocument *errDocument = [QCloudWebisteErrorDocument new];
errDocument.key = errorDocKey;
// 指定通用错误文档的对象键，当发生错误且未命中重定向规则中的错误码重定向时，将返回该对象键的内容
config.errorDocument = errDocument;

// 重定向所有请求配置
QCloudWebsiteRedirectAllRequestsTo *redir = [QCloudWebsiteRedirectAllRequestsTo new];
redir.protocol  = derPro;
// 指定重定向所有请求的目标协议，只能设置为 https
config.redirectAllRequestsTo = redir;

// 单条重定向规则配置
QCloudWebsiteRoutingRule *rule = [QCloudWebsiteRoutingRule new];

// 重定向规则的条件配置
QCloudWebsiteCondition *contition = [QCloudWebsiteCondition new];
contition.httpErrorCodeReturnedEquals = errorCode;
rule.condition = contition;

// 重定向规则的具体重定向目标配置
QCloudWebsiteRedirect *webRe = [QCloudWebsiteRedirect new];
webRe.protocol = derPro;

// 指定重定向规则的具体重定向目标的对象键，替换方式为替换原始请求中所匹配到的前缀部分，
// 仅可在 Condition 为 KeyPrefixEquals 时设置
webRe.replaceKeyPrefixWith = replaceKeyPrefixWith;
rule.redirect = webRe;

QCloudWebsiteRoutingRules *routingRules = [QCloudWebsiteRoutingRules new];
routingRules.routingRule = @[rule];

// 重定向规则配置，最多设置100条 RoutingRule
config.rules = routingRules;
putReq.websiteConfiguration  = config;

[putReq setFinishBlock:^(id outputObject, NSError *error) {
    // outputObject 包含所有的响应 http 头部
    NSDictionary* info = (NSDictionary *) outputObject;
}];

[[QCloudCOSXMLService defaultCOSXML] PutBucketWebsite:putReq];
```

>?更多完整示例，请前往 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Objc/Examples/cases/BucketWebsite.m) 查看。

**Swift**

[//]: # (.cssg-snippet-put-bucket-website)
```swift
let req = QCloudPutBucketWebsiteRequest.init();

// 存储桶名称，由BucketName-Appid 组成，可以在COS控制台查看 https://console.cloud.tencent.com/cos5/bucket
req.bucket = "examplebucket-1250000000";

let indexDocumentSuffix = "index.html";
let errorDocKey = "error.html";
let errorCode = 451;
let replaceKeyPrefixWith = "404.html";

let config = QCloudWebsiteConfiguration.init();

let indexDocument = QCloudWebsiteIndexDocument.init();

// 指定索引文档的对象键后缀。例如指定为index.html，那么当访问到存储桶的根目录时，会自动返回
// index.html 的内容，或者当访问到article/目录时，会自动返回 article/index.html的内容
indexDocument.suffix = indexDocumentSuffix;

// 索引文档配置
config.indexDocument = indexDocument;

// 错误文档配置
let errDocument = QCloudWebisteErrorDocument.init();
errDocument.key = errorDocKey;

// 指定通用错误文档的对象键，当发生错误且未命中重定向规则中的错误码重定向时，将返回该对象键的内容
config.errorDocument = errDocument;

// 重定向所有请求配置
let redir = QCloudWebsiteRedirectAllRequestsTo.init();

// 指定重定向所有请求的目标协议，只能设置为 https
redir.protocol  = "https";
config.redirectAllRequestsTo = redir;

// 单条重定向规则配置
let rule = QCloudWebsiteRoutingRule.init();

// 重定向规则的条件配置
let contition = QCloudWebsiteCondition.init();
contition.httpErrorCodeReturnedEquals = Int32(errorCode);
rule.condition = contition;

// 重定向规则的具体重定向目标配置
let webRe = QCloudWebsiteRedirect.init();
webRe.protocol = "https";

// 指定重定向规则的具体重定向目标的对象键，替换方式为替换原始请求中所匹配到的前缀部分，
// 仅可在 Condition 为 KeyPrefixEquals 时设置
webRe.replaceKeyPrefixWith = replaceKeyPrefixWith;
rule.redirect = webRe;

let routingRules = QCloudWebsiteRoutingRules.init();
routingRules.routingRule = [rule];

// 重定向规则配置，最多设置100条 RoutingRule
config.rules = routingRules;
req.websiteConfiguration  = config;

req.finishBlock = {(result,error) in
    if let result = result {
        // result 包含响应的 header 信息
    } else {
        print(error!);
    }
}
QCloudCOSXMLService.defaultCOSXML().putBucketWebsite(req);
```

>?更多完整示例，请前往 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Swift/Examples/cases/BucketWebsite.swift) 查看。

## 查询静态网站配置

#### 功能说明

GET Bucket website 用于查询与存储桶关联的静态网站配置信息。

#### 示例代码
**Objective-C**

[//]: # (.cssg-snippet-get-bucket-website)
```objective-c
QCloudGetBucketWebsiteRequest *getReq = [QCloudGetBucketWebsiteRequest new];

// 存储桶名称，由BucketName-Appid 组成，可以在COS控制台查看 https://console.cloud.tencent.com/cos5/bucket
getReq.bucket = @"examplebucket-1250000000";
[getReq setFinishBlock:^(QCloudWebsiteConfiguration *  result,
                         NSError * error) {
    
    // 设置重定向规则，最多设置100条RoutingRule
    QCloudWebsiteRoutingRules *rules =result.rules;
    
    // 索引文档
    QCloudWebsiteIndexDocument *indexDocument = result.indexDocument;
    
    // 错误文档
    QCloudWebisteErrorDocument *errorDocument = result.errorDocument;
   
    // 重定向所有请求
    QCloudWebsiteRedirectAllRequestsTo *redirectAllRequestsTo = result.redirectAllRequestsTo;
    
}];
[[QCloudCOSXMLService defaultCOSXML] GetBucketWebsite:getReq];
```

>?更多完整示例，请前往 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Objc/Examples/cases/BucketWebsite.m) 查看。

**Swift**

[//]: # (.cssg-snippet-get-bucket-website)
```swift
let req = QCloudGetBucketWebsiteRequest.init();

// 存储桶名称，由BucketName-Appid 组成，可以在COS控制台查看 https://console.cloud.tencent.com/cos5/bucket
req.bucket = "examplebucket-1250000000";

req.setFinish {(result,error) in
    if let result = result {
        let rules = result.rules
    } else {
        print(error!);
    }
}
QCloudCOSXMLService.defaultCOSXML().getBucketWebsite(req);
```

>?更多完整示例，请前往 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Swift/Examples/cases/BucketWebsite.swift) 查看。

## 删除静态网站配置

#### 功能说明

DELETE Bucket website 用于删除存储桶中的静态网站配置。

#### 示例代码
**Objective-C**

[//]: # (.cssg-snippet-delete-bucket-website)
```objective-c
QCloudDeleteBucketWebsiteRequest *delReq = [QCloudDeleteBucketWebsiteRequest new];

// 存储桶名称，由BucketName-Appid 组成，可以在COS控制台查看 https://console.cloud.tencent.com/cos5/bucket
delReq.bucket = @"examplebucket-1250000000";

[delReq setFinishBlock:^(id outputObject, NSError *error) {
    // outputObject 包含所有的响应 http 头部
    NSDictionary* info = (NSDictionary *) outputObject;
}];
[[QCloudCOSXMLService defaultCOSXML] DeleteBucketWebsite:delReq];
```

>?更多完整示例，请前往 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Objc/Examples/cases/BucketWebsite.m) 查看。

**Swift**

[//]: # (.cssg-snippet-delete-bucket-website)
```swift
let delReq = QCloudDeleteBucketWebsiteRequest.init();

// 存储桶名称，由BucketName-Appid 组成，可以在COS控制台查看 https://console.cloud.tencent.com/cos5/bucket
delReq.bucket = "examplebucket-1250000000";

delReq.finishBlock = {(result,error) in
    if let result = result {
        // result 包含响应的 header 信息
    } else {
        print(error!);
    }
}

QCloudCOSXMLService.defaultCOSXML().deleteBucketWebsite(delReq);
```

>?更多完整示例，请前往 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Swift/Examples/cases/BucketWebsite.swift) 查看。

