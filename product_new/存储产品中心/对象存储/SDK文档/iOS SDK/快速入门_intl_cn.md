## 下载与安装

### 相关资源

- 对象存储服务的 iOS SDK 地址：[XML iOS SDK](https://github.com/tencentyun/qcloud-sdk-ios.git)。   
- 若您需要下载打包好的 Framework 格式的 SDK，可以从 [realease](https://github.com/tencentyun/qcloud-sdk-ios/releases) 中选择需要的版本进行下载。
- 更多示例可参考 Demo：[ XML iOS  SDK Demo](https://github.com/tencentyun/qcloud-sdk-ios-samples.git)。
- COS XML 版本的更新日志请参考：[XML iOS  SDK  ChangeLog](https://github.com/tencentyun/qcloud-sdk-ios/blob/master/CHANGELOG.md)。

### 环境依赖

- SDK 支持 iOS 8.0及以上版本的系统。
- 手机必须要有网络（GPRS、3G、4G 或 Wi-Fi 网络等）。
- 从访问管理控制台中的 [API 密钥管理](https://console.cloud.tencent.com/capi) 页面获取 SecretId、SecretKey，以及在 [账号中心](https://console.cloud.tencent.com/developer) 中获取 APPID 信息。

>关于文章中出现的 SecretID、SecretKey、Bucket 等名称的含义和获取方式请参见 [COS 术语信息](https://intl.cloud.tencent.com/document/product/436/7751#.E6.9C.AF.E8.AF.AD.E4.BF.A1.E6.81.AF)。

### 安装 SDK

#### SDK 导入

您可以通过 cocoapods 或下载打包好的静态库的方式来集成 SDK。在这里我们推荐您使用 cocoapods 的方式来进行导入。

- **使用 Cocoapods 导入（推荐）**  
  在 Podfile 文件中使用：
```shell
pod 'QCloudCOSXML'
```

- **使用打包好的静态库导入（手动集成方式）**  
  将 **QCloudCOSXML.framework、QCloudCore.framework 和 libmtasdk.a** 拖入到工程中，如下图所示：
  ![](https://main.qcloudimg.com/raw/ce990d8871293daec0aa434f28b152e6.png)  
  并添加以下依赖库：
 - CoreTelephony
 - Foundation
 - SystemConfiguration
 - libc++.tbd

#### 工程配置

在 Build Settings 中设置 Other Linker Flags，加入以下参数：

```shell
-ObjC
-all_load
```

如下图所示：
![](https://main.qcloudimg.com/raw/125218fad3f4781cae8f992d9a152057.png)

>
>腾讯云对象存储 XML iOS 的 SDK 使用 HTTP 协议。为了确保在 iOS 系统上可以运行，您需要开启允许通过 HTTP 传输。
>   您可以通过以下两种方式开启允许通过 HTTP 传输：
> - **手动设置方式**
>   在工程 info.plist 文件中添加 App Transport Security Settings 类型，然后在 App Transport Security Settings 下添加 Allow Arbitrary Loads 类型 Boolean，值设为 YES。
> - **代码设置方式**
>   您可以在集成 SDK 的 App 的 info.plist 中需要添加如下代码：
> ```shell
> <key>NSAppTransportSecurity</key>
> <dict>
> <key>NSExceptionDomains</key>
> <dict>
> 	<key>myqcloud.com</key>
> 	<dict>
> 		<key>NSIncludesSubdomains</key>
> 		<true/>
> 		<key>NSTemporaryExceptionAllowsInsecureHTTPLoads</key>
> 		<true/>
> 	</dict>
> </dict>
> </dict>
> ```
> 
> SDK 中同时也引入了腾讯移动分析（mta）的功能，若是想关闭该功能，可以通过如下方式进行设置：
> - 导入头文件
> `#import <QCloudCore/MTAConfig.h>`
> - 在注册完默认的 cosxml 服务之后，添加如下代码：
>`[TACMTAConfig getInstance].statEnable = NO;`

## 开始使用

下面为您介绍如何使用 COS iOS SDK 完成一个基础操作，例如初始化客户端、创建存储桶、查询存储桶列表、上传对象、查询对象列表、下载对象和删除对象。更多细节可以参见 [XML iOS SDK Demo](https://github.com/tencentyun/qcloud-sdk-ios-samples)，具体接口如何使用请参照 Demo 中提供的单元测试文件。

### 前提条件
需先在 [腾讯云控制台](https://console.cloud.tencent.com/cos5) 上申请 COS 业务的 APPID。

<span id="step1"></span>
### 初始化

在使用 SDK 的功能之前，需要导入一些必要的头文件和进行一些初始化工作。
引入上传 SDK 的头文件：

```objective-c
QCloudCore.h,    
QCloudCOSXML/QCloudCOSXML.h
```

#### 方法原型

实例化 QCloudServiceConfiguration 对象：

```
QCloudServiceConfiguration* configuration = [QCloudServiceConfiguration new];
configuration.appID = @"APPID"//项目ID;
```

实例化 QCloudCOSXMLService 对象：

<pre>
+ (QCloudCOSXMLService*) registerDefaultCOSXMLWithConfiguration:(QCloudServiceConfiguration*)configuration;
</pre>

实例化 QCloudCOSTransferManagerService 对象：

<pre>
+ (QCloudCOSTransferMangerService*) registerDefaultCOSTransferMangerWithConfiguration:(QCloudServiceConfiguration*)configuration;
</pre>

##### QCloudServiceConfiguration 参数说明

| 参数名称 | 说明                     | 类型                   | 必填 |
| -------- | ------------------------ | ---------------------- | ---- |
| appID    | 项目 ID，即 APPID      | NSString *             | 否   |
| endpoint | 配置 endpoint 相关信息 | QCloudCOSXMLEndPoint * | 是   |

##### QCloudCOSXMLEndPoint 参数说明

| 参数名称    | 说明                                | 类型       | 必填 |
| ----------- | ----------------------------------- | ---------- | ---- |
| regionName  | 服务所属的地域                    | NSString * | 是   |
| serviceName | 域名，默认是：`myqcloud.com`          | NSString * | 否   |
| useHTTPS    | 是否使用 HTTPS 服务，默认是 NO    | BOOL       | 否   |
| suffix      | 支持自定义`http://bucketname.suffix`  | NSString   | 否   |

#### 初始化示例

下示例中用到的 APPID，SecretId，SecretKey 等可以从 [COS 控制台](https://console.cloud.tencent.com/cos5) 中获取。

>
> 1. QCloudServiceConfiguration 的 signatureProvider 对象需要实现 QCloudSignatureProvider 协议。
> 2. 使用 SDK 操作前，首先要实例化一个默认的云服务配置对象 QCloudServiceConfiguration，其次需要实例化 QCloudCOSXMLService 和 QCloudCOSTransferManagerService 对象。  
> 3. 如果 QCloudServiceConfiguration 发生改变，可以通过`registerCOSTransferMangerWithConfiguration:(QCloudServiceConfiguration*)configuration withKey:(NSString*)key`注册一个新的QCloudCOSTransferManagerService，但是默认的 QCloudCOSTransferManagerService 只能有一个。



[//]: # (.cssg-snippet-global-init)
```objective-c
//AppDelegate.m
//第一步：注册默认的 COS 服务
- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
    QCloudServiceConfiguration* configuration = [QCloudServiceConfiguration new];
    configuration.appID = @"1250000000";
    configuration.signatureProvider = self;
    QCloudCOSXMLEndPoint* endpoint = [[QCloudCOSXMLEndPoint alloc] init];
    endpoint.regionName = @"COS_REGION";//服务地域名称，可用的地域请参考注释
    configuration.endpoint = endpoint;
    [QCloudCOSXMLService registerDefaultCOSXMLWithConfiguration:configuration];
    [QCloudCOSTransferMangerService registerDefaultCOSTransferMangerWithConfiguration:configuration];
    return YES;
}

//第二步：实现 QCloudSignatureProvider 协议
//实现签名的过程，我们推荐在服务器端实现签名的过程，详情请参考接下来的 “生成签名” 这一章。
```

#### swift 示例

[//]: # (.cssg-snippet-swift-global-init)
```swift
//AppDelegate.m
//第一步：注册默认的 COS 服务

func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplication.LaunchOptionsKey: Any]?) -> Bool {
    let config = QCloudServiceConfiguration.init();
    config.signatureProvider = self;
    config.appID = "appId";
    let endpoint = QCloudCOSXMLEndPoint.init();
    endpoint.regionName = "region";
    endpoint.useHTTPS = true;
    config.endpoint = endpoint;
    QCloudCOSXMLService.registerDefaultCOSXML(with: config);
    QCloudCOSTransferMangerService.registerDefaultCOSTransferManger(with: config);
    return true;
}


//第二步：实现 QCloudSignatureProvider 协议
//实现签名的过程，我们推荐在服务器端实现签名的过程，详情请参考接下来的 “生成签名” 这一章。
```

### 创建存储桶

[//]: # (.cssg-snippet-put-bucket)
```objective-c
QCloudPutBucketRequest* request = [QCloudPutBucketRequest new];
request.bucket = @"examplebucket-1250000000"; //additional actions after finishing
[request setFinishBlock:^(id outputObject, NSError* error) {
    //可以从 outputObject 中获取服务器返回的 header 信息
}];
[[QCloudCOSXMLService defaultCOSXML] PutBucket:request];
```

#### swift 示例

[//]: # (.cssg-snippet-swift-put-bucket)
```swift
let putBucketReq = QCloudPutBucketRequest.init();
putBucketReq.bucket = "examplebucket-1250000000";
putBucketReq.finishBlock = {(result,error) in
    if error != nil {
        print(error!);
    } else {
        print(result!);
    }}
QCloudCOSXMLService.defaultCOSXML().putBucket(putBucketReq);
```

### 查询存储桶列表

[//]: # (.cssg-snippet-get-service)
```objective-c
QCloudGetServiceRequest* request = [[QCloudGetServiceRequest alloc] init];
[request setFinishBlock:^(QCloudListAllMyBucketsResult* result, NSError* error) {
    //从 result 中获取返回信息
}];
[[QCloudCOSXMLService defaultCOSXML] GetService:request];
```

#### swift 示例

[//]: # (.cssg-snippet-swift-get-service)
```swift
let getServiceReq = QCloudGetServiceRequest.init();
getServiceReq.setFinish{(result,error) in
    if result == nil {
        print(error!);
    } else {
        //从 result 中获取返回信息
        print(result!);
    }}
QCloudCOSXMLService.defaultCOSXML().getService(getServiceReq);
```

### 上传对象

假设您已经申请了自己业务 Bucket。事实上，SDK 所有的请求对应了相应的 Request 类，只要生成相应的请求，设置好相应的属性，然后将请求交给 QCloudCOSTransferMangerService 对象，就可以完成相应的动作。其中，request 的 body 部分传入需要上传的对象在本地的 URL（NSURL\* 类型）。    

上传对象的接口需要用到签名来进行身份认证，发出的请求会自动向初始化时指定的遵循 QCloudSignatureProvider 协议的对象去请求签名。签名如何生成可以参考以下的 [生成签名](#.E7.94.9F.E6.88.90.E7.AD.BE.E5.90.8D) 部分。

>URL 所对应的对象在上传过程中是不能进行变更的，否则会导致出错。

#### 示例

[//]: # (.cssg-snippet-transfer-upload-object)
```objective-c
QCloudCOSXMLUploadObjectRequest* put = [QCloudCOSXMLUploadObjectRequest new];
put.object = @"exampleobject";
put.bucket = @"examplebucket-1250000000";
put.body = [@"testFileContent" dataUsingEncoding:NSUTF8StringEncoding];
//设置一些上传的参数
put.initMultipleUploadFinishBlock = ^(QCloudInitiateMultipartUploadResult * multipleUploadInitResult,
    QCloudCOSXMLUploadObjectResumeData resumeData) {
    //在初始化分块上传完成以后会回调该 block，在这里可以获取 resumeData，
    //并且可以通过 resumeData 生成一个分块上传的请求
    QCloudCOSXMLUploadObjectRequest* request = [QCloudCOSXMLUploadObjectRequest
        requestWithRequestData:resumeData];
};
[put setSendProcessBlock:^(int64_t bytesSent, int64_t totalBytesSent,
    int64_t totalBytesExpectedToSend) {
    NSLog(@"upload %lld totalSend %lld aim %lld", bytesSent, totalBytesSent,
        totalBytesExpectedToSend);
}];
[put setFinishBlock:^(QCloudUploadObjectResult *result, NSError* error) {
    //可以从 result 获取结果
}];

[[QCloudCOSTransferMangerService defaultCOSTransferManager] UploadObject:put];

//•••在完成了初始化，并且上传没有完成前
NSError* error;
//这里是主动调用取消，并且产生 resumetData 的例子
QCloudCOSXMLUploadObjectResumeData resumeData = [put cancelByProductingResumeData:&error];
QCloudCOSXMLUploadObjectRequest* request = nil;
if (resumeData) {
    request = [QCloudCOSXMLUploadObjectRequest requestWithRequestData:resumeData];
}
//生成的用于恢复上传的请求可以直接上传
[[QCloudCOSTransferMangerService defaultCOSTransferManager] UploadObject:request];
```

#### swift 示例

[//]: # (.cssg-snippet-swift-transfer-upload-object)
```swift
let uploadRequest = QCloudCOSXMLUploadObjectRequest<AnyObject>.init();
let dataBody:NSData? = "wrwrwrwrwrw".data(using: .utf8) as NSData?;
uploadRequest.body = dataBody!;
uploadRequest.bucket = "examplebucket-1250000000";
uploadRequest.object = "exampleobject";
//设置上传参数
uploadRequest.initMultipleUploadFinishBlock = {(multipleUploadInitResult,resumeData) in
    //在初始化分块上传完成以后会回调该 block，在这里可以获取 resumeData，并且可以通过 resumeData 生成一个分块上传的请求
    let resumeUploadRequest = QCloudCOSXMLUploadObjectRequest<AnyObject>.init(request: resumeData as Data?);
}
uploadRequest.sendProcessBlock = {(bytesSent , totalBytesSent , totalBytesExpectedToSend) in
    
}
uploadRequest.setFinish { (result, error) in
    if error != nil{
        print(error!)
    }else{
        //从 result 中获取请求的结果
        print(result!);
    }}

QCloudCOSTransferMangerService.defaultCOSTransferManager().uploadObject(uploadRequest);

//•••在完成了初始化，并且上传没有完成前
var error:NSError?;
    //这里是主动调用取消，并且产生 resumetData 的例子
do {
    let resumedData = try uploadRequest.cancel(byProductingResumeData: &error);
        var resumeUploadRequest:QCloudCOSXMLUploadObjectRequest<AnyObject>;
             resumeUploadRequest = QCloudCOSXMLUploadObjectRequest<AnyObject>.init(request: resumedData as Data?);
             //生成的用于恢复上传的请求可以直接上传
    if resumeUploadRequest != nil {
        QCloudCOSTransferMangerService.defaultCOSTransferManager().uploadObject(resumeUploadRequest!);
    }
             
} catch  {
    print("resumeData 为空");
    return;
}
```

#### QCloudCOSXMLUploadObjectRequest 参数说明

| 参数名称                      | 说明                                                         | 类型                  | 必填 |
| ----------------------------- | ------------------------------------------------------------ | --------------------- | ---- |
| Object                        | 对象键（Key）是对象在存储桶中的唯一标识。例如，在对象的访问域名`examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/picture.jpg`中，对象键为`doc/picture.jpg`，详情请参见 [对象概述](https://intl.cloud.tencent.com/document/product/436/13324) | NSString *            | 是   |
| bucket                        | 存储桶名，可在 [COS 控制台](https://console.cloud.tencent.com/cos5/bucket) 查看，格式为 &lt;BucketName-APPID&gt; ，例如`examplebucket-1250000000` | NSString *            | 是   |
| body                          | 需要上传的文件的路径。填入NSURL * 类型变量                   | BodyType              | 是   |
| storageClass                  | 对象的存储级别                                               | QCloudCOSStorageClass | 是   |
| cacheControl                  | RFC 2616 中定义的缓存策略                                    | NSString *            | 否   |
| contentDisposition            | RFC 2616 中定义的文件名称                                    | NSString *            | 否   |
| expect                        | 当使用 expect=@"100-Continue" 时，在收到服务端确认后才会发送请求内容 | NSString *            | 否   |
| expires                       | RFC 2616 中定义的过期时间                                    | NSString *            | 否   |
| initMultipleUploadFinishBlock | 如果该 request 产生了分块上传的请求，那么在分块上传初始化完成后，会通过这个 block 来回调，可以在该回调 block 中获取分块完成后的 bucket，key，uploadID，以及用于后续上传失败后恢复上传的 ResumeData | block                 | 否   |
| accessControlList             | 定义 Object 的 ACL 属性。有效值：private，public-read；默认值：private | NSString *            | 否   |
| grantRead                     | 赋予被授权者读的权限，格式：id="[OwnerUin]"                  | NSString *            | 否   |
| grantWrite                    | 授予被授权者写的权限，格式同上                               | NSString *            | 否   |
| grantFullControl              | 授予被授权者读写权限，格式同上                               | NSString *            | 否   |

### 查询对象列表

[//]: # (.cssg-snippet-get-bucket)
```objective-c
QCloudGetBucketRequest* request = [QCloudGetBucketRequest new];
request.bucket = @"examplebucket-1250000000";
request.maxKeys = 1000;

[request setFinishBlock:^(QCloudListBucketResult * result, NSError* error) {
    // result 返回具体信息
}];

[[QCloudCOSXMLService defaultCOSXML] GetBucket:request];
```

#### swift 示例

[//]: # (.cssg-snippet-swift-get-bucket)
```swift
let getBucketReq = QCloudGetBucketRequest.init();
getBucketReq.bucket = "examplebucket-1250000000";
getBucketReq.maxKeys = 1000;
getBucketReq.setFinish { (result, error) in
    if error != nil{
        print(error!);
    }else{
        print( result!.commonPrefixes);
    }}
QCloudCOSXMLService.defaultCOSXML().getBucket(getBucketReq);
```

### 下载对象

[//]: # (.cssg-snippet-get-object)
```objective-c
QCloudGetObjectRequest* request = [QCloudGetObjectRequest new];
//设置下载的路径 URL，如果设置了，文件将会被下载到指定路径中
//如果未设置该参数，那么文件将会被下载至内存里，存放在在 finishBlock 的 outputObject 里
request.downloadingURL = [NSURL URLWithString:QCloudTempFilePathWithExtension(@"downding")];
request.object = @"exampleobject";
request.bucket = @"examplebucket-1250000000";

[request setFinishBlock:^(id outputObject, NSError *error) {
    //可以从 outputObject 中获取 response 中 etag 或者自定义头部等信息
}];
[request setDownProcessBlock:^(int64_t bytesDownload, int64_t totalBytesDownload,
    int64_t totalBytesExpectedToDownload) {
    //下载过程中的进度
}];

[[QCloudCOSXMLService defaultCOSXML] GetObject:request];
```

#### swift 示例

[//]: # (.cssg-snippet-swift-get-object)
```swift
let getObject = QCloudGetObjectRequest.init();
getObject.bucket = "examplebucket-1250000000";
getObject.object = "exampleobject";
getObject.downloadingURL = URL.init(string: NSTemporaryDirectory())!.appendingPathComponent(getObject.object);
getObject.finishBlock = {(result,error) in
    if error != nil{
        print(error!);
    }else{
        print(result!);
    }};
getObject.downProcessBlock = {(bytesDownload, totalBytesDownload,  totalBytesExpectedToDownload) in
    print("totalBytesDownload:\(totalBytesDownload) totalBytesExpectedToDownload:\(totalBytesExpectedToDownload)");
}
QCloudCOSXMLService.defaultCOSXML().getObject(getObject);
```

### 删除对象

[//]: # (.cssg-snippet-delete-object)
```objective-c
QCloudDeleteObjectRequest* deleteObjectRequest = [QCloudDeleteObjectRequest new];
deleteObjectRequest.bucket = @"examplebucket-1250000000";
deleteObjectRequest.object = @"exampleobject";

[deleteObjectRequest setFinishBlock:^(id outputObject, NSError *error) {
    //可以从 outputObject 中获取 response 中 etag 或者自定义头部等信息
}];

[[QCloudCOSXMLService defaultCOSXML] DeleteObject:deleteObjectRequest];
```

#### swift 示例

[//]: # (.cssg-snippet-swift-delete-object)
```swift
let deleteObject = QCloudDeleteObjectRequest.init();
deleteObject.bucket = "examplebucket-1250000000";
deleteObject.object = "exampleobject";
deleteObject.finishBlock = {(result,error)in
    if error != nil{
        print(error!);
    }else{
        print(result!);
    }}
QCloudCOSXMLService.defaultCOSXML().deleteObject(deleteObject);
```

## 生成签名

SDK 中的请求需要用到签名，以确认访问的用户的身份，也保障了访问的安全性。当签名不正确时，大部分 COS 的服务将无法访问并且返回403错误。在 SDK 中可以生成签名，每个请求会向 QCloudServiceConfiguration 对象中的signatureProvider 对象来请求生成签名。我们可以将负责生成签名的对象在一开始赋值给 signatureProvider，该生成签名的对象需要遵循 QCloudSignatureProvider 协议，并实现生成签名的方法：

```objective-c
- (void) signatureWithFields:(QCloudSignatureFields* )fileds    
					request:(QCloudBizHTTPRequest* )request    
					urlRequest:(NSURLRequest* )urlRequst    
					compelete:(QCloudHTTPAuthentationContinueBlock)continueBlock
```

### 接入 CAM 系统实现临时签名（推荐）

虽然在本地提供了永久的 SecretId 和 SecretKey 来生成签名的接口，但请注意，将永久的 SecretId 和 SecretKey 存储在本地是非常危险的行为，容易造成泄露引起不必要的损失。因此基于安全性的考虑，建议您在服务器端实现签名的过程。

>强烈建议返回服务器时间作为签名的开始时间，用来避免由于用户手机本地时间偏差过大导致的签名不正确。

推荐您在自己的签名服务器内接入腾讯云的 CAM（Cloud Access Manager，访问管理）来实现整个签名流程。

![](https://main.qcloudimg.com/raw/58b5fff8c6bcf92691adc7299a2bdbf6.png) 

至于如何搭建签名服务器接入 CAM 系统，您可以参考 [移动应用直传实践](https://intl.cloud.tencent.com/document/product/436/30618)。

签名服务器接入 CAM 系统后，当客户端向签名服务器端请求签名时，签名服务器端会向 CAM 系统请求临时证书，然后返回给客户端。
CAM 系统会根据您的永久 SecretId 和 SecretKey 来生成临时的 SecretId，SecretKey 和临时 Token 来生成签名，可以最大限度地提高安全性。终端收到这些临时密钥的信息后，通过它们构建一个 QCloudCredential 对象，然后通过这个 QCloudCredentail 对象生成 QCloudAuthentationCreator，最后通过使用 Creator 来生成包含签名信息的 QCloudSignature 对象。具体的操作可以参考以下示例：

[//]: # (.cssg-snippet-global-init-signature-sts)
```objective-c
- (void) signatureWithFields:(QCloudSignatureFields*)fileds
                     request:(QCloudBizHTTPRequest*)request
                  urlRequest:(NSMutableURLRequest*)urlRequst
                   compelete:(QCloudHTTPAuthentationContinueBlock)continueBlock
{
    /*向签名服务器请求临时的 Secret ID,Secret Key,Token*/
    QCloudCredential* credential = [QCloudCredential new];
    credential.secretID = @"COS_SECRETID";
    credential.secretKey = @"COS_SECRETKEY";
    credential.token = @"COS_TOKEN";
    /*强烈建议返回服务器时间作为签名的开始时间，用来避免由于用户手机本地时间偏差过大导致的签名不正确 */
    credential.startDate = [[[NSDateFormatter alloc] init] dateFromString:@"start-time"];
    credential.experationDate  = [[[NSDateFormatter alloc] init] dateFromString:@"expire-time"];
    QCloudAuthentationV5Creator* creator = [[QCloudAuthentationV5Creator alloc] initWithCredential:credential];
    QCloudSignature* signature =  [creator signatureForData:urlRequst];
    continueBlock(signature, nil);
}
```

#### swift 示例

[//]: # (.cssg-snippet-swift-global-init-signature-sts)
```swift

func signature(with fileds: QCloudSignatureFields!, request: QCloudBizHTTPRequest!, urlRequest urlRequst: NSMutableURLRequest!, compelete continueBlock: QCloudHTTPAuthentationContinueBlock!) {
    let cre = QCloudCredential.init();
    cre.secretID = "COS_SECRETID";
    cre.secretKey = "COS_SECRETKEY";
    cre.token = "COS_TOKEN";
    /*强烈建议返回服务器时间作为签名的开始时间，用来避免由于用户手机本地时间偏差过大导致的签名不正确 */
    cre.startDate = DateFormatter().date(from: "start-time");
    cre.experationDate = DateFormatter().date(from: "expire-time");
    let auth = QCloudAuthentationV5Creator.init(credential: cre);
    let signature = auth?.signature(forData: urlRequst)
    continueBlock(signature,nil);
}
```

### 在终端使用永久密钥生成签名（不推荐）

>我们不推荐您在终端使用永久密钥生成签名，该方式有泄密数据的风险。

示例代码如下：

[//]: # (.cssg-snippet-global-init-signature)
```objective-c
- (void) signatureWithFields:(QCloudSignatureFields*)fileds
                     request:(QCloudBizHTTPRequest*)request
                  urlRequest:(NSMutableURLRequest*)urlRequst
                   compelete:(QCloudHTTPAuthentationContinueBlock)continueBlock
{
    
    QCloudCredential* credential = [QCloudCredential new];
    credential.secretID = @"COS_SECRETID";
    credential.secretKey = @"COS_SECRETKEY";
    QCloudAuthentationV5Creator* creator = [[QCloudAuthentationV5Creator alloc] initWithCredential:credential];
    QCloudSignature* signature =  [creator signatureForData:urlRequst];
    continueBlock(signature, nil);
}
```

#### swift 示例

[//]: # (.cssg-snippet-swift-global-init-signature)
```swift

func signature(with fileds: QCloudSignatureFields!, request: QCloudBizHTTPRequest!, urlRequest urlRequst: NSMutableURLRequest!, compelete continueBlock: QCloudHTTPAuthentationContinueBlock!) {
    let cre = QCloudCredential.init();
    cre.secretID = "COS_SECRETID";
    cre.secretKey = "COS_SECRETKEY";
    let auth = QCloudAuthentationV5Creator.init(credential: cre);
    let signature = auth?.signature(forData: urlRequst)
    continueBlock(signature,nil);
}
```

### 使用脚手架工具管理异步签名

到这一步时，您已经可以生成签名正常使用 SDK 里面的接口了。但为了方便您实现临时签名，从服务器端获取 tempSecretKey 等临时签名需要的信息，我们提供了脚手架工具可供使用。您可以依照前面的代码来生成签名，也可以通过我们的脚手架工具 QCloudCredentailFenceQueue 来方便地获取临时签名。
QCloudCredentailFenceQueue 提供了栅栏机制，也就是说您使用 QCloudCredentailFenceQueue 获取签名的话，所有需要获取签名的请求会等待签名完成后再执行，免去了自己管理异步过程。   
使用 QCloudCredentailFenceQueue，我们需要先生成一个实例。

```objective-c
//AppDelegate.m
//AppDelegate需遵循QCloudCredentailFenceQueueDelegate协议
//
- (BOOL)application:(UIApplication * )application didFinishLaunchingWithOptions:(NSDictionary * )launchOptions {
    // init step
    self.credentialFenceQueue = [QCloudCredentailFenceQueue new];
    self.credentialFenceQueue.delegate = self;
    return YES;
}

```

然后调用 QCloudCredentailFenceQueue 的类需要遵循 QCloudCredentailFenceQueueDelegate 并实现协议内定义的方法：

```objective-c
- (void) fenceQueue:(QCloudCredentailFenceQueue * )queue requestCreatorWithContinue:(QCloudCredentailFenceQueueContinue)continueBlock
```

当通过 QCloudCredentailFenceQueue 去获取签名时，所有需要签名的 SDK 里的请求都会等待该协议定义的方法内拿到了签名所需的参数并生成有效的签名后执行。请看以下示例：

[//]: # (.cssg-snippet-global-init-fence-queue)
```objective-c
//AppDelegate.m

//这里定义一个成员变量 @property (nonatomic) QCloudCredentailFenceQueue* credentialFenceQueue;

- (void) fenceQueue:(QCloudCredentailFenceQueue * )queue requestCreatorWithContinue:(QCloudCredentailFenceQueueContinue)continueBlock
{
    QCloudCredential* credential = [QCloudCredential new];
    //在这里可以同步过程从服务器获取临时签名需要的 secretID，secretKey，expiretionDate 和 token 参数
    credential.secretID = @"COS_SECRETID";
    credential.secretKey = @"COS_SECRETKEY";
    /*强烈建议返回服务器时间作为签名的开始时间，用来避免由于用户手机本地时间偏差过大导致的签名不正确 */
    credential.startDate = [[[NSDateFormatter alloc] init] dateFromString:@"start-time"];
    credential.experationDate = [[[NSDateFormatter alloc] init] dateFromString:@"expire-time"];
    credential.token = @"COS_TOKEN";
    QCloudAuthentationV5Creator* creator = [[QCloudAuthentationV5Creator alloc]
        initWithCredential:credential];
    continueBlock(creator, nil);
}

- (void) signatureWithFields:(QCloudSignatureFields*)fileds
                     request:(QCloudBizHTTPRequest*)request
                  urlRequest:(NSMutableURLRequest*)urlRequst
                   compelete:(QCloudHTTPAuthentationContinueBlock)continueBlock
{
    [self.credentialFenceQueue performAction:^(QCloudAuthentationCreator *creator, NSError *error) {
        if (error) {
            continueBlock(nil, error);
        } else {
            QCloudSignature* signature =  [creator signatureForData:urlRequst];
            continueBlock(signature, nil);
        }
    }];
}
```

#### swift 示例

[//]: # (.cssg-snippet-swift-global-init-fence-queue)
```swift
//AppDelegate.m

// 这里定义一个成员变量 @property (nonatomic) QCloudCredentailFenceQueue* credentialFenceQueue;

func fenceQueue(_ queue: QCloudCredentailFenceQueue!, requestCreatorWithContinue continueBlock: QCloudCredentailFenceQueueContinue!) {
    let cre = QCloudCredential.init();
    //在这里可以同步过程从服务器获取临时签名需要的 secretID，secretKey，expiretionDate 和 token 参数
    cre.secretID = "COS_SECRETID";
    cre.secretKey = "COS_SECRETKEY";
    cre.token = "COS_TOKEN";
    /*强烈建议返回服务器时间作为签名的开始时间，用来避免由于用户手机本地时间偏差过大导致的签名不正确 */
    cre.startDate = DateFormatter().date(from: "start-time");
    cre.experationDate = DateFormatter().date(from: "expire-time");
    let auth = QCloudAuthentationV5Creator.init(credential: cre);
    continueBlock(auth,nil);
}

func signature(with fileds: QCloudSignatureFields!, request: QCloudBizHTTPRequest!, urlRequest urlRequst: NSMutableURLRequest!, compelete continueBlock: QCloudHTTPAuthentationContinueBlock!) {
    self.credentialFenceQueue?.performAction({ (creator, error) in
        if error != nil {
            continueBlock(nil,error!);
        }else{
            let signature = creator?.signature(forData: urlRequst);
            continueBlock(signature,nil);
        }
    })
}
```

至此，您就可以通过我们提供的脚手架工具来生成临时签名了，当然您也可以自己去实现具体的签名过程。

## 精简版 SDK 使用指南

对于部分仅仅使用到上传和下载功能，并且对 SDK 体积要求较高的用户，我们提供了只有上传和下载功能的精简版 SDK，集成进去后的包增量只有完整版的一半。  

精简版 SDK 是通过 Cocoapods 的 Subspec 功能实现的，因此目前只支持通过 Cocoapods 集成的方式集成精简版 SDK。需要使用精简版的 SDK 只需要在 Podfile 中加入。

```
pod 'QCloudCOSXML/Transfer'
```

>对于 Mobile Line 的用户而言，只有在**没有使用** TACStorage 的情况下可以使用精简版的 SDK。与此同时，[Cocoapods](https://github.com/CocoaPods/Specs) 的官方源需要在**所有源的前面**（建议放在 Podfile 的第一行）。其它用户可忽略此说明。

对于精简版的 SDK ，没有 QCloudCOSXML.h 头文件，取而代之的是初始化时需要导入以下的头文件：

```
#import <QCloudCOSXML/QCloudCOSXMLTransfer.h>
#import <QCloudCore/QCloudCore.h>
```

精简版 SDK 初始化的过程，上传和下载的接口与完整版 SDK 一致。
