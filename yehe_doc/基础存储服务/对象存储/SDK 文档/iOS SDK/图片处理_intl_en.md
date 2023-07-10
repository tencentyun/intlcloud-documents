## Overview

COS has integrated [Cloud Infinite](https://intl.cloud.tencent.com/document/product/1045) (CI), a one-stop professional multimedia solution that offers the image processing features outlined below. For more information, see [Image Processing Overview](https://intl.cloud.tencent.com/document/product/436/35280).

<table>
   <tr>
      <th>Service</td>
      <th>Feature</td>
      <th>Description</td>
   </tr>
   <tr>
      <td rowspan=12>Basic image processing service</td>
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
      <td><a href="https://intl.cloud.tencent.com/document/product/436/36371">Gaussian blur</a></td>
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
   <tr>
      <td><a href="https://intl.cloud.tencent.com/document/product/1045/33443">Setting style</a></td>
      <td>Sets image styles to easily manage images for different purposes</td>
   </tr>
</table>


## SDK API Reference

For the parameters and method descriptions of all the APIs in the SDK, please see [SDK API Reference](https://cos-ios-sdk-doc-1253960454.file.myqcloud.com/).

## Using Image Processing when Uploading

The following example shows how COS automatically processes an image when you upload it.

Upon successful upload, COS will save both the original and processed images. You can obtain the processing result using a common download request.

#### Sample code
**Objective-C**

[//]: # ".cssg-snippet-upload-with-pic-operation"
```objective-c
QCloudPutObjectWatermarkRequest* put = [QCloudPutObjectWatermarkRequest new];

// Object key, i.e. the full path of a COS object. If the object is in a directory, the path should be "dir1/object1"
put.object = @"exampleobject";
// Bucket name in the format: `BucketName-APPID`
put.bucket = @"examplebucket-1250000000";

put.body =  [@"123456789" dataUsingEncoding:NSUTF8StringEncoding];
QCloudPicOperations * op = [[QCloudPicOperations alloc]init];

// Indicate whether to return information on the original image. “0” (default): no; “1”: yes.
op.is_pic_info = NO;
QCloudPicOperationRule * rule = [[QCloudPicOperationRule alloc]init];

// File path of the processing result. If it starts with “/”, the result is stored in the specified folder. Otherwise, it is stored in the same directory as the original image file.
rule.fileid = @"test";

```

>?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Objc/Examples/cases/PictureOperation.m).


**Swift**

[//]: # ".cssg-snippet-upload-with-pic-operation"
```swift
let put = QCloudPutObjectWatermarkRequest<AnyObject>();

// Object key, i.e. the full path of a COS object. If the object is in a directory, the path should be "dir1/object1"
put.object = "exampleobject";
// Bucket name in the format: `BucketName-APPID`

put.bucket = "examplebucket-1250000000";
put.body = "123456789".data(using: .utf8)! as NSData;
let op = QCloudPicOperations.init();

// Indicate whether to return information on the original image. “0” (default): no; “1”: yes.
op.is_pic_info = false;

let rule = QCloudPicOperationRule.init();

// File path of the processing result. If it starts with “/”, the result is stored in the specified folder. Otherwise, it is stored in the same directory as the original image file.

rule.fileid = "test";
```

>?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Swift/Examples/cases/PictureOperation.swift).



```

```
