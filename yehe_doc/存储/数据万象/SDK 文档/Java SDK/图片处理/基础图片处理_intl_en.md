## Overview

COS has integrated [Cloud Infinite](https://www.tencentcloud.com/document/product/1045) (CI), a one-stop professional multimedia solution that offers the image processing features outlined below. For more information, see [Image Processing Overview](https://intl.cloud.tencent.com/document/product/436/35280).

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


## Basic Image Processing

When performing basic image processing, you need to specify the image processing rule. For more information, see [Image Processing Overview](https://intl.cloud.tencent.com/document/product/436/35280).
For all the code samples, visit [GitHub](https://github.com/tencentyun/cos-java-sdk-v5/blob/master/src/main/java/com/qcloud/cos/demo/ci/BasicImageProcessing.java).
Below are some examples:

### Scaling

```java
String bucketName = "examplebucket-1250000000";
String key = "qrcode.png";
GetObjectRequest getObj = new GetObjectRequest(bucketName, key);
// Scale the width and height to 50% of the input image
String rule = "imageMogr2/thumbnail/!50p";
getObj.putCustomQueryParameter(rule, null);
cosClient.getObject(getObj, new File("qrcode-50p.png"));
```

### Cropping

```java
String bucketName = "examplebucket-1250000000";
String key = "qrcode.png";
GetObjectRequest getObj = new GetObjectRequest(bucketName, key);
// Crop the radius of an inscribed circle to an integer greater than zero and less than half of the shorter side of the input image. The center of the inscribed circle is the center of the image.
String rule = "imageMogr2/iradius/150";
getObj.putCustomQueryParameter(rule, null);
cosClient.getObject(getObj, new File("qrcode-cropping.png"));
```

### Rotation

```java
String bucketName = "examplebucket-1250000000";
String key = "qrcode.png";
GetObjectRequest getObj = new GetObjectRequest(bucketName, key);
// Rotate clockwise by 90 degrees
String rule = "imageMogr2/rotate/90";
getObj.putCustomQueryParameter(rule, null);
cosClient.getObject(getObj, new File("qrcode-rotate.png"));
```







