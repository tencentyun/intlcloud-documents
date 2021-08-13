## Overview

COS has integrated [Cloud Infinite](https://intl.cloud.tencent.com/document/product/1045) (CI), a one-stop professional multimedia solution that offers the image processing features outlined below. For more information, please see [Image Processing Overview](https://intl.cloud.tencent.com/document/product/436/35280).

<table>
   <tr>
      <th>Service</td>
      <th>Feature</td>
      <th>Description</td>
   </tr>
   <tr>
      <td rowspan=11>Basic image processing service</td>
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


## SDK API Reference

For the parameters and method descriptions of all the APIs in the SDK, please see [SDK API Reference](https://cos-android-sdk-doc-1253960454.file.myqcloud.com/).

## Processing an Image upon the Upload

The following example shows how to automatically process an image when you upload it to COS.

When the image is uploaded successfully, COS will save both the input and output images. You can later obtain the processing results using a general download request.

#### Sample code

[//]: # ".cssg-snippet-upload-with-pic-operation"
```java
List<PicOperationRule> rules = new LinkedList<>();
// Add a rule to convert the image to PNG format, and the resulting image will be saved in a bucket with a location identifier in the format:
// examplepngobject
rules.add(new PicOperationRule("examplepngobject", "imageView2/format/png"));
PicOperations picOperations = new PicOperations(true, rules);

PutObjectRequest putObjectRequest = new PutObjectRequest(bucket, cosPath, srcPath);
putObjectRequest.setPicOperations(picOperations);

// If the upload is successful, you will get 2 images: the original and the processed images
COSXMLUploadTask cosxmlUploadTask = transferManager.upload(bucket, cosPath,
        srcPath, uploadId);
```

>?For more samples, please visit [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/Android/app/src/androidTest/java/com/tencent/qcloud/cosxml/cssg/PictureOperation.java).

