## Overview

This document provides an overview of APIs and SDK code samples for basic image processing.

<table>
   <tr>
      <th>Service</td>
      <th>Feature</td>
      <th>Description</td>
   </tr>
   <tr>
      <td rowspan=11>Basic image processing</td>
      <td><a href="https://intl.cloud.tencent.com/document/product/436/36366">Scaling</a></td>
      <td>Proportional scaling, scaling image to target width and height</td>
   </tr>
   <tr>
      <td><a href="https://intl.cloud.tencent.com/document/product/436/36367">Cropping</a></td>
      <td>Regular cropping, cropping and scaling, cropping to circle, smart face cropping</td>
   </tr>
   <tr>
      <td><a href="https://intl.cloud.tencent.com/document/product/436/36368">Rotation</a></td>
      <td>Adaptive rotation, regular rotation</td>
   </tr>
   <tr>
      <td><a href="https://intl.cloud.tencent.com/document/product/436/36369">Format conversion</a></td>
      <td>Format conversion, GIF format optimization, progressive display</td>
   </tr>
   <tr>
      <td><a href="https://intl.cloud.tencent.com/document/product/436/36370">Quality change</a></td>
      <td>Quality change for JPG and WebP images</td>
   </tr>
   <tr>
      <td><a href="https://intl.cloud.tencent.com/document/product/436/36371">Gaussian blurring</a></td>
      <td>Image blurring</td>
   </tr>
   <tr>
      <td><a href="https://intl.cloud.tencent.com/document/product/436/36372">Sharpening</a></td>
      <td>Image sharpening</td>
   </tr>
   <tr>
      <td>Watermarking</td>
      <td><a href="https://intl.cloud.tencent.com/document/product/436/36373">Image watermark</a>, <a href="https://intl.cloud.tencent.com/document/product/436/36374">text watermark</a></td>
   </tr>
   <tr>
      <td>Image information acquisition</td>
      <td><a href="https://intl.cloud.tencent.com/document/product/436/36375">Basic information</a>, <a href="https://intl.cloud.tencent.com/document/product/436/36376">EXIF information</a>, <a href="https://intl.cloud.tencent.com/document/product/436/36377">average hue</a></td>
   </tr>
   <tr>
      <td><a href="https://intl.cloud.tencent.com/document/product/436/36378">Metadata removal</a></td>
      <td>Including EXIF information</td>
   </tr>
   <tr>
      <td><a href="https://intl.cloud.tencent.com/document/product/436/36379">Quick thumbnail template</a></td>
      <td>Quick image format conversion, scaling, and cropping for thumbnail generation</td>
   </tr>
</table>



## SDK API References

For the parameters and method description of all the APIs in the SDK, see the [API documentation](https://cos-dotnet-sdk-doc-1253960454.file.myqcloud.com/).

## Processing Image During Upload

The following example shows how to automatically process an image when you upload it to COS.

When the image is uploaded successfully, COS will save both the original and the processed images. You can later obtain the processing results by using a general download request.

#### Sample code

[//]: #	".cssg-snippet-upload-with-pic-operation"

```cs
PutObjectRequest request = new PutObjectRequest(bucket, key, srcPath);

JObject o = new JObject();
// Do not return the input image
o["is_pic_info"] = 0;
JArray rules = new JArray();
JObject rule = new JObject();
rule["bucket"] = bucket;
rule["fileid"] = "desample_photo.jpg";
// Processing parameters. For rules, visit https://cloud.tencent.com/document/product/436/44879.
rule["rule"] = "imageMogr2/thumbnail/400x400";
rules.Add(rule);
o["rules"] = rules;

string ruleString = o.ToString(Formatting.None);
request.SetRequestHeader("Pic-Operations", ruleString);
// Execute the request
PutObjectResult result = cosXml.PutObject(request);
```

> ?For more complete samples, visit [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/PictureOperation.cs).

## Processing In-Cloud Image

The following example shows how to process an image stored in COS and save the processing result to COS.

#### Sample code

[//]: #	".cssg-snippet-process-with-pic-operation"

```cs
JObject o = new JObject();
// Do not return the input image
o["is_pic_info"] = 0;
JArray rules = new JArray();
JObject rule = new JObject();
rule["bucket"] = bucket;
rule["fileid"] = "desample_photo.jpg";
// Processing parameters. For rules, visit https://cloud.tencent.com/document/product/436/44879.
rule["rule"] = "imageMogr2/thumbnail/400x400";
rules.Add(rule);
o["rules"] = rules;
string ruleString = o.ToString(Formatting.None);

ImageProcessRequest request = new ImageProcessRequest(bucket, key, ruleString);
ImageProcessResult result = cosXml.ImageProcess(request);
```

> ?For more complete samples, visit [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/PictureOperation.cs).

## Processing Image During Download

The following example shows how to process an image stored in COS during download.

#### Sample code

[//]: #	".cssg-snippet-download-with-pic-operation"

```cs
GetObjectRequest getObjectRequest = new GetObjectRequest(bucket, key, localDir, localFileName);
// Processing parameters. This sample converts the image into TPG format. For the rules, visit https://cloud.tencent.com/document/product/436/44879.
getObjectRequest.SetQueryParameter("imageMogr2/format/tpg", null);
```

> ?For more complete samples, visit [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/PictureOperation.cs).
