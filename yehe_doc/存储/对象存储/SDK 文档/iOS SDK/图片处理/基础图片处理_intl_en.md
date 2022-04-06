## Overview


This document provides an overview of APIs and SDK code samples related to basic image processing.

<table>
   <tr>
      <th>Service</td>
      <th>Feature</td>
      <th>Description</td>
   </tr>
   <tr>
      <td rowspan=11>Image Processing-Basic Services</td>
      <td><a href="https://intl.cloud.tencent.com/document/product/436/36366">Scaling</a></td>
      <td>Proportional scaling, scaling image to target width and height, and more</td>
   </tr>
   <tr>
      <td><a href="https://intl.cloud.tencent.com/document/product/436/36367">Cropping</a></td>
      <td>Cut (regular cropping), crop (scaling and cropping), iradius (inscribed circle cropping), and scrop (smart cropping)</td>
   </tr>
   <tr>
      <td><a href="https://intl.cloud.tencent.com/document/product/436/36368">Rotation</a></td>
      <td>Adaptive rotation and common rotation</td>
   </tr>
   <tr>
      <td><a href="https://intl.cloud.tencent.com/document/product/436/36369">Format conversion</a></td>
      <td>Format conversion, GIF optimization, and progressive display</td>
   </tr>
   <tr>
      <td><a href="https://intl.cloud.tencent.com/document/product/436/36370">Quality conversion</a></td>
      <td>Changes the quality of images in JPG and WEBP formats</td>
   </tr>
   <tr>
      <td><a href="https://intl.cloud.tencent.com/document/product/436/36371">Gaussian blurring</a></td>
      <td>Blurs images</td>
   </tr>
   <tr>
      <td><a href="https://intl.cloud.tencent.com/document/product/436/36372">Sharpening</a></td>
      <td>Sharpens images</td>
   </tr>
   <tr>
      <td>Watermarking</td>
      <td><a href="https://intl.cloud.tencent.com/document/product/436/36373">Image watermarks</a>, <a href="https://intl.cloud.tencent.com/document/product/436/36374">text watermarks</a></td>
   </tr>
   <tr>
      <td>Obtaining image information</td>
      <td><a href="https://intl.cloud.tencent.com/document/product/436/36375">Basic information</a>, <a href="https://intl.cloud.tencent.com/document/product/436/36376">EXIF data</a>, <a href="https://intl.cloud.tencent.com/document/product/436/36377">average hue</a></td>
   </tr>
   <tr>
      <td><a href="https://intl.cloud.tencent.com/document/product/436/36378">Removing metadata</a></td>
      <td>Includes EXIF data</td>
   </tr>
   <tr>
      <td><a href="https://intl.cloud.tencent.com/document/product/436/36379">Quick thumbnail template</a></td>
      <td>Performs quick format conversion, scaling, and cropping to generate thumbnails</td>
   </tr>
</table>


## SDK API References

For parameters and method description of all APIs in the SDK, please see [SDK API Reference](https://cos-ios-sdk-doc-1253960454.file.myqcloud.com/).

## Processing an Image upon the Upload

The following example shows how to automatically process an image when you upload it to COS.

When the image is uploaded successfully, COS will save both the input and output images. You can later obtain the processing results using a general download request.

#### Sample code
**Objective-C**

[//]: # (.cssg-snippet-upload-with-pic-operation)
```objective-c
QCloudPutObjectWatermarkRequest* put = [QCloudPutObjectWatermarkRequest new];

// Object key, i.e., the full path of a COS object. If the object is in a directory, the path should be "video/xxx/movie.mp4"
put.object = @"exampleobject";
// Bucket name in the format of BucketName-Appid, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
put.bucket = @"examplebucket-1250000000";

put.body =  [@"123456789" dataUsingEncoding:NSUTF8StringEncoding];
QCloudPicOperations * op = [[QCloudPicOperations alloc]init];

// Indicate whether to return information of the original image. `0` (default): no; `1`: yes
op.is_pic_info = NO;
QCloudPicOperationRule * rule = [[QCloudPicOperationRule alloc]init];

// Path of processing result file. If the path starts with `/`, the result file is stored in the specified folder. Otherwise, it is stored in the same directory as the input image file.
rule.fileid = @"test";

// Blind watermark text, which must be URL-safe Base64-encoded. This parameter is required if `type` is set to `3` and does not take effect if `type` is set to `1` or `2`.
rule.text = @"123"; // The watermark text can only be a string of [a-z, A-Z, 0-9]

// Blind watermark type. Valid values: `1` (semi-blind), `2` (perfectly blind), `3` (text)
rule.type = QCloudPicOperationRuleText;
op.rule = @[rule];
put.picOperations = op;
[put setFinishBlock:^(id outputObject, NSError *error) {
   
}];
[[QCloudCOSXMLService defaultCOSXML] PutWatermarkObject:put];
```

>?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Objc/Examples/cases/PictureOperation.m).


**Swift**

[//]: # (.cssg-snippet-upload-with-pic-operation)
```swift
let put = QCloudPutObjectWatermarkRequest<AnyObject>();

// Object key, i.e., the full path of a COS object. If the object is in a directory, the path should be "video/xxx/movie.mp4"
put.object = "exampleobject";
// Bucket name in the format of BucketName-Appid, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket

put.bucket = "examplebucket-1250000000";
put.body = "123456789".data(using: .utf8)! as NSData;
let op = QCloudPicOperations.init();

// Indicate whether to return information of the original image. `0` (default): no; `1`: yes
op.is_pic_info = false;

let rule = QCloudPicOperationRule.init();

// Path of processing result file. If the path starts with `/`, the result file is stored in the specified folder. Otherwise, it is stored in the same directory as the input image file.

rule.fileid = "test";

// Blind watermark text, which must be URL-safe Base64-encoded. This parameter is required if `type` is set to `3` and does not take effect if `type` is set to `1` or `2`.
rule.text = "123";

// Blind watermark type. Valid values: `1` (semi-blind), `2` (perfectly blind), `3` (text)
rule.type = .text;

op.rule = [rule];
put.picOperations = op;
put.setFinish { (outoutObject, error) in
    
};
QCloudCOSXMLService.defaultCOSXML().putWatermarkObject(put);
```

>?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Swift/Examples/cases/PictureOperation.swift).


## Processing In-Cloud Data

The following example shows how to automatically process an image when you upload it to COS.

When the image is uploaded successfully, COS will save both the input and output images. You can later obtain the processing results using a general download request.

#### Sample code
**Objective-C**

[//]: # (.cssg-snippet-process-with-pic-operation)
```objective-c
QCloudCICloudDataOperationsRequest* put = [QCloudCICloudDataOperationsRequest new];
    
// Object key, i.e., the full path of a COS object. If the object is in a directory, the path should be "video/xxx/movie.mp4"
put.object = @"exampleobject";
// Bucket name in the format of BucketName-Appid, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
put.bucket = @"examplebucket-1250000000";
    
QCloudPicOperations * op = [[QCloudPicOperations alloc]init];
    
// Indicate whether to return information of the original image. `0` (default): no; `1`: yes
op.is_pic_info = NO;
QCloudPicOperationRule * rule = [[QCloudPicOperationRule alloc]init];
    
// Path of processing result file. If the path starts with `/`, the result file is stored in the specified folder. Otherwise, it is stored in the same directory as the input image file.
rule.fileid = @"test";
    
// Blind watermark text, which must be URL-safe Base64-encoded. This parameter is required if `type` is set to `3` and does not take effect if `type` is set to `1` or `2`.
rule.text = @"123"; // The watermark text can only be a string of [a-z, A-Z, 0-9]
    
// Blind watermark type. Valid values: `1` (semi-blind), `2` (perfectly blind), `3` (text)
rule.type = QCloudPicOperationRuleText;
op.rule = @[rule];
put.picOperations = op;
   [put setFinishBlock:^(QCloudPutObjectWatermarkResult *outputObject, NSError *error) {
       
}];
[[QCloudCOSXMLService defaultCOSXML] CloudDataOperations:put];
```

>?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Objc/Examples/cases/PictureOperation.m).


**Swift**

[//]: # (.cssg-snippet-process-with-pic-operation)
```swift
let put = QCloudCICloudDataOperationsRequest<AnyObject>();
        
// Object key, i.e., the full path of a COS object. If the object is in a directory, the path should be "video/xxx/movie.mp4"
put.object = "exampleobject";
// Bucket name in the format of BucketName-Appid, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
        
put.bucket = "examplebucket-1250000000";
let op = QCloudPicOperations.init();
        
// Indicate whether to return information of the original image. `0` (default): no; `1`: yes
op.is_pic_info = false;
        
let rule = QCloudPicOperationRule.init();
        
// Path of processing result file. If the path starts with `/`, the result file is stored in the specified folder. Otherwise, it is stored in the same directory as the input image file.
        
rule.fileid = "test";
        
// Blind watermark text, which must be URL-safe Base64-encoded. This parameter is required if `type` is set to `3` and does not take effect if `type` is set to `1` or `2`.
rule.text = "123";
        
// Blind watermark type. Valid values: `1` (semi-blind), `2` (perfectly blind), `3` (text)
rule.type = .text;
        
op.rule = [rule];
put.picOperations = op;
put.setFinish { (outoutObject, error) in
            
};
QCloudCOSXMLService.defaultCOSXML().cloudDataOperations(put);
```

>?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Swift/Examples/cases/PictureOperation.swift).

