## 简介


本文档提供关于基础图片处理的相关的 API 概览以及 SDK 示例代码。

<table>
   <tr>
      <th>服务</td>
      <th>功能</td>
      <th>说明</td>
   </tr>
   <tr>
      <td rowspan=11>基础图片处理服务</td>
      <td><a href="https://intl.cloud.tencent.com/document/product/436/36366">缩放</a></td>
      <td>等比缩放、设定目标宽高缩放等多种方式</td>
   </tr>
   <tr>
      <td><a href="https://intl.cloud.tencent.com/document/product/436/36367">裁剪</a></td>
      <td>普通裁剪、缩放裁剪、内切圆、人脸智能裁剪</td>
   </tr>
   <tr>
      <td><a href="https://intl.cloud.tencent.com/document/product/436/36368">旋转</a></td>
      <td>自适应旋转、普通旋转</td>
   </tr>
   <tr>
      <td><a href="https://intl.cloud.tencent.com/document/product/436/36369">格式转换</a></td>
      <td>格式转换、GIF 格式优化、渐进显示</td>
   </tr>
   <tr>
      <td><a href="https://intl.cloud.tencent.com/document/product/436/36370">质量变换</a></td>
      <td>针对 JPG 和 WEBP 图片进行质量变换</td>
   </tr>
   <tr>
      <td><a href="https://intl.cloud.tencent.com/document/product/436/36371">高斯模糊</a></td>
      <td>对图片进行模糊处理</td>
   </tr>
   <tr>
      <td><a href="https://intl.cloud.tencent.com/document/product/436/36372">锐化</a></td>
      <td>对图片进行锐化处理</td>
   </tr>
   <tr>
      <td>添加水印</td>
      <td><a href="https://intl.cloud.tencent.com/document/product/436/36373">图片水印</a>、<a href="https://intl.cloud.tencent.com/document/product/436/36374">文字水印</a></td>
   </tr>
   <tr>
      <td>获取图片信息</td>
      <td><a href="https://intl.cloud.tencent.com/document/product/436/36375">基本信息</a>、<a href="https://intl.cloud.tencent.com/document/product/436/36376">EXIF 信息</a>、<a href="https://intl.cloud.tencent.com/document/product/436/36377">主色调</a></td>
   </tr>
   <tr>
      <td><a href="https://intl.cloud.tencent.com/document/product/436/36378">去除元信息</a></td>
      <td>包括 EXIF 信息</td>
   </tr>
   <tr>
      <td><a href="https://intl.cloud.tencent.com/document/product/436/36379">快速缩略模板</a></td>
      <td>快速实现图片格式转换、缩略、剪裁等功能，生成缩略图</td>
   </tr>
</table>


## SDK API 参考

SDK 所有接口的具体参数与方法说明，请参考 [SDK API](https://cos-ios-sdk-doc-1253960454.file.myqcloud.com/)。

## 上传时使用图片处理

下面示例展示了如何在上传图片时自动实现图片处理。

图片上传完成后，COS 会存储原始图片和已处理过的图片。后续用户可以通过普通的下载请求获取处理结果。

#### 示例代码
**Objective-C**

[//]: # (.cssg-snippet-upload-with-pic-operation)
```objective-c
QCloudPutObjectWatermarkRequest* put = [QCloudPutObjectWatermarkRequest new];

// 对象键，是对象在 COS 上的完整路径，如果带目录的话，格式为 "video/xxx/movie.mp4"
put.object = @"exampleobject";
// 存储桶名称，由BucketName-Appid 组成，可以在COS控制台查看 https://console.cloud.tencent.com/cos5/bucket
put.bucket = @"examplebucket-1250000000";

put.body =  [@"123456789" dataUsingEncoding:NSUTF8StringEncoding];
QCloudPicOperations * op = [[QCloudPicOperations alloc]init];

// 是否返回原图信息。0表示不返回原图信息，1表示返回原图信息，默认为0
op.is_pic_info = NO;
QCloudPicOperationRule * rule = [[QCloudPicOperationRule alloc]init];

// 处理结果的文件路径名称，如以/开头，则存入指定文件夹中，否则，存入原图文件存储的同目录
rule.fileid = @"test";

// 盲水印文字，需要经过 URL 安全的 Base64 编码。当 type 为3时必填，type
rule.text = @"123"; // 水印文字只能是 [a-zA-Z0-9]

// 盲水印类型，有效值：1 半盲；2 全盲；3 文字
rule.type = QCloudPicOperationRuleText;
op.rule = @[rule];
put.picOperations = op;
[put setFinishBlock:^(id outputObject, NSError *error) {
   
}];
[[QCloudCOSXMLService defaultCOSXML] PutWatermarkObject:put];
```

>?更多完整示例，请前往 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Objc/Examples/cases/PictureOperation.m) 查看。


**Swift**

[//]: # (.cssg-snippet-upload-with-pic-operation)
```swift
let put = QCloudPutObjectWatermarkRequest<AnyObject>();

// 对象键，是对象在 COS 上的完整路径，如果带目录的话，格式为 "video/xxx/movie.mp4"
put.object = "exampleobject";
// 存储桶名称，由BucketName-Appid 组成，可以在COS控制台查看 https://console.cloud.tencent.com/cos5/bucket

put.bucket = "examplebucket-1250000000";
put.body = "123456789".data(using: .utf8)! as NSData;
let op = QCloudPicOperations.init();

// 是否返回原图信息。0表示不返回原图信息，1表示返回原图信息，默认为0
op.is_pic_info = false;

let rule = QCloudPicOperationRule.init();

// 处理结果的文件路径名称，如以/开头，则存入指定文件夹中，否则，存入原图文件存储的同目录

rule.fileid = "test";

// 盲水印文字，需要经过 URL 安全的 Base64 编码。当 type 为3时必填，type 为1或2时无效。
rule.text = "123";

// 盲水印类型，有效值：1 半盲；2 全盲；3 文字
rule.type = .text;

op.rule = [rule];
put.picOperations = op;
put.setFinish { (outoutObject, error) in
    
};
QCloudCOSXMLService.defaultCOSXML().putWatermarkObject(put);
```

>?更多完整示例，请前往 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Swift/Examples/cases/PictureOperation.swift) 查看。


## 云上数据处理

下面示例展示了如何在上传图片时自动实现图片处理。

图片上传完成后，COS 会存储原始图片和已处理过的图片。后续用户可以通过普通的下载请求获取处理结果。

#### 示例代码
**Objective-C**

[//]: # (.cssg-snippet-process-with-pic-operation)
```objective-c
QCloudCICloudDataOperationsRequest* put = [QCloudCICloudDataOperationsRequest new];
    
// 对象键，是对象在 COS 上的完整路径，如果带目录的话，格式为 "video/xxx/movie.mp4"
put.object = @"exampleobject";
// 存储桶名称，由BucketName-Appid 组成，可以在COS控制台查看 https://console.cloud.tencent.com/cos5/bucket
put.bucket = @"examplebucket-1250000000";
    
QCloudPicOperations * op = [[QCloudPicOperations alloc]init];
    
// 是否返回原图信息。0表示不返回原图信息，1表示返回原图信息，默认为0
op.is_pic_info = NO;
QCloudPicOperationRule * rule = [[QCloudPicOperationRule alloc]init];
    
// 处理结果的文件路径名称，如以/开头，则存入指定文件夹中，否则，存入原图文件存储的同目录
rule.fileid = @"test";
    
// 盲水印文字，需要经过 URL 安全的 Base64 编码。当 type 为3时必填，type
rule.text = @"123"; // 水印文字只能是 [a-zA-Z0-9]
    
// 盲水印类型，有效值：1 半盲；2 全盲；3 文字
rule.type = QCloudPicOperationRuleText;
op.rule = @[rule];
put.picOperations = op;
   [put setFinishBlock:^(QCloudPutObjectWatermarkResult *outputObject, NSError *error) {
       
}];
[[QCloudCOSXMLService defaultCOSXML] CloudDataOperations:put];
```

>?更多完整示例，请前往 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Objc/Examples/cases/PictureOperation.m) 查看。


**Swift**

[//]: # (.cssg-snippet-process-with-pic-operation)
```swift
let put = QCloudCICloudDataOperationsRequest<AnyObject>();
        
// 对象键，是对象在 COS 上的完整路径，如果带目录的话，格式为 "video/xxx/movie.mp4"
put.object = "exampleobject";
// 存储桶名称，由BucketName-Appid 组成，可以在COS控制台查看 https://console.cloud.tencent.com/cos5/bucket
        
put.bucket = "examplebucket-1250000000";
let op = QCloudPicOperations.init();
        
// 是否返回原图信息。0表示不返回原图信息，1表示返回原图信息，默认为0
op.is_pic_info = false;
        
let rule = QCloudPicOperationRule.init();
        
// 处理结果的文件路径名称，如以/开头，则存入指定文件夹中，否则，存入原图文件存储的同目录
        
rule.fileid = "test";
        
// 盲水印文字，需要经过 URL 安全的 Base64 编码。当 type 为3时必填，type 为1或2时无效。
rule.text = "123";
        
// 盲水印类型，有效值：1 半盲；2 全盲；3 文字
rule.type = .text;
        
op.rule = [rule];
put.picOperations = op;
put.setFinish { (outoutObject, error) in
            
};
QCloudCOSXMLService.defaultCOSXML().cloudDataOperations(put);
```

>?更多完整示例，请前往 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Swift/Examples/cases/PictureOperation.swift) 查看。

